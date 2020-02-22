title: 七周七语言——Ruby 篇
date: 2018-02-09 00:53:36
desc: 
tags: [lang] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/ruby.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/ruby.jpg
---

松本行弘（Yukihiro Matsumoto）大约在1993年发明了Ruby，

<!-- more -->

## Day 1

### Ruby简史

> 松本行弘（Yukihiro Matsumoto）大约在1993年发明了Ruby，大家多称他为Matz。从语言的角度看，Ruby出身于所谓的脚本语言家族，是一种解释型、面向对象、动态类型的语言。解释型， 意味着Ruby代码由解释器而非编译器执行。动态类型，意味着类型在运行时而非编译时绑定。从 这两方面看，Ruby采取的策略是在灵活性和运行时安全之间寻找平衡点，我们稍后还会深入讨论 这一点。面向对象，意味着Ruby支持封装（把数据和行为一起打包）、类继承（用一棵类树来组 织对象类型）、多态（对象可表现为多种形式）等特性。Ruby多年来一直默默蛰伏，只为等待一 个恰当的出现时机。终于，随着Rails框架崭露头角，Ruby也在2006年前后一鸣惊人。在企业开 发的丛林中跋涉了十年之后，Ruby指引人们重新找回了编程乐趣。尽管从执行速度上说，Ruby 谈不上有多高效，但它却能让程序员的编程效率大幅提高。——《7周7语言:理解多种编程范型》 [美]Bruce A. Tate

