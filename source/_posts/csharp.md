title: C#面向对象的学习笔记
date: 2017-03-05 01:45:41
desc: 
tags: [lang] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/csharp.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/csharp.jpg
---

像我这种 C with class 的使用者，把 class 拿来当 struct 来用，还用来做 OJ 的题目之外，好像没有什么其他用途了。以前看到 C++ 里面类的时候，也只是大概浏览了一下，现在我觉得可以边看边学边记。

<!-- more -->

学 Java 的时候跑回来翻了翻，发现一大堆错 23333。

深入学习下去以后。在我学习了 Java 以后，CSharp 的设计真的很像很像 java，甚至我觉得把这篇文章改改，就变成了 java 的学习笔记（笑）。一开始可能会有很多不懂的地方，都是学习了 Java 之后才能理解，写了一点 C++ 之后才能理解的。我不能说我完全掌握了，但是还是能解释一些现象。

## 定义

我觉得，面对对象这一概念是模糊的，你知道有这个东西，你知道怎么使用，却很难描述清楚它是什么。

百度百科的解释：

```
面向对象(Object Oriented,OO)是软件开发方法。

起初，“面向对象”是专指在程序设计中采用封装、继承、多态等设计方法。

```

你知道他是好东西就行了 =w=

## C# 封装

### Public
Public 访问修饰符 允许一个类将其成员变量和成员函数暴露给其他的函数和对象。任何公有成员可以被外部的类访问。

### Private
Private 访问修饰符 允许一个类将其成员变量和成员函数对其他的函数和对象进行隐藏。只有同一个类中的函数可以访问它的私有成员。即使是类的实例也不能访问它的私有成员。

### Protected
Protected 访问修饰符 允许子类访问它的基类的成员变量和成员函数。

### Internal
Internal 访问说明符允许一个类将其成员变量和成员函数暴露给当前程序中的其他函数和对象。internal 访问是对同一程序集内可访问

### Protected internal
Protected Internal 访问修饰符允许一个类将其成员变量和成员函数对同一应用程序内的子类以外的其他的类对象和函数进行隐藏。

### 个人理解
public 是大家都可以访问的，用来访问修改 private 的成员变量和成员函数。protected 是基类和子类才能访问。internal 是在同一程序集中可访问。


## C# 类定义

```csharp
<access specifier> class  class_name 
{
    // member variables
    <access specifier> <data type> variable1;
    <access specifier> <data type> variable2;
    ...
    <access specifier> <data type> variableN;
    // member methods
    <access specifier> <return type> method1(parameter_list) 
    {
        // method body 
    }
    <access specifier> <return type> method2(parameter_list) 
    {
        // method body 
    }
    ...
    <access specifier> <return type> methodN(parameter_list) 
    {
        // method body 
    }
}
```

- 访问标识符 <access specifier> 指定了对类及其成员的访问规则。如果没有指定，则使用默认的访问标识符。类的默认访问标识符是 internal，成员的默认访问标识符是 private。

- 数据类型 <data type> 指定了变量的类型，返回类型 <return type> 指定了返回的方法返回的数据类型。

- 如果要访问类的成员，您要使用点（.）运算符。

- 点运算符链接了对象的名称和成员的名称。

## C# 中的构造函数

类的 构造函数 是类的一个特殊的成员函数，当创建类的新对象时执行。构造函数的名称与类的名称完全相同，它没有任何返回类型。

构造函数是很方便的，相当于初始化的功能。构造函数可以有多个，根据传参类型不同来区分。

```csharp
using System;
namespace LineApplication
{
   class Line
   {
      private double length;   // 线条的长度



      public Line(double len)  // 参数化构造函数
      {
         Console.WriteLine("对象已创建，length = {0}", len);
         length = len;
      }
  public Line()
      {
         Console.WriteLine("对象已创建");
      }



      public void setLength( double len )
      {
         length = len;
      }
      public double getLength()
      {
         return length;
      }

      static void Main(string[] args)
      {
         Line line = new Line(10.0);
         Console.WriteLine("线条的长度： {0}", line.getLength()); 
         // 设置线条长度
         line.setLength(6.0);
         Console.WriteLine("线条的长度： {0}", line.getLength()); 
         Console.ReadKey();
      }
   }
}
```

## C# 中的析构函数

