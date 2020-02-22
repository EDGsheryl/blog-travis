title: 爬虫练习——四六级成绩抓取
date: 2017-08-26 02:04:08
desc: 
tags: [Python] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/cet4.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/cet4.jpg
---

辅导员突然给我打了个 QQ 电话，吓得我赶紧接起电话。我以为是要约谈我。突然问我会不会爬虫，嘛。当然是不会辣。QAQ。

<!-- more -->

## 环境准备

- 临时下载从未用过的 JetBrains PyCharm 2017.2.2 x64
- 很早安装但是不经常用的 Python 3.6
- pip3 和库：requests BeautifulSoup4 xlwt
- 名单

## 爬虫部分

### 模拟抓取

首先，我们肯定是要模拟自己正常查询的这一个过程，抓一个包，发现很明显的特征 /query?zkzh=&xm=。事实上，我们通常还会变成 /query?zkzh=&xm=&yzm=。但是我们有特殊的绕过技巧 诶嘿。

然后使用 requests 和 beautifulsoup 可以轻松的分离出很多东西，我们发现我们要的东西都在 td 标签里，很快就分离了

### 字符串处理

但是输出来看，有个很恼火的东西，就是他长成这个样子

	张三

                    电子科技大学

                    英语四级

                    51002017******

                    

                        

                        107

                        

                    

                        

                        177

                        

                    

                        

                        108

                        

                    --

                    --

哇 这可让我炸了毛了。我于是求助叶姐姐，问他正则匹配非空怎么弄。然后问来，发现不会用。于是跑去网上找资料，用 re 库，然后发现了更加痛苦的事情，我匹配串写不来=-=。。

想了好多办法，甚至想要用 C++ 来处理，感觉自己有点蠢，就先存了，然后在读回来，然后 split 掉，然后就可以拼成没有的串辣

大概像酱紫：
	李四 电子科技大学 英语六级 510020171****** 86 145 96

嗯嗯 然后全部抓一遍就 ok 辣

## Excel处理

发现 excel 拖出来可以 txt 很好看，粘贴回去发现就是一坨。。。。

于是就写了第二个程序来处理。

处理过程非常简单，就对对应的格子写一下，然后人工排版一下美滋滋。

## 后记

听说爬虫是有框架的，来（lan）日（de）再（qu）说（xue）

爬虫应该是基本技能之一，啊喂=-=

## 部分展示

[https://github.com/EDGsheryl/CET-4-6-score-catch](https://github.com/EDGsheryl/CET-4-6-score-catch)

