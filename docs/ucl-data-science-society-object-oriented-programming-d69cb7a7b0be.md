# UCL 数据科学学会:面向对象编程介绍

> 原文：<https://towardsdatascience.com/ucl-data-science-society-object-oriented-programming-d69cb7a7b0be?source=collection_archive---------32----------------------->

## 工作坊 4:什么是 OOP，在 Python 中定义类、添加属性、添加方法、类继承

![](img/ee3538869e152c25d2ee6deb0fc71402.png)

克里斯托夫·高尔在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

今年，作为 UCL 数据科学学会的科学负责人，该学会将在整个学年举办一系列 20 场研讨会，涵盖的主题包括数据科学家工具包 Python 和机器学习方法简介。对于我所展示和交付的每一个，我的目标是创建一系列的小博客，这些小博客将概述主要观点，并为任何希望跟进的人提供完整研讨会的链接。所有这些都可以在我们的 [GitHub](https://github.com/UCL-DSS) 上找到，并将在全年更新新的研讨会和挑战。

第四个工作坊是对面向对象编程的介绍，我们将向你介绍如何定义一个类，添加属性，添加方法和类继承。虽然这里将分享一些亮点，但完整的研讨会，包括问题表，可以在[这里](https://github.com/UCL-DSS/Object_oriented_programming)找到。

如果您错过了之前的研讨会，可以在这里找到:

*   [Python 基础知识](/ucl-data-science-society-python-fundamentals-3fb30ec020fa)
*   [Python 序列](/ucl-data-science-society-python-sequences-e3ffa67604a0)
*   [Python 逻辑](/ucl-data-science-society-python-logic-3eb847362a97)

## **面向对象编程**

首先，什么是面向对象编程？首先，这是一种组织代码的方式，可以将特征和行为数据捆绑到一个结构中。这种结构允许你使用类作为蓝图来创建多个对象，遵循**不要重复**的主要编码原则之一。这允许您在整个代码中创建对象，允许您在整个工作流的不同点访问相同的信息或功能。

这与数据科学社区中经常使用的过程化编程形成对比，在过程化编程中，代码遵循一系列步骤，以便使用函数和代码块来完成任务。这可以在之前的研讨会中看到，我们使用 jupyter 笔记本中的代码块一点一点地完成序列。

然而，面向对象编程的好处是，你可以用一种简单易行的方式存储数据和你想在多个不同的条目中执行的相关动作，同时允许你创建一个可以反复使用的蓝图。当您知道每个实例都有某些特征，并且您可能希望反复对这些数据执行相同的功能时，这将非常有用。这方面的一个例子可以是存储关于雇员的数据，由此他们每个人都有工资、水平经验或级别，并且共同的行动包括工作周年纪念或晋升。

## **定义一个类别**

我们可以通过定义一个类来实现这个处理雇员数据的蓝图。这是一种结构和/或蓝图，允许我们在未来创建特定的对象，以相同的属性和功能反复使用。

这是使用关键字 **class** 完成的，后面是包含方法的缩进块。这方面的一个例子是:

```
class Employee:

    pass
```

这里我们简单地定义了一个 Employee 类，它将 pass 作为唯一的当前属性，这意味着我们没有当前功能。我们可以通过创建该对象的实例来检查我们是否创建了一个类，并检查它是否是该类的一部分:

```
juliet = Employee()juliet.__class__.__name__#out:
'Employee'
```

很好，现在我们知道我们有员工了！

**添加属性**

创建一个类并使其真正有用的下一步是开始添加属性。这是 don 使用的`__init__()`方法，该方法在创建类的实例(对象)时被调用。

出于我们的目的，因为我们有一个雇员，我们想要分配一个工资、一个级别和工作年限:

```
#define the employee class
class Employee:

    #add the constructor method with associated attributes
    def __init__(self, wage, grade, years_worked):
        self.wage = wage
        self.grade = grade
        self.exp = years_worked

#create an instance of that employee     
juliet = Employee(30_000, 1, 1)
```

我们现在有了我们想要的属性。在这一点上，注意到 **self** 参数作为第一个参数被传递是很重要的，即使它没有在代码中被显式地传递。在类中定义属性或方法就是这种情况，以确保我们将属性分配给特定的类。

那么如何访问这些信息呢？既然我们已经创建了该实例，我们可能希望在以后访问这些信息。我们可以使用点符号来实现这一点，这意味着我们可以将`.`和属性名放在实例之后来访问它。在这种情况下，对于朱丽叶，我们可以这样做:

```
print("Juliet's wage is:", juliet.wage)
print("Juliet's grade is:", juliet.grade)
print("Juliet has worked for", juliet.exp, "years")#out:
Juliet's wage is: 30000
Juliet's grade is: 1
Juliet has worked for 1 years
```

好吧，我们可以访问这个，太好了，但是改变这些信息呢？嗯，就像 Python 中的普通变量一样，我们也可以使用`=`结合上面的点符号来更新信息。例如，如果我们想给朱莉加薪，那么我们可以这样做:

```
#print out the current information
print(f"Juliet's current wage is: {juliet.wage}")
print(f"Juliet's current grade is: {juliet.grade}")
print("\n")juliet.wage += 5000
juliet.grade += 1#print out the new information
print(f"Juliet's new wage is: {juliet.wage}")
print(f"Juliet's new grade is: {juliet.grade}")#out: 
Juliet's current wage is: 30000
Juliet's current grade is: 1Juliet's new wage is: 35000
Juliet's new grade is: 2
```

然而，这样做可能会很痛苦！如果我们有成千上万的这些记录呢？有没有更简单的方法？是的有！

**添加方法**

我们可以通过向我们的类中添加方法来简化这一点，以便能够执行我们知道是例行的或将在类中的数据存储上经常使用的操作。在我们的案例中，这可以是给我们的员工升职，从而提高他们的工资和级别，或者我们的员工有一个工作纪念日，从而增加他们为公司工作的年限。

在这里，我们可以通过创建一个方法来关注第一个示例，该方法给我们的员工一个标准工资增加 10%并且级别增加 1 的晋升(在我看来这是一个很好的晋升！).我们可以这样实现:

```
#create the employee class
class Employee:

    #add the init constructor in the same way we have done already 
    def __init__(self, wage = 20_000, grade=1, years_worked=0):
        self.wage = wage
        self.grade = grade
        self.exp = years_worked

    #add a promotion method
    #with assumed values
    def promotion(self, wage_increase = 10, grade_increase = 1):
        self.wage += wage_increase/100 * self.wage
        self.grade += grade_increase
```

然后，我们可以使用如下晋升方法给 Juliet 加薪:

```
juliet = Employee(30_000, 1, 1)#Checking the original objects attributes
print("Juliet's wage is:", juliet.wage)
print("Juliet's grade is:", juliet.grade)
print("Juliet has worked for", juliet.exp, "years\n")#Giving William and promotion
print("Juliet has got a promotion\n")
juliet.promotion()#Checking to see that the grade and wage have changed
print("Juliet's wage is now:", juliet.wage)
print("Juliet's grade is now:", juliet.grade)#out:
Juliet's wage is: 30000
Juliet's grade is: 1
Juliet has worked for 1 years

Juliet has got a promotion

Juliet's wage is now: 33000.0
Juliet's grade is now: 2
```

我们可以看到，这将使生活变得更加简单，特别是如果我们向多人提供不止一次的推广，还允许我们灵活地改变推广的规模。

但是，如果我们有不同类型、不同特点的员工，那会怎么样呢？

## 类继承

在代码中使用类的好处是，类可以从其他类继承属性和方法。这在编程的许多方面都很有用，并且允许您在不想重新编写的现有功能的基础上进行构建。

从本质上讲，这允许您定义一个新的类来获得原始类的所有功能，但是您可以添加额外的功能。实现这一点的方法是通过以下符号:

```
class MyChild(MyParent):     
    pass
```

其中 MyParent 是其功能由 MyChild 类扩展/继承的类。出于我们的目的，我们可以创建一个数据科学家员工，他最初与原来的员工没有什么不同:

```
#ctreate the Data Scientist class inheriting from the Employee class
class DataScientist(Employee):

    #add no new functionality for now
    pass#create an instance of jessicae
jessica = DataScientist(70_000, 6, 10)#print Jessica's wage
print(f"Jessica's current wage is: {jessica.wage}")#give her a promotion
jessica.promotion()print(f"Jessica's new wage is: {jessica.wage}")#out:
Jessica's current wage is: 70000
Jessica's new wage is: 77000.0
```

在这里，我们可以看到我们拥有原始父类的所有功能，而不必编写太多代码。

然而，我们当然对扩展这个原始父类的功能感兴趣，以允许数据科学家有不同的行为。在我们的案例中，我们希望数据科学家具有他们所知道的语言属性，并且有能力学习一门新的语言，这可能会导致工资增加，而无需必要的晋升。我们可以这样做:

```
#create the Data Scientist class inheriting from the employee class
class DataScientist(Employee): 

    #child's initialisation
    def __init__(self, wage = 20_000, 
                grade=1, years_worked=0,
                 p_languages = []):
        #use the parents initialisation
        Employee.__init__(self, wage, 
                          grade, years_worked)
        #new characteristics to add
        self.languages = p_languages

    #add language learning functionality
    def learn_lang(self, new_lang, promotion = False, wage_increase = 10,
                  grade_increase = 0):
        #add the new language
        self.languages.append(new_lang)

        #if promotion is true
        if promotion == True:
            #add promotion
            self.promotion(wage_increase,
                          grade_increase)
```

这可以实现为:

```
#create new DataScientist
jessica = DataScientist(80000, 7, 15, ["Python", "R", "SQL"])#Print her current languages and wage    
print(f"Jessica's current languages are {jessica.languages}")
print(f"Jessica's current wage is £{jessica.wage}")
print(f"Jessica's current grade is {jessica.grade}")#She learns a language 
#so we give her a promotion
jessica.learn_lang("JavaScript", promotion = True)#check what languages she now knows
print(f"Jessica's new languages are {jessica.languages}")
print(f"Jessica's new wage is £{jessica.wage}")
print(f"Jessica's new grade is {jessica.grade}")#out:

Jessica's current languages are ['Python', 'R', 'SQL'] 
Jessica's current wage is £80000 
Jessica's current grade is 7 Jessica's new languages are ['Python', 'R', 'SQL', 'JavaScript'] Jessica's new wage is £88000.0 
Jessica's new grade is 7
```

这样，我们就有了面向对象编程的基础！当然，还有很多东西需要学习，包括装饰器、类方法和其他功能，但是我们希望这已经给了你一个很好的基础，如果你有兴趣的话，可以继续学习！

完整的研讨会笔记，以及进一步的示例和挑战，可以在 这里找到 [**。如果您想了解我们协会的更多信息，请随时关注我们的社交网站:**](https://github.com/UCL-DSS/Object_oriented_programming7)

https://www.facebook.com/ucldata[脸书](https://www.facebook.com/ucldata)

insta gram:[https://www.instagram.com/ucl.datasci/](https://www.instagram.com/ucl.datasci/)

领英:【https://www.linkedin.com/company/ucldata/ 

如果你想了解 UCL 数据科学协会和其他优秀作者的最新信息，请使用我下面的推荐代码注册 medium。

<https://philip-wilkinson.medium.com/membership>  </univariate-outlier-detection-in-python-40b621295bc5>  </introduction-to-hierarchical-clustering-part-1-theory-linkage-and-affinity-e3b6a4817702>  </introduction-to-decision-tree-classifiers-from-scikit-learn-32cd5d23f4d> [## scikit-learn 决策树分类器简介

towardsdatascience.com](/introduction-to-decision-tree-classifiers-from-scikit-learn-32cd5d23f4d)