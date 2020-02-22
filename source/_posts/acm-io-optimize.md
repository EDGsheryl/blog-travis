title: ACM 输入输出优化技巧
date: 2017-05-18 02:02:49
desc: 
tags: [ACM] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/acm-optimize.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/acm-optimize.jpg
---

在 ACM 竞赛中，时间效率是至关重要的一个指标。如果一个程序在输入输出上消耗太多时间，肯定影响算法本身占用的时间。而输入输出优化其实是一个老生长谈的问题

<!-- more -->

## 题外话
在这里还是要说一句，比较喜欢 Leetcode 和 Topcoder 的输入输出形式：通过 class 来作为接口传递。我们就不用关心输入输出问题了。

## scanf和cin
scanf 是 C 语言的读入，但是常常会忘记 &

scanf 在格式化读入上有奇效。适用于一些骚读入。

```cpp
scanf("%d+%d",&a,&b);//类似的东西。
```

## printf和cout
printf 也是 C 语言的函数。

但是占位符这个东西呀，太麻烦了，尤其是 long long 的占位符。喵喵喵？

这时候就要说 cout 大法好

(update 2017-08-26:根据后来的经验，关同步的 cin 甚至可以比 scanf 快，但是 cout 速度就是提不上去，如果输出字符串，更加推荐 puts)

```cpp
ios::sync_with_stdio(false);
```

这句话，字面意思 iostream 的啥同步和标准io啥的关掉。

翻了翻别人的博客

	cin  cout之所以效率低
	是因为先把要输出的东西存入缓冲区，再输出
	导致效率降低
	而这段语句可以来打消iostream的输入 输出缓存
	可以节省许多时间，使效率与scanf与printf相差无几
	还有应注意的是scanf与printf使用的头文件应是stdio.h而不是 iostream。

```cpp
cin.tie(0)
```

	在默认的情况下cin绑定的是cout
	每次执行 << 操作符的时候都要调用flush，这样会增加IO负担。
	可以通过tie(0)（0表示NULL）来解除cin与cout的绑定，进一步加快执行效率。

## 测试比较

在 Codeforces 上，今天做了对比

同一题目：

- 使用scanf,printf   平均用时342ms  内存19700 KB
- 使用优化的cincout   平均用时358ms  内存19800 KB
- 使用不优化cincout   平均用时1435ms 内存19800 KB

由于 cf 的超多组测试，我们认为他比较平均吧。

可以看出 cin cout 和 printf scanf 其实可以相差比较小的。

## 更加厉害的方法

可以逐字符读入处理。甚至可以一下子全读进来瞎搞。

    可以但没有必要。
