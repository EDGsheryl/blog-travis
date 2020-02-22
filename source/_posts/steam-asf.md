title: Steam 挂卡工具 ASF 的 Ubuntu 部署
date: 2017-12-25 02:08:13
desc: 
tags: [linux, sa] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/steam-asf.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/steam-asf.jpg
---

在室(jin)友(qian)的诱惑下，好想要 NEKOPARA 的背景啊 QAQ

<!-- more -->

就跑去弄了一个 ASF 这么一个神奇的云挂卡工具

因为最近社区被封了，然后你需要特殊的上网技巧。

## ASF入门

ASF 3.0 传送门：[https://github.com/JustArchi/ArchiSteamFarm/releases/](https://github.com/JustArchi/ArchiSteamFarm/releases/)

现在市面上的资料绝大多数是 2.0 版本的，但是好像也能用。

首先我们拿 Windows 来举例子。下载后解压，几个关键的文件是

	├── config
	│   ├── ASF.json
	│   ├── ASF.db
	│   ├── Bot1.json
	│   ├── Bot1.db
	│   ├── Bot1.bin
	│   ├── Bot2.json
	│   ├── Bot2.db
	│   ├── Bot2.bin
	│   └── ...
	├── ArchiSteamFarm.exe
	└── ConfigGenerator.html

其中 ConfigGenerator.html 是拿来生成 .json 的配置文件的，也可以用[https://justarchi.github.io/ArchiSteamFarm/#/bot](https://justarchi.github.io/ArchiSteamFarm/#/bot)

把生成的配置文件放在 config 文件下，然后双击 ArchiSteamFarm.exe 即可 <del>喊666</del> 运行挂卡程序了。是不是很简单！

## Ubuntu上部署

由于寝室晚上要熄灯。。。我们就想到了一种真·云挂卡的方案。

首先你要有一台能上 Steam 社区的服务器，然后在 Ubuntu 上安装 .NET Core 环境。

我的妈呀，我之前装了半天的 mono，要么告诉我不能运行，要么告诉我少库。其实网上那些是 2.0 的教程，但是 3.0 他换了！

安装 .NET Core 环境官方教程（记得选择 Linux）：[https://www.microsoft.com/net/learn/get-started/linuxubuntu](https://www.microsoft.com/net/learn/get-started/linuxubuntu)

按照步骤来，如果他说少 libicu55，那么你把 Ubuntu 17.04，Ubuntu 17.10 的步骤也做一遍估计就好了。

安装好以后，先跳过以下步骤，如果后面不能运行，尝试这一步

	dotnet new console -o myApp

**先跳过上面这步骤**

然后把下载下来的 ASF-linux 版本解压了，（不会的可以 Win 上解压丢回服务器）。

然后 chmod 赋权，然后 ./ArchiSteamFarm 即可正常运行。

## 最后

其实安装本身没有难度，就是你得找到你为啥错了 2333 像我就是因为搞不来依赖所以到处乱搞 最后冷静了一下 找了官方的环境安装教程就搞定了。

如果你愿意实现不需要手动输入令牌，那么你可以看这里：[https://github.com/JustArchi/ArchiSteamFarm/wiki/Escrow](https://github.com/JustArchi/ArchiSteamFarm/wiki/Escrow)


