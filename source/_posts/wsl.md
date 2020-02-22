title: WSL 安装指南
date: 2018-04-22 19:13:54
desc: 
tags: [windows] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/wsl/wsl.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/wsl/wsl.jpg
---

在学习编程的时候，我们可能会学到如何使用 Linux，那简便快捷地建立这样一个环境是挺有必要的。除了用虚拟机安装 Linux 之外，我们可以用 WSL 来解决这样一个问题。

<!-- more -->

## 什么是WSL

Windows Subsystem for Linux（简称 WSL）是一个为在 Windows 10 上能够原生运行 Linux 二进制可执行文件（ELF 格式）的兼容层。它是由微软与 Canonical 公司合作开发，目标是使纯正的 Ubuntu 14.04 "Trusty Tahr" 映像能下载和解压到用户的本地计算机，并且映像内的工具和实用工具能在此子系统上原生运行。

当然现在的 WSL 支持了更多发行版，可以在商店里看到。

## 如何安装

### 勾上系统选项

控制面板 -> 程序和功能 -> 启用或关闭 Windows 功能 -> 勾选 适用于 Linux 的 Windows 子系统

Control Panel -> Programs -> Programs and Features -> Turn Windows features on or off -> windows Subsystem for Linux

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/wsl/813233-20171024162129051-1763340853.png)

勾选上之后，系统会查找对应组件，然后重启电脑。

### 在商店中安装

我们在商店中搜索 `WSL`

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/wsl/QQ%E6%88%AA%E5%9B%BE20180422154459.png)

（什么？你问我怎么打开商店？在任务栏“开始”的右边有个搜索，可以输入 store 或者商店打开）

点击 get the apps 就会出现

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/wsl/QQ%E6%88%AA%E5%9B%BE20180422154046.png)

我们可以尝试一下 Ubuntu 。

### 初次运行wsl

按下 win + R，运行 cmd 。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/wsl/QQ%E6%88%AA%E5%9B%BE20180422154619.png)

在 cmd 中输入命令 ```bash```

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/wsl/QQ%E6%88%AA%E5%9B%BE20180422154808.png)

或者在开始菜单栏里面找到 Ubuntu 也是可以的。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/wsl/QQ%E6%88%AA%E5%9B%BE20180422155424.png)

然后根据安装向导就能轻易完成安装辣。


## 其他的配置

### WSL中访问本地文件

在 /mnt 目录下有 c、d、e 等文件夹，分别表示本地的 C 盘、D 盘、E 盘，直接 cd 到相应路径下即可。

### 本地访问WSL的根目录

微软强烈不建议在外部对 WSL 文件系统进行更改，所以未公开 WSL 所在的根目录。（但是还是可以找到的。）

### 字体设置

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/wsl/QQ%E6%88%AA%E5%9B%BE20180422155824.png)

在窗体上右键，选择 Properties 选项，就可以更改字体和字体大小

### 常用工具

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/wsl/QQ%E6%88%AA%E5%9B%BE20180422160123.png)

可以看到自带了一些工具 ```git```、```ssh```，当然如果没有对应的工具的话，我们还可以尝试用包管理器，使用 ```apt``` 来安装想要的工具。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/wsl/QQ%E6%88%AA%E5%9B%BE20180422160407.png)

### 安装图形界面

安装图形界面的方法略麻烦，想要详细了解的可以点这里 [https://www.jianshu.com/p/aca81f8c7f08](https://www.jianshu.com/p/aca81f8c7f08)

## 其他的发行版

当然，我们还可以安装一些其他发行版的 Linux，当然这可能需要我们自己摸索，或者使用搜索引擎来帮助我们

[ArchLinux的WSL安装](https://www.cnblogs.com/wurui1994/p/7839777.html "ArchLinux的WSL安装")

## 后记

为了写这篇，我在我的 win 10 上装了个 win 10 虚拟机，然后再装了 WSL。。。。。。
