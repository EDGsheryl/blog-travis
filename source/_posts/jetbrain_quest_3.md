title: JetBrains Quest Challenge 3
date: 2020-03-14 17:43:00
desc: 
tags: [JetBrains, CTF] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/quest-title-3.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/quest-title-3.jpg
---

第三弹 Quest，这一次的难度比较高，最后的奖品是一个 20% OFF 的 Discounts Code，可能就没有之前那么香

<!-- more -->

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/annualreport-2019.png)

JetBrains 成立 20 周年了，如果不去了解 JetBrains 的历史，也不会知道 IDEA 是 2000 年推出的 IDE

IDE 将一些工具集成化、简化、可视化，从而达到降低学习成本、提高工作效率，感谢 JetBrains 的 Innovation，为 Coding 带来更多乐趣

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/JetBrains-Products.png)

第三轮的题目同样来自一则推文

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/twitter3.png)

# Base64

特征其实不是很明显，就 base64 一下吧

```Text
Have you seen the post on our Instagram account?
```

(是一个导流广告 x)

# Instagram

吃下这发安利，我们可以到对应页面看到这个 post

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/Instagram.png)

```text
Welcome to the final Quest! You should start on the Kotlin Playground: https://jb.gg/kotlin_quest
P.S. If you don’t know about the #JetBrainsQuest, it’s not too late to find out.
```

# Kotlin

实际上这个 n 需要多试几次，因为之前那个移位密码也有很多 #，实际上应该和之前一样是 `n=3`

```Kotlin
fun main() {
   val s = "Zh#kdyh#ehhq#zrunlqj#552:#rq#wkh#ylghr#iru#wkh#iluvw#hslvrgh#ri#wkh#SksVwrup#HDS1#Li#zh#jdyh#|rx#d#foxh/#lw#zrxog#eh#hdv|#dv#sl1"

   val n: Int = 3;
   for (c in s) {
       print(c - n)
   }
}
```

然后解出

```text
We have been working 22/7 on the video for the first episode of the PhpStorm EAP. If we gave you a clue, it would be easy as pi.
```

# Pi equals to 3.14....

指向了一个视频，我 0.25 倍速度也没看出个所以然，看了别人才知道是一个 URL 被改了，改了的 URL 是最终的线索

视频跳之 3:14 有蜜汁转场效果

<iframe width="560" height="315" src="https://www.youtube.com/embed/OtQuAr3n87c" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

[https://jb.gg/31415926](https://jb.gg/31415926)

# 猝不及防的快问快答

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/questions.png)

答完之后会得到下一步的线索

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/quiz-done.png)

# 藏头诗

```text
Not Everything Today Does All You Could Ask. Lessons Learned From Other Relevant Solutions, Possibly Even Another Kind Emerge. Risking Sometimes Being Liberal Or Generous Proves Ordinary Simple Tests Infinitely More Annoying. Get Examining Hidden Initial Designated Early Symbols. They Have Everything Needed, Except Xerox, To Completely Level Up Everything.
```

一段让人摸不着头脑的文字，看了网友表示这是 acronym

```text
.Net day call for speakers blog post image hides the next clue
```

# .NET DAY

通过搜索引擎找到这个页面

[https://blog.jetbrains.com/dotnet/2020/02/13/jetbrains-net-day-online-2020-call-speakers/](https://blog.jetbrains.com/dotnet/2020/02/13/jetbrains-net-day-online-2020-call-speakers/)

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/clues-in-pic.png)

线索很好找， `you_are_looking_for_build_201-6303`

# Tip today

这一步就比较硬核了，你需要下载安装，好大啊。。。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/eap.png)

然后算出答案想必不是什么难事吧！

# 神秘代码

46023125


