title: JetBrains Quest Challenge 1
date: 2020-03-13 12:00:00
desc: 
tags: [JetBrains, CTF] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/quest-title-2.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/quest-title-2.jpg
---

根据上一轮的 Quest 的最后邮件提示，我们可以知道第二轮举行时间为 2020-03-11 19:00:00

<!-- more -->

第二轮的题目也是一则推文

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/twitter-2.png)

# Reverse the string

我们可以看出这可能是一个反转的字符串

```python
print(".spleh A+lrtC/dmC .thgis fo tuo si ti semitemos ,etihw si txet nehw sa drah kooL .tseretni wohs dluohs uoy ecalp a si ,dessecorp si xat hctuD erehw esac ehT .sedih tseuq fo txen eht erehw si ,deificeps era segaugnal cificeps-niamod tcudorp ehT"[::-1])
```

可以得到

```Text
The product domain-specific languages are specified, is where the next of quest hides. The case where Dutch tax is processed, is a place you should show interest. Look hard as when text is white, sometimes it is out of sight. Cmd/Ctrl+A helps.
```

# Hidden Words

看起来是进入 [https://www.jetbrains.com/mps/](https://www.jetbrains.com/mps/) 这个页面了

提到了 Dutch Tax，我们到相关公司机构的最佳实践页面寻找线索，果然在 PDF 界面发现了隐藏的文字

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/hidden-words.png)

复制出这段话

```text
This is our 20th year as a company,
we have shared numbers in our JetBrains
Annual report, sharing the section with
18,650 numbers will progress your quest.
```

实际上这个页面有点难找，我是根据搜索结果，然后推断出今年的 URL [](https://www.jetbrains.com/company/annualreport/2019/)

# Sharing the section

根据上面数字提示 18,650 我在页面搜索了 18K、18650 等等，都没找到结果，最后发现有个 18000，其实图中数字加起来是 18650

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/sharing.png)

点击上方的 sharing 按钮就可以得到下一个提示了

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/sharing-2.png)

```text
I have found the JetBrains Quest! 
Sometimes you just need to look closely at the Haskell language, Hello,World! 
in the hackathon lego brainstorms project https://blog.jetbrains.com/blog/2019/11/22/jetbrains-7th-annual-hackathon/ 

#JetBrainsQuest https://www.jetbrains.com/company/annualreport/2019/ 来自 @JetBrains
```

# Hello, World with Haskell

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/comic.png)

仔细看上方其实是有一段文字的，火星英文！

```text
d1D j00 kN0w J378r41n2 12 4lW4Y2 H1R1N9? ch3CK 0u7 73h K4r33r2 P493 4nD 533 1f 7H3r3 12 4 J08 F0r J00 0R 4 KW357 cH4LL3n93 70 90 fUr7h3r @ l3457.
```

```text
Did you know Jetbrains is always hiring? Check out the careers page and see if there is a job for you or for newest challenge to go further at least.
```

# Find the job

找到 Hiring 的界面，然后去 Jobs 的页面寻找，发现有一个 `Fearless Quester` 的职位

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/job.png)

里面的有用信息应该如下：

```text
To progress with your quest what you’ll need:
- To check out what we have for game developers.
- Be geeky enough to remember how you used to cheat at Konami games.
- Try cheating on the page.
```

# Konami Cheating Code

这一步其实挺难的，你得知道有这么一个地方，然后输入秘籍，经典的 上上下下左右左右 BABA

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/game_page.png)

然后通关小游戏就能获得奖励辣

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/cong-letter2.png)

