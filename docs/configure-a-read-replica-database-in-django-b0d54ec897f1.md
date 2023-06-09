# 在 Django 中配置读取副本数据库

> 原文：<https://towardsdatascience.com/configure-a-read-replica-database-in-django-b0d54ec897f1?source=collection_archive---------29----------------------->

## 软件开发

## 何时以及如何在 Django 中配置读取副本数据库

![](img/7b25fe4477f64822e3044124e326c3b6.png)

图片由[海燕](https://unsplash.com/@petrebels)在 [Unsplash](https://unsplash.com/photos/JwMGy1h-JsY) 上拍摄

# 何时以及如何在 Django 中配置读取副本数据库

在软件工程中，最关键的步骤之一是架构的选择，以至于选择中的任何错误都可能导致网站出现故障，从而对业务绩效产生不利影响。

通常，与系统性能相关的问题，尤其是对于大型复杂的系统，对于维护和诊断是至关重要的，因为它们可能与不同的软件环境相关。这些问题可能由多种因素引起，包括硬件、软件或网络相关问题。

下一篇文章将讨论与[数据库](https://www.dtm.io/blog/tag/database/)性能相关的问题，以及使用读取副本减轻这些问题的方法。我目前的体验是基于部署在谷歌云平台上的 [App Engine](https://cloud.google.com/appengine) 应用和 [PostgreSQL 复制](https://cloud.google.com/sql/docs/postgres/replication)。

## 数据库中的性能问题

在大多数情况下，由于与数据库性能相关的问题，系统会变得混乱。造成这种情况的因素有很多，最常见的是选择了错误的模式设计。因此，如果在牢记预期操作的同时没有正确设计，[数据库](https://www.dtm.io/blog/tag/database/)将最终表现不佳。相反，一个设计良好的模式不一定能达到标准，因为许多其他因素会影响它的性能，例如连接数、压力或负载处理能力，或者数据库要处理的数据量。例如，当单个数据库处理大量用户(考虑几千个)时，它将遇到大量连接命中，并且它不一定有资源来实时满足这些命中。因此，为了缓解这种情况，引入了副本的概念。

## 数据库副本

关于软件和硬件的术语“复制”是指利用特定资源的多个副本(或复制品)来改善/增强性能、服务可用性和容错的过程。关于[数据库](https://www.dtm.io/blog/tag/database/)系统中的复制，通常认为多台服务器在处理相同的数据。有多种配置和过程可用于将复制合并到数据库中:

*   在所有情况下都允许读或写命令。
*   多个只读实例和一个主实例(允许读/写命令)。注意，在这种模式中，数据复制和同步可以以同步和异步方式执行。

## 在 Django 中处理读取副本配置

在 [Django](https://www.dtm.io/blog/tag/django/) 应用中配置和使用读取副本之前，应考虑以下两点:

*   读取副本实例应该在 Django 应用程序中声明为数据库。
*   需要配置路由器来选择相应的读取副本。

**在 Django 中声明读取副本实例为数据库的程序**

在 [Django](https://www.dtm.io/blog/tag/django/) 中将读取副本配置和声明为数据库的方法包括设置 Django 设置文件。如上所述，我们将设置一个默认的单个主实例(允许读/写的服务器)[数据库](https://www.dtm.io/blog/tag/database/)，而读副本将被声明为附加数据库。例如，考虑到已经配置了两个复制副本，settings.py 文件应该如下所示:

```
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "HOST": "/cloudsql/project-id:region:master-instance-id",
        "NAME": "pg_master",
        "USER": "pg_user",
        "PASSWORD": "master_password",
    },
    "replica_1": {
        "ENGINE": "django.db.backends.postgresql", 
        "HOST": "/cloudsql/project-id:region:replica1-instance-id",
        "NAME": "pg_replica1",
        "USER": "pg_user",
        "PASSWORD": "replica1_password",
    },
    "replica_2": {
        "ENGINE": "django.db.backends.postgresql",
        "HOST": "/cloudsql/project-id:region:replica2-instance-id",
        "NAME": "pg_replica2",
        "USER": "pg_user",
        "PASSWORD": "replica2_password",
    }
}
```

一旦配置完成，这两个副本就可以通过 [Django](https://www.dtm.io/blog/tag/django/) 应用程序使用了。我们可以通过使用 QuerySet API 的方法[来再次确认这一点。例如，可以使用以下命令从主数据库和副本数据库检查 **Lead** 模型的可访问性:](https://docs.djangoproject.com/en/2.2/ref/models/querysets/#using)

```
# Here the leads are retrieved from the master instance:
Lead.objects.all()# Here the leads are retrieved from the replica instance 1:
Lead.objects.using('replica_1').all()# Here the leads are retrieved from the replica instance 2:
Lead.objects.using('replica_2').all()
```

也可以在通过传递“using”参数的“ [save](https://docs.djangoproject.com/en/2.2/topics/db/multi-db/#selecting-a-database-for-save) 方法保存对象时，将给定的[数据库](https://www.dtm.io/blog/tag/database/)设置为可用。请注意，在一个读取副本中保存对象时，将会遇到错误，因为实例只允许读取操作，不允许写入。

**路由器配置有助于在需要时访问特定的读取副本**

一旦在 [Django](https://www.dtm.io/blog/tag/django/) 应用程序中配置了副本实例，并且确保了可访问性，软件开发人员就以这样的方式设计程序，即在适当的相应副本上执行只读操作。因此，默认情况下，这种方法会妨碍可扩展性，因为它更像是配置复制副本实例选择的手动过程。这意味着将来添加更多的副本将需要修改代码并手动配置路由过程。

然而，手动配置的另一个聪明的方法是使用 Django 的数据库路由器。在这种配置中，可以创建定制的路由器，它自动选择默认实例来执行写操作，或者选择随机选择的副本来执行读操作。下面是自定义路由器配置，显示了该过程的工作原理:

```
class DatabaseRouter:
    def db_for_read(self, model, **hints):
        return random.choice(['replica_1', 'replica_2']) def db_for_write(self, model, **hints):
        return 'default' def allow_relation(self, obj1, obj2, **hints):
        return True def allow_migrate(self, db, label, model=None, **hints):
        return True
```

按照上面的过程，现在我们需要通过设置默认的数据库路由来更新“setting.py”文件:

```
DATABASE_ROUTERS = ['app.router.DatabaseRouter']
```

一旦更改生效，应用程序中的所有读取操作将被路由到副本，写入操作将被定向到主实例。

## 结论

总结一下我们的讨论，在 Django 中打开读取副本实例的过程非常简单。此外，它有助于增强应用程序的性能以及整个系统的功能。在我们原始代码的基础上，对配置文件和设置进行微小的修改，就可以让事情朝着对系统有利的方向发展。

感谢阅读这篇文章！如果你有任何问题，请在下面留言。另外，看看我以前的文章，你可能会喜欢:

</data-structures-simplified-and-classified-e0c1e304436b>  <https://vpodk.medium.com/principles-of-software-engineering-6b702faf74a6> 