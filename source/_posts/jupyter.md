title: 一种交互式文档——Jupyter 的部署
date: 2018-06-16 23:10:43
desc: 
tags: [Python] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jupyter/title.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jupyter/title.jpg
---

也许说到 Jupyter 你会觉得陌生，但想必你或多或少听过鼎鼎大名的 IPython。

<!-- more -->

其实 Jupyter 脱胎于 IPython 项目，IPython 顾名思义，是专注于 Python 的项目，但随着项目发展壮大，已经不仅仅局限于 Python 这一种编程语言了。Jupyter 的名字就很好地释义了这一发展过程，它是 Julia、Python 以及 R 语言的组合，字形相近于木星（Jupiter），而且现在支持的语言也远超这三种了。

Jupyter 就是这样一个将说明文字、代码、图表、公式、结论都整合在一个文档中的文档工具。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jupyter/widgets.gif)

## Jupyter 的优点

- 极其适合数据分析
	想象一下如下混乱的场景：你在终端中运行程序，可视化结果却显示在另一个窗口中，包含函数和类的脚本存在其他文档中，更可恶的是你还需另外写一份说明文档来解释程序如何执行以及结果如何。此时 Jupyter Notebook 从天而降，将所有内容收归一处，你是不是顿觉灵台清明，思路更加清晰了呢？
- 支持多语言
	也许你习惯使用 R 语言来做数据分析，或者是想用学术界常用的 MATLAB 和 Mathematica，这些都不成问题，只要安装相对应的核（kernel）即可。
-  分享便捷
	支持以网页的形式分享，GitHub 中天然支持 Notebook 展示，也可以通过 nbviewer 分享你的文档。当然也支持导出成 HTML、Markdown 、PDF 等多种格式的文档。
- 远程运行
	在任何地点都可以通过网络链接远程服务器来实现运算。
- 交互式展现
	不仅可以输出图片、视频、数学公式，甚至可以呈现一些互动的可视化内容，比如可以缩放的地图或者是可以旋转的三维模型。

## 安装 Jupyter

首先我们先更新一下（可选项）
```bash
$ apt update
$ apt upgrade
```

然后安装 pip，用 pip 直接安装 Jupyter
```bash
$ apt install python3-pip
$ pip3 install jupyter
```

## 运行 Jupyter

```bash
$ jupyter notebook [--allow-root]
```
使用上述命令就可以直接启动 jupyter，如果你是 root 用户，需要添加 --allow-root 选项。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jupyter/QQ%E6%88%AA%E5%9B%BE20180616204944.png)

在本地，你可以直接用 token 访问，就可以直接开始使用啦。（在我的 Ubuntu 上他会自动启动浏览器）

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jupyter/QQ%E6%88%AA%E5%9B%BE20180616204915.png)

如果你是在 VPS 安装的 Jupyter，则需要映射到公网上，需要添加启动选项 --id=xxx.xxx.xxx.xxx 然后直接用浏览器访问就行了。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jupyter/QQ%E6%88%AA%E5%9B%BE20180616205439.png)

## 安装其他语言支持

[https://github.com/jupyter/jupyter/wiki/Jupyter-kernels](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels)

可以参考官方给出的 kernel 列表，根据需求安装自己需要的语言。

文章开头的图是 C++ 的 Cling 的一个示例


## 在线 Jupyter

除了自己搭建 Jupyter 之外，我们还可以用 Azure notebook

[https://notebooks.azure.com/](https://notebooks.azure.com/)

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/jupyter/QQ%E6%88%AA%E5%9B%BE20180616221105.png)

这是微软提供的在线jupyter服务，通过 Terminal 我们可以看到大概有 20 G 的存储空间，但是好像只支持 Python、R。

但是微软添加了其他的功能，你可以一键 clone 别人的供自己研究，也可以从 GitHub 上导入，然后还可以 git pull。