title: 初探正则表达式
date: 2018-04-17 23:01:56
desc: 
tags: [lang] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/regex/regex.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/regex/regex.jpg
---

后来的后来，在 Tusimple，天天被抓去写正则。。。

<!-- more -->

## 什么是正则表达式

引用百科的话：

> 正则表达式（英语：Regular Expression，在代码中常简写为regex、regexp或RE），又称正规表示式、正规表示法、正规表达式、规则表达式、常规表示法，是计算机科学的一个概念。正则表达式使用单个字符串来描述、匹配一系列匹配某个句法规则的字符串。在很多文本编辑器里，正则表达式通常被用来检索、替换那些匹配某个模式的文本。
> 
许多程序设计语言都支持利用正则表达式进行字符串操作。例如，在Perl中就内建了一个功能强大的正则表达式引擎。正则表达式这个概念最初是由Unix中的工具软件（例如sed和grep）普及开的。正则表达式通常缩写成regex，单数有regexp、regex，复数有regexps、regexes、regexen。

[https://zh.wikipedia.org/wiki/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F](https://zh.wikipedia.org/wiki/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F "百科链接")

## 什么时候使用正则表达式

在有以下需求的时候使用

- 从文本中找到我们想要的内容。
- 检测一段文本是否符合设定好的规则

## 为什么使用正则表达式

正则表达式的本质是一个工具，好的工具能简化我们的思维复杂度和编程复杂度。

使用正则表达式完全是为了简化我们的代码，而不是为了炫技 :D

## 如何使用正则表达式

### 例子1

例如我们想要修改某个配置文件，配置参数为“啥 post 啥 size”的

我们用 Vim 打开配置文件，输入

	/\w*size\w*

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/regex/1.png)

然后回车，按 N 查找下一个，就能很快找到那一行了，原来我们要找的是 post_max_size。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/regex/2.png)

### 例子2

检测上传的文件的文件名

我们想要 jpg，png，gif

	img0912.jpg
	updated_img0912.png
	favicon.gif

所以以下文件名应该被过滤

	.bash_profile
	workspace.doc
	documentation.html
	img0912.jpg.tmp
	access.lock

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/regex/3.png)

### 例子3

正则表达式被很多编程语言支持，在 C++ 中也不例外，看一个改编自《c++ primer》的示例

	```c++
	#include <bits/stdc++.h>
	
	int main()
	{
	    std::string s("[[:alpha:]]*[^c]ei[[:alpha:]]*");
	    std::regex r(s);
	    std::smatch m;
	    std::string d("receipt freind theif receive");
	
	    if (std::regex_search(d,m,r))
	        std::cout<<m.str()<<std::endl;
	}
	
	//output: freind
	
	```

## 如何学习使用正则表达式

学习正则表达式的最好方法是实践，所以这里推荐一些网站和工具。

[https://regex101.com/](https://regex101.com/) in JavaScript, Python, PCRE 16-bit, generates explanation of pattern

[https://www.debuggex.com/](https://www.debuggex.com/) 正则验证测试，清晰明了

[https://mengzhuo.org/regex/](https://mengzhuo.org/regex/) 中文版正则验证测试

[http://refiddle.com/](http://refiddle.com/) 测试工具

[http://myregexp.com/](http://myregexp.com/) 也是测试工具，都可以试一试

[http://regex.alf.nu](http://regex.alf.nu) 闯关模式练习正则表达式，完成一个个正则匹配的测验

[http://regexone.com/](http://regexone.com/) 通过实际练习掌握正则表达式

[https://regexcrossword.com/](https://regexcrossword.com/) 正则挑战，有不同难度，很丰富

[http://callumacrae.github.io/regex-tuesday/](http://callumacrae.github.io/regex-tuesday/) 正则挑战，完成正则匹配要求

[https://msdn.microsoft.com/zh-cn/library/az24scfc.aspx](https://msdn.microsoft.com/zh-cn/library/az24scfc.aspx) MSDN 微软出品

当然学习资料不只有这些，需要善用搜索引擎来发现。

## 题外话

这篇被我拿去当了公众号推送，感觉自己都不会说话了，我惊奇的发现原来微信公众号是富文本格式的。

上面的闯关测验还是不错的，感觉自己学到了不少=w=