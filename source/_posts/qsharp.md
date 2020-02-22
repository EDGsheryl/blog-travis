title: 配置 Q# 开发环境
date: 2018-06-30 15:23:49
desc: 
tags: [lang] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/qsharp/title.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/qsharp/title.jpg
---

Q# 是一门特定领域编程语言，用来表达量子算法。它最初作为量子开发套件的一部分由微软公开发布给公众。

<!-- more -->

> Q# (pronounced as Q sharp) is a domain-specific programming language used for expressing quantum algorithms. It was initially released to the public by Microsoft as part of the Quantum Development Kit.

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/qsharp/DQ1nXgxUIAEm2V7.jpg)

## 安装开发环境

这里只给出 Windows 下的安装方法

### 安装 Visual Studio

去官网下载 [Visual Studio download page](https://visualstudio.microsoft.com/downloads/) ，我们选择社区版，社区版是免费版本，而其他两个版本提供付费功能。

安装只需要安装 Visual Studio 的本体和 **.NET Core cross-platform development** 即可，不需要安装其他的开发组件。

### 安装 Quantum Development Kit

下载并安装 [Quantum Development Kit](https://marketplace.visualstudio.com/items?itemName=quantum.DevKit) 

### Clone repo

打开 Visual Studio，在上方菜单栏找到（团队 > 管理连接）(Team > Manage Connections)

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/qsharp/QQ%E5%9B%BE%E7%89%8720180630114022.png)

然后会在右侧弹出对话框，选择克隆，输入 `https://github.com/Microsoft/Quantum.git`，选择克隆的目录，克隆下来。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/qsharp/QQ%E6%88%AA%E5%9B%BE20180630114040.png)

克隆完成后，对话框变成了 Solution Explorer，双击打开 QsharpLibraries.sln, 此时就会开始安装依赖项。

（可选项）要安装用于非商业用途的库，请在 GitHub 上导航到 Microsoft / Quantum-NC。然后克隆存储库并打开 Quantum-NC.sln 解决方案。（此句话机翻 2333）

### 验证安装

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/qsharp/QQ%E6%88%AA%E5%9B%BE20180630115316.png)

右键 TeleportationSample 这个 project（在 Sample > 0.Introduction内）点击设为启动项目

然后按 F5 运行。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/qsharp/QQ%E5%9B%BE%E7%89%8720180630115633.png)

出现上图代表你已经成功配置好了。

## 如何新建一个 Q# 程序

文件 > 新建 > 项目

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/qsharp/QQ%E6%88%AA%E5%9B%BE20180630140945.png)

## 参考资料

[https://docs.microsoft.com/en-us/quantum/quantum-installconfig?view=qsharp-preview&tabs=tabid-vs2017](https://docs.microsoft.com/en-us/quantum/quantum-installconfig?view=qsharp-preview&tabs=tabid-vs2017)
