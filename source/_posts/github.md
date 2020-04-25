title: Git、GitHub 入门笔记
date: 2020-04-25 13:46:00
desc: 
tags: [git, github] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/github.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/github.jpg
---

4 月 7 日，全球最主流的版本控制系统——Git 迎来 15 周年纪念日，项目主要维护者 Junio C Hamano（滨野 纯）先生发邮件庆祝了这一日子。

<!-- more -->

## 版本控制

软件的迭代是软件工程当中很自然、很重要的方法论。

从一个简单版本，到逐渐演化成一个复杂系统，如果我们想让项目健康地运行下去需要较好的质量把关，对于每一次堆砌代码都做审查。

什么是版本控制？

> 版本控制（Revision control）是维护工程蓝图的标准作法，能追踪工程蓝图从诞生一直到定案的过程。此外，版本控制也是一种软件工程技巧，借此能在软件开发的过程中，确保由不同人所编辑的同一代码文件案都得到同步。[拓展阅读](https://en.wikipedia.org/wiki/Version_control "拓展阅读")

按照常理来说，按下 `Ctrl + S` 也就是一种简单的版本控制方法。

例如你写完了一个模块、一个组件、一个功能，甚至一行代码、一个注释、一个空格，都可以进行版本控制。

版本控制不是目的，而是一种提高团队开发效率的手段，版本控制的核心述求是历史纪录查询和实现协同开发。

## 版本控制工具

主流的版本控制工具主要分为两种，即集中式与分布式。

集中式版本控制工具类似网吧的管理系统，所有项目的历史文件与版本信息都存放在服务器上，而客户端就只能保存当前的状态信息。这种所有鸡蛋装在一个篮子里的模式缺点非常明显，一旦服务器损坏，项目所有的历史数据就会丢失，因此需要大规模的安全备份。比较有代表性的集中式版本控制工具有 SVN、VSS、CVS 等。

分布式版本控制工具最大的特性就是任意客户端之间可以互联，当然也包括服务器。这样一来，开发者的客户端本地也存有项目完整的历史记录，当有一个客户端损坏时，可以从另一个没有被损坏的客户端中提取历史数据，恢复之前的状态。在协同开发时，各个客户端之间可以很好地同步开发进度，避免出现重复提交等问题。

毫无疑问，分布式版本控制工具拥有更为先进的理念，其诞生的过程也是得益于网络通信技术的普及与开源社区的蓬勃发展。

## 故事的开始

我们的故事始于 1991 年，大名鼎鼎的开源项目 Linux 问世，作者 Linus Torvalds 一跃成为 IT 界的大明星，被人们称为天才。

由于当时 Linux 社区仍采用传统的集中式版本管理，开发者提交的 patch 都汇集到 Linus 这里，让他肩上的担子很重。

在项目早期，Linus 以最原始的人力来完成 Linux 版本管理工作，包括逐条细看每个 patch、手动合并开发者提交的代码、更新版本历史信息等。

然而随着社区的逐渐壮大，Linux 的系统变得越来越庞大，代码越来越繁杂，继续依靠手动合并代码显然已经不太现实。

1999 年，一家名为 BitMover 的公司发布了一款收费的分布式版本控制软件 BitKeeper ，BitMover 的 CEO Larry 给 Linux 社区特别提供了一个可以免费使用的版本，期望 BitKeeper 能帮助 Linus 免于陷入不断加重的 Linux 内核管理工作中，但条件是不能破解这款产品。

BitMover 的初衷也很简单，借助 Linux 的名声向大家推介自己家的产品。

Linus 在使用 BitKeeper 之后不久就爱上了它，直言其是“ Best tool for the job ”。

BitKeeper 让每个开发者都拥有自己的主副本（ master copy ），完整的副本意味着可以在本地做所有事，而不是所有的 patch 只能提交到服务器（Linus）这里。

于是，Linus 可以把一些 patch 的审查工作交给 Liunx 子系统的维护者们，对于比较值得信任的维护者甚至不需要他自己再审查一遍，而他只需要对一些自己不太信任的维护者 “重点关照” 即可。2002 年，Linux 内核主线代码就全面开始使用 BitKeeper。

尽管 BitKeeper 的出现赋予了 Linux 社区更好的协同开发能力，让 Linux 内核的开发效率成倍提高，但其闭源的特性仍然让 Linus 在开源界遭到了一些非议。开源泰斗 RMS 就严厉批评 Linus 不该使用一款非自由的软件来管理世界上最大的开源项目。这些负面的声音也为之后 Linux 与 BitKeeper 的分道扬镳埋下了伏笔。

## 分道扬镳

2005 年，Linus 本人所属公司 OSDL 的老板 Andrew Morton 资助的一个项目组开始对 BitKeeper 协议进行反向编译，试图破解 BitKeeper 以创造出一个类似的开源工具。BitMover 公司很快发现了这一动作，Larry 表示这破坏了免费版 BitKeeper 的许可协议，尽管这件事或许与 Linus 本人无关，但确实严重影响了公司的利益，他们最终决定逐步停止对免费版 BitKeeper 的支持，但会给 Linux 进行工具迭代的时间。

BitMover 的做法在当时来看确实也无可厚非，他们正当地维护了自己的合法权利，挽回了因产品被破解可能带来的经济损失。

## Git

同生活中的许多伟大事物一样，Git 诞生于一个极富纷争大举创新的年代。

Linux 内核开源项目有着为数众多的参与者。 绝大多数的 Linux 内核维护工作都花在了提交补丁和保存归档的繁琐事务上（1991－2002年间）。 到 2002 年，整个项目组开始启用一个专有的分布式版本控制系统 BitKeeper 来管理和维护代码。

到了 2005 年，开发 BitKeeper 的商业公司同 Linux 内核开源社区的合作关系结束，他们收回了 Linux 内核社区免费使用 BitKeeper 的权力。 这就迫使 Linux 开源社区（特别是 Linux 的缔造者 Linus Torvalds）基于使用 BitKeeper 时的经验教训，开发出自己的版本系统。 他们对新的系统制订了若干目标：

- 速度
- 简单的设计
- 对非线性开发模式的强力支持（允许成千上万个并行开发的分支）
- 完全分布式
- 有能力高效管理类似 Linux 内核一样的超大规模项目（速度和数据量）

自诞生于 2005 年以来，Git 日臻成熟完善，在高度易用的同时，仍然保留着初期设定的目标。 它的速度飞快，极其适合管理大项目，有着令人难以置信的非线性分支管理系统。

2008 年，基于 Git 实现的代码托管平台 GitHub 面世，从此 Git 更是享誉全球。有意思的是，GitHub 当初并不是由 Git 社区的人做的，而是出自 Ruby 社区的开发者之手，两个社区在最初的关系还有些不太和睦，原因是 Git 社区的人对于 GitHub 那群人拿 Git 去做商业化感觉很不爽……当然，这些都是老开发者口中的陈年往事了。毫无疑问，GitHub 对于 Git 的普及做出了巨大的贡献。Hamano 也表示：“ 有 GitHub 替我们做文档以及用户支持，何乐而不为呢。”

和 Git 的飞速发展形成鲜明对比的是，与 Linux 分道扬镳后的 BitKeeper 每况愈下，尽管后者是世界上首个商用级的分布式版本控制工具，但在 Git 诞生之后，BitKeeper 的市场占有率断崖式下滑，几乎沦落到无人问津的地步。Git 与 BitKeeper 的不同境遇可以说是 21世纪初软件行业的缩影，传统的软件商业模式在开源浪潮的席卷下迎来了前所未有的挑战。

## Git 配置指南

### 配置 SSH Key

#### 创建 SSH Key。

在创建 ssh-key 的时候，请注意在 `$HOME/.ssh` 下是否已经存在，如果已经存在则没有必要创建 ssh-key（请注意检查以防止造成不必要的损失）

```bash
$ ssh-keygen -t rsa -C "youremail@example.com"
```

你需要按照提示填写，或是使用默认值，一路回车。

如果一切顺利的话，可以在用户主目录里找到 `.ssh` 目录，里面有 `id_rsa` 和 `id_rsa.pub` 两个文件。

id_rsa 是私钥，不能泄露出去；id_rsa.pub 是公钥，用于服务器验证你的身份。

#### GitHub 客户顿配置

在网页端打开 `Account settings`，选择 `SSH Keys` 

然后点击 `Add SSH Key`，填上任意 Title，在 Key 文本框里粘贴 id_rsa.pub 文件的内容

这样，Github 的服务器就能够验证你的身份，你就能拉取你帐号对应的私有 Repo 了。

### 本地安装 Git 客户端

#### 安装 Git

```bash
$ sudo apt-get install git
```

#### 配置本地git

其实我一直没有理解这部分的配置的用途。

```bash
$ git config --global user.email "email@youremail.com"
$ git config --global user.name "yourname"
```

#### 提交 Commit 到 branch

```bash
$ git add -A
$ git commit -m "commit message"
$ git push origin master
```

## Git 进阶推荐

在网络上学习 Git 的参考资料有很多，依靠实践是学习进步的较快方法

[https://learngitbranching.js.org/](https://learngitbranching.js.org/)

## 参考资料
- [Git 15 周年：当年的分道扬镳，成就了今天的开源传奇](https://my.oschina.net/editorial-story/blog/3288572)
- [Git 简史](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-Git-%E7%AE%80%E5%8F%B2)