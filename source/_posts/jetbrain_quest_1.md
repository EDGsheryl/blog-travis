title: JetBrains Quest Challenge 1
date: 2020-03-10 12:00:00
desc: 
tags: [JetBrains, CTF] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/quest-title-1.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/quest-title-1.jpg
---

JetBrains 给大家发福利了，免费三个月 All package 的 Coupon Code，只需要参加官方举办的 Quest Challenge，这是一个程序猿解密游戏

<!-- more -->

JetBrains 20 周年纪念，在 Twitter 上发布了这样一则推文

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/twitter.png)

# Hex to char

我们可以看出这可能是一段十六进制的数字，那么他可能给的是一个字符串。

```python
quest = "48 61 76 65 20 79 6f 75 20 73 65 65 6e 20 74 68 65 20 73 6f 75 72 63 65 20 63 6f 64 65 20 6f 66 20 74 68 65 20 4a 65 74 42 72 61 69 6e 73 20 77 65 62 73 69 74 65 3f"
ans = ""

for ch in quest.split(' '):
    ans += chr(int(ch, 16))

print(ans)
```

可以得到

```Text
Have you seen the source code of the JetBrains website?
```



# Source Code

在官网页面，空白处右键，查看源码，你可以看到一段 HTML 注释

```html
        <!--
      O
{o)xxx|===============-
      O

Welcome to the JetBrains Quest.

What awaits ahead is a series of challenges. Each one will require a little initiative, a little thinking, and a whole lot of JetBrains to get to the end. Cheating is allowed and in some places encouraged. You have until the 15th of March at 12:00 CET to finish all the quests.
Getting to the end of each quest will earn you a reward.
Let the quest commence!

JetBrains has a lot of products, but there is one that looks like a joke on our Products page, you should start there... (hint: use Chrome Incognito mode)
It’s dangerous to go alone take this key: Good luck! == Jrrg#oxfn$

                 O
-===============|xxx(o}
                 O
-->
```

欢迎来到JetBrains Quest。

未来将面临一系列挑战。 每个人都需要一点努力，一点思考和很多 JetBrains 才能达到终点。允许作弊，在某些地方鼓励作弊。您必须在 3 月 15 日欧洲中部时间 12:00 之前完成所有任务。
到达每个任务的结尾将为您带来奖励。
让任务开始！

JetBrains有很多产品，但是我们的“产品”页面上有一个看起来像个玩笑的产品，您应该从那里开始...（提示：使用 Chrome 隐身模式）

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/what-is-JK.png)

你这个 JK 是什么鬼啦！

# Count the prime

轻拿鼠标点击，打开一个对话框

```Text
You have discovered our JetBrains Quest! If you don’t know what this is, you should start from Twitter, Facebook or LinkedIn.


To continue to the next challenge you need to go to the following link… But there is a problem, the last 3 digits are missing:


https://jb.gg/###


To get these digits you need to know how many prime numbers there are between 500 and 5000


Good Luck!
```

您已发现我们的JetBrains Quest！ 如果您不知道这是什么，则应从Twitter，Facebook或LinkedIn开始。

要继续下一个挑战，您需要转到以下链接…但是存在问题，后三位数字丢失：

https://jb.gg/###

要获得这些数字，您需要知道 500 和 5000 之间有多少个质数

祝好运！

想像一下，如果是一个宅宅，怀着怎样的心情，点开了 JK，发现和想象中的不太一样 QwQ。。。

```
isPrime = lambda x: all(x % i != 0 for i in range(int(x ** 0.5) + 1)[2:])
ans = 0

for num in range(500, 5000):
    if isPrime(num):
        ans += 1

print(ans)
```

然后打开对应的网址

# Trace the issue

得到了一张新的图片，应该和台球无关吧。。。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/mps.png)

图上有 YT，youtrack 是一个项目管理工具，这一步我认为是最难的地方，你得知道这个工具是干嘛的，然后发现他其实有公开的 issue，找到对应的 issue 就能知道下一步提示了

```text
“The key is to think back to the beginning.” – The JetBrains Quest team.

Qlfh$#Li#|rx#duh#uhdglqj#wklv#|rx#pxvw#kdyh#zrunhg#rxw#krz#wr#ghfu|sw#lw1#Wklv#lv#rxu#lvvxh#wudfnhu#ghvljqhg#iru#djloh#whdpv1#Lw#lv#iuhh#iru#xs#wr#6#xvhuv#lq#Forxg#dqg#iru#43#xvhuv#lq#Vwdqgdorqh/#vr#li#|rx#zdqw#wr#jlyh#lw#d#jr#lq#|rxu#whdp#wkhq#zh#wrwdoo|#uhfrpphqg#lw1#|rx#kdyh#ilqlvkhg#wkh#iluvw#Txhvw/#qrz#lw“v#wlph#wr#uhghhp#|rxu#iluvw#sul}h1#Wkh#frgh#iru#wkh#iluvw#txhvw#lv#‟EhfdxvhFrgh†1#Jr#wr#wkh#Txhvw#Sdjh#dqg#xvh#wkh#frgh#wr#fodlp#|rxu#sul}h1#kwwsv=22zzz1mhweudlqv1frp2surpr2txhvw2
```

我以为只是倒过来，我想了半天，以为是弗吉尼亚密码，解密网站告诉我 key 是 ddd，那不就是凯撒吗。。。

``` Python
quest = "Qlfh$#Li#|rx#duh#uhdglqj#wklv#|rx#pxvw#kdyh#zrunhg#rxw#krz#wr#ghfu|sw#lw1#Wklv#lv#rxu#lvvxh#wudfnhu#ghvljqhg#iru#djloh#whdpv1#Lw#lv#iuhh#iru#xs#wr#6#xvhuv#lq#Forxg#dqg#iru#43#xvhuv#lq#Vwdqgdorqh/#vr#li#|rx#zdqw#wr#jlyh#lw#d#jr#lq#|rxu#whdp#wkhq#zh#wrwdoo|#uhfrpphqg#lw1#|rx#kdyh#ilqlvkhg#wkh#iluvw#Txhvw/#qrz#lw“v#wlph#wr#uhghhp#|rxu#iluvw#sul}h1#Wkh#frgh#iru#wkh#iluvw#txhvw#lv#‟EhfdxvhFrgh†1#Jr#wr#wkh#Txhvw#Sdjh#dqg#xvh#wkh#frgh#wr#fodlp#|rxu#sul}h1#kwwsv=22zzz1mhweudlqv1frp2surpr2txhvw2"
ans = ""

for i in range(len(quest)):
    ans += chr(ord(quest[i]) - 3)

print(ans)
```

接下来的你懂了吧！

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/cong-letter1.png)

除了本次的奖励之外，其实邮件里还有一些细节

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jetbrains-quest/next-clues.png)

比如下面的时间，他是一个 UNIX 时间戳。

还有那一行 `Y0U H4V3` 的信息都比较嗨客