### 环境搭建
[http://www.ruby-lang.org ][1] 是 Ruby 的官方网站。

（有意思的是，松本行弘前辈似乎认为他开创了一个有趣的先例：/*lang.*/g，以至于后来的语言官网格式会参考他，例如 golang.org）

根据官网的提示应该很快能搭建起环境，目前最新版似乎是 v3.5.0，而我的机子上是 v3.3.3，之前在服务器上使用 Jekyll 工具的时候似乎使用了更早的 Ruby 版本，所以可以看需求安装对应版本。

安装好可以使用 ```ruby -v``` 命令查看安装好的 Ruby 版本，或者输入 irb 启动 Ruby 解释器，验证 Ruby 是否正确安装。

### 第一天内容总结

Ruby 的特点：

- Ruby 是几乎是解释执行的，但是也有开发者正在开发虚拟机，想把 Ruby 代码编译成字节码再执行。
- Ruby 的变量是不需要事先声明的。Ruby 的类型是鸭子类型。
- Ruby 是一门纯面向对象的语言。
- 大量的语法糖（Syntactic Sugar）

好吧 我现在觉得《7周7语言》这本书讲的太笼统了，感觉没看到啥第一天的讲述内容就结束了 QwQ。。。

Ruby 的设计初衷，似乎目标是作为脚本语言，所以解释执行这一设定非常自然（与 Python，Perl，Bash 相比较）。

Ruby 的类型采用鸭子类型设计：他只要可以像鸭子一样走路，像鸭子一样叫，那他就是鸭子。

面向对象部分没有深入了解，但是所有类型都是对象。

**大量的语法糖**。Ruby的语法确实花里胡哨！这根本原因是Ruby的设计者松本行弘前辈认为人适应机器是本末倒置的行为，所以他从机器适应人的角度来设计语法规则，同时他认为执行效率问题不是最大的问题，所以语法糖而且是大量的语法糖应运而生。

```Ruby
> print "Hello, Ruby"
Hello, Ruby=> nil
> puts "Hello, Ruby"
Hello, Ruby
=> nil
> p "Hello, Ruby"
"Hello, Ruby"
=> "Hello, Ruby"
```

从上述例子可以看出不同的打印字符串的方法，结果不尽相同，而且我们可以注意到 Ruby 的解释执行是有返回类型的。

程序分支控制上，除了 if，还有 unless（if 的否定，虽然从翻译上很容易弄混）。不仅如此，还可以 if 后置，例如

```Ruby
> x = 4
=> 4
> puts "this statement is True" if x == 4
this statement is True
=> nil
> puts "this statement is False" unless x == 5
this statement is False
=> nil
```

循环控制也如此。

```Ruby
> x = 1
=> 1
> x = x + 1 while x < 10
=> nil
> x
=> 10
```

似乎我也没写过多少 Ruby 程序，仅仅只能分享一些自认为有趣的东西。


### 自习部分

其实七周七语言这本书真的偷懒——让你自己去查其他资料！

找：

- ✔ Ruby API文档： [http://ruby-doc.org/][2]
- ✔ Programming Ruby ：The Pragmatic Programmer’s Guide [TFH08]的免费在线版本。[传送门][3]
- ✔ 替换字符串某一部分的方法。[搬运传送门][4]
- ✔ 有关Ruby正则表达式的资料。[搬运传送门][5]
- ✔ 有关Ruby区间（range）的资料。[搬运传送门][6]

做：

- ✔ 打印字符串"Hello, world."。
- ✖ 在字符串"Hello, Ruby."中，找出"Ruby."所在下标。
- ✖ 打印你的名字十遍。
- ✖ 打印字符串"This is sentence number 1."，其中的数字1会一直变化到10。
- ✖ 从文件运行Ruby程序。
- ✖ 加分题：如果你感觉意犹未尽，还可以写一个选随机数的程序。该程序让玩家猜随机数 是多少，并告诉玩家是猜大了还是猜小了。

Well, 其实编程提升最快的方法是多敲代码，但是上述任务似乎有些（太简单了）。。

（逃）

------

## Day 2

Day 2 的内容似乎也很杂，这本书不适合系统的学习一门语言，但是时候作为开拓读物之类的。。。

### 函数

与 Python 函数的定义相似

```Ruby
def tell_the_truth
    true
end
```

Ruby 设定函数结束前处理的最后一句话的返回值，作为函数的返回值。

### 数组

```Ruby
> animals = ['lion','tiger','bear']
=> ["lion", "tiger", "bear"]
> animals[0]
=> "lion"
> animals[1]
=> "tiger"
> animals[2]
=> "bear"
> animals[3]
=> nil
> animals[-1]
=> "bear"
> animals[-2]
=> "tiger"
> animals[-3]
=> "lion"
> animals[-4]
=> nil
> animals[9]  = 'cat'
=> "cat"
> animals
=> ["lion", "tiger", "bear", nil, nil, nil, nil, nil, nil, "cat"]
```

Ruby 的数组长得也与 Python 相似。。。下标从 0 开始，超出数组长度则返回 nil，有趣的事情是，Ruby 有倒数（从后往前数）这个设定，例子中倒数第一个是 bear，倒数第三个是 lion，而没有倒数第四个。

### 散列

```Ruby
>  {:array => [1,2,3],:string => "string!"}
=> {:array=>[1, 2, 3], :string=>"string!"}
> things[[1,2,3]]
=> nil
> things["qwer"]
=> nil
> things[:string]
=> "string!"
```

map

### 代码块

一段代码可以作为一个整体来传递！

```Ruby
> 3.times {p "Hello"}
"Hello"
"Hello"
"Hello"
=> 3

 class Fixnum        
    def my_times        
        i = self            
        while i>0           
            i = i - 1            
            yield               
        end                 
    end                 
 end                 

> 3.my_times{p "Hello"}
"Hello"
"Hello"
"Hello"
=> nil
```

原理大概就是酱紫 （最后函数应该 return self，与 Ruby 设计保持一致）

### 类

Ruby 的类感觉并不能一两句话就说完，详细了解：[传送门][7]

Ruby 似乎不能多重继承（例如棱形继承），Java 采用接口来解决这个问题，而 Ruby 采用 Module 来解决。我们对一个类可以进行一个系列的动作的时候，只要 include 对应的模块就行了，该行为称为 Mix in。

Ruby 太实用了！

### 自习

查

- ✖ 分别找到用代码块和不用代码块读取文件的方法，用代码块有什么好处？ 
- ✔ 如何把散列表转换成数组？数组能转换成散列表吗？ 
```
散列表是一个映射，如果只储存value，则可以Hash.each {|i,o| Array.push(o)}
数组当然可以转换成散列，对应的是数组下标映射到数组里的值。
```
- ✔ 你能循环遍历散列表吗？ 
```
    感觉从理论上来说可行
    def my_each(&block)
        while true
            self.each {|i,v| block.call}
        end
    end
    但是为啥代码跑不通。。。
    或者我们把每对单独提出来做一个新的散列表，用数组储存他们，然后对数组进行循环遍历。
```
- ✔ Ruby的数组能当作栈来用，它还能用作哪些常用的数据结构？
```
    队列
    大根堆小根堆（二叉树）
```

做

- ✖ 有一个数组，包含16个数字。仅用each方法打印数组中的内容，一次打印4个数字。然后， 用可枚举模块的each_slice方法重做一遍。
- ✔ 我们前面实现了一个有趣的树类Tree，但它不具有简洁的用户接口，来设置一棵新树， 为它写一个初始化方法，接受散列表和数组嵌套的结构。写好之后，你可以这样设置新 树：{'grandpa' => { 'dad' => {'child 1' => {}, 'child 2' => {} }, 'uncle' => {'child 3' => {}, 'child 4' => {} } } }。

```Ruby
class Tree 
	attr_accessor :name, :children

	def initialize(name,t=[]) 
		if (name.class == Hash)
			name.each {|n,v| setdata(n,v)}
		else
			@name = name
			@children = Array.new(0)
			t.each {|n,v| @children.push(Tree.new(n,v)) }
		end
	end

	def setdata(name,children=[])
		@name = name
		@children = Array.new(0)
		children.each {|n,v| @children.push(Tree.new(n,v)) }
	end

	def visitall(n)
		for i in (1..n) 
			print("\t")
		end
		p name
		children.each {|i| i.visitall(n+1)}
	end

end

mytree = Tree.new({'grandpa'=> { 'dad' => {'child 1' => {}, 'child 2' => {} }, 'uncle' => {'child 3' => {}, 'child 4' => {} } } })
mytree.visitall(0)

=begin
    迭代的方式生成
=end

```

- ✖ 写一个简单的grep程序，把文件中出现某词组的行全都打印出来。这需要使用简单的正则 表达式匹配，并从文件中读取各行。（这在Ruby中超乎想象地简单。）如果你愿意的话， 还可以加上行号。

------

## Day3

### Metaprogramming

#### 开放类

```Ruby
class NilClass
	def blank?
		true
	end
end

class String 
	def blank?
		self.size == 0
	end
end

["","blank",NIL].each do |element|
	puts element unless element.blank?
end
```

事实上我们在这里并不是新建了两个新的类，而是在原有的类的基础上加了些东西。如果你愿意，甚至可以把它玩坏。

#### method_missing

Ruby 在找不到某种方法的时候，例如你操作的对象不是你想像的那个类型，Ruby 会显示诊断信息，使得 Ruby 更加易于调试。而如果我们覆盖了 method_missing 方法的话，我们可以更改返回值或者行为。

借用书上的例子（改）：
```Ruby
class Roman
    def self.method_missing name, *args
        roman = name.to_s
        (roman.count("I") +
         roman.count("V") * 5 +
         roman.count("X") * 10 +
         roman.count("L") * 50 +
         roman.count("C") * 100 )
    end
end        
```

非常巧妙的一个演示，尽管有些不对（跟计数法的计算方法有偏差）。

## 语言总结

我认为书上的语言足够简介：

> Ruby 的纯面向对象可以让你用一致的方式来处理对象。鸭子类型根据对象可提供的方法，而
不是对象的继承层次，实现了更切合实际的多态设计。Ruby的模块和开放类，使程序员能把行为 紧密结合到语法上，这大大超越了类中定义的传统方法和实例变量。

而不足之处在于：

- 性能问题
    但是我们很高兴看到 Ruby 效率越来越高了，设计者本人也认为效率问题会因为计算机计算速度变快而从另一个角度解决效率问题。

- 并发问题
    事实上一直不理解书上这段话。

- 类型安全
    无法进行编译的时候的检查，事实上在做第二天自习的时候就遇到了这个问题：构造函数被直接覆盖，而不是重载，而之后需要传入两个参数但我只传入一个参数，没有任何错误提示。

总之，很欣赏 Ruby 的设计哲学。我相信会有越来越多的人了解 Ruby，接受 Ruby 并使用 Ruby。


## 参考资料
    http://www.ruby-lang.org
    http://ruby-doc.org/
    http://ruby-doc.com/docs/ProgrammingRuby/
    http://www.runoob.com/ruby/ruby-string.html
    http://www.runoob.com/ruby/ruby-regular-expressions.html
    http://www.runoob.com/ruby/ruby-range.html
    http://www.runoob.com/ruby/ruby-object-oriented.html