类的 析构函数 是类的一个特殊的成员函数，当类的对象超出范围时执行。析构函数的名称是在类的名称前加上一个波浪形（~）作为前缀，它不返回值，也不带任何参数。析构函数用于在结束程序（比如关闭文件、释放内存等）之前释放资源。析构函数不能继承或重载。

```csharp
using System;
namespace LineApplication
{
  class Line
   {
      private double length;   // 线条的长度
      public Line()  // 构造函数
      {
         Console.WriteLine("对象已创建");
      }
      ~Line() //析构函数
      {
         Console.WriteLine("对象已删除");
      }

      public void setLength( double len )
      {
         length = len;
      }
      public double getLength()
      {
         return length;
      }

      static void Main(string[] args)
      {
         Line line = new Line();
         // 设置线条长度
         line.setLength(6.0);
         Console.WriteLine("线条的长度： {0}", line.getLength());           
      }
   }
}
```

## C# 类的静态成员
我们可以使用 static 关键字把类成员定义为静态的。当我们声明一个类成员为静态时，意味着无论有多少个类的对象被创建，只会有一个该静态成员的副本。
关键字 static 意味着类中只有一个该成员的实例。静态变量用于定义常量，因为它们的值可以通过直接调用类而不需要创建类的实例来获取。静态变量可在成员函数或类的定义外部进行初始化。您也可以在类的定义内部初始化静态变量。

您也可以把一个成员函数声明为 static。这样的函数只能访问静态变量。静态函数在对象被创建之前就已经存在。下面的实例演示了静态函数的用法：

大概是所有实例共享一个参数的意思。

## C# 继承

### 基类和派生类

写新程序的时候，要设计新的类，继承了已有的类。已有的类被称为的基类，新的类被称为派生类。

```csharp
<acess-specifier> class <base_class>
{
 ...
}
class <derived_class> : <base_class>
{
 ...
}
```

### 基类的初始化
派生类继承了基类的成员变量和成员方法。因此父类对象应在子类对象创建之前被创建。您可以在成员初始化列表中进行父类的初始化。

```csharp
<acess-specifier> class <base_class>
{
 ...
}
class <derived_class> : <base_class>
{
 public <derived> (double l, double w) : base (l, w) {}
}
```

### 多重继承

首先我们需要知道什么是多重继承。。。（不懂2333）

C# 不支持多重继承。但是，可以使用接口来实现多重继承。

## C# 多态性

### 函数重载

您可以在同一个范围内对相同的函数名有多个定义。函数的定义必须彼此不同，可以是参数列表中的参数类型不同，也可以是参数个数不同。不能重载只有返回类型不同的函数声明。

### 动态多态性

动态多态性是通过 抽象类 和 虚方法 实现的。我在刚刚看到这个东西的时候是看不懂的。

首先我们需要理解一下抽象类。

然后再了解一下虚方法。

我在写 C++ 实验的时候，大概了解到动态多态性是什么了。基类和派生类（或者说子类和父类）有完全同名的函数，我们在使用父类的时候，他会去使用父类里的那个成员函数，而使用子类的时候，会去调用子类的成员函数。我们用基类指针指向一个父类或者子类的时候，他会根据指向的内容是什么然后做出判断去调用哪一个。这听上去有点不可思议，有一点反“C 常识”。

CSharp 是没有指针的，所以替代品就是引用了。

#### 抽象类

C# 允许使用关键字 abstract 创建抽象类，用于提供接口的部分类的实现。当一个派生类继承自该抽象类时，实现即完成。抽象类包含抽象方法，抽象方法可被派生类实现。派生类具有更专业的功能。

下面是有关抽象类的一些规则：
- 不能创建一个抽象类的实例。

- 不能在一个抽象类外部声明一个抽象方法。

- 通过在类定义前面放置关键字 sealed，可以将类声明为密封类。当一个类被声明为 sealed 时，它不能被继承。抽象类不能被声明为 sealed。

#### 虚方法

当有一个定义在类中的函数需要在继承类中实现时，可以使用虚方法。虚方法是使用关键字 virtual 声明的。虚方法可以在不同的继承类中有不同的实现。对虚方法的调用是在运行时发生的。

## C# 接口

Interface 接口定义了所有类继承接口时应遵循的语法合同。接口定义了语法合同 "是什么" 部分，派生类定义了语法合同 "怎么做" 部分。

粗粗一想 interface 和 abstract class 两者好像没啥区别，也可以互相替换。

但是其实区别也有，C# 中不允许多重继承，但是可以实现多个 interface。可以算是向多重继承的一种妥协。