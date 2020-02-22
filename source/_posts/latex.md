title: LaTeX 入门学习笔记
date: 2017-03-20 01:54:29
desc: 
tags: [lang] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/latex.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/latex.jpg
---

《离散数学》老师表示大家可以用 LaTeX 写课设，于是周末心血来潮准备用 LaTeX 写论文，哇安装起来很麻烦，最终在叶姐姐的指导下写完了QwQ。

<!-- more -->

# 安装

有很多方案，我一开始选择 latatexLive + atom 然后，我的 atom 挂了。。

Plan B：latexlive + sublime text 然后我卸载的时候，不知道卸了什么其他的东西，不过电脑好像没有坏。

最后选择了 Win 的套餐 CTeX

# 使用

## documentclass
```
	\documentclass[]{}
```
文档设置，用 utf-8 参数来支持中文，不过不知道为什么，复制到其他地方就会导致打不开，可能默认用 ascii 打开文档导致溢出爆炸？

## usepackage

载入库，类似与 Python 的 import 或者说是 C 系的 include
```
	\usepackage{}
	\usepackage[top=1in,bottom=1in,left=1.25in,right=1.25in]{geometry}
```
可以设置页面边距哟

## begin

来闭合一个区域
```
	\begin
	\end
```

## author

设置作者
```
	\author{}
```

## title

设置文章标题
```
	\title{}
```
## maketitle

让该页面加入标题作者时间信息

```
	\maketitle
```

## section

格式化文章，真的很好用

```
	\\(?:sub){0,1,2}section
```

(上面是 \section 和 \subsection 和 \subsubsection 的意思，叶姐姐太强了)

## cite
引用
```
	\cite{}
```

配合使用形成参考文献
```
	\begin{thebibliography}{0}
	
	\end{thebibliography}
```

## 其他

\\是换行

\par是换段落

\newpage换页

# 范例
```latex
	\documentclass[UTF8]{ctexart}
	\usepackage[top=1in,bottom=1in,left=1.25in,right=1.25in]{geometry}
	\usepackage{cite}
	\usepackage{abstract}
		\author{EDGsheryl}
	    \title{SQL技术研究综述}
	
	\begin{document}
		\maketitle
	    \begin{abstract}  随着计算机技术的迅速发展，在“信息时代”的21世纪，计算…… \textbf{关键词：SQL，库存管理系统}
	    \end{abstract}
	
	    \section{引言}
	    结构化查询语言(Structured Query Language)简称SQL，是一种特殊目的的编程\cite{Baidu}
	
	    \section{SQL技术简介}
	        \subsection{应用}
	        结构化查询语言SQL（STRUCTURED QUERY LANGUAGE）是最重要的关系数据……
	        \subsection{支持标准}
	        SQL 是1986年10 月由美国国家标准局（ANSI）通过的数据库语言美国标……
	        \subsection{其他版本SQL}
	        各种不同的数据库对SQL语言的支持与标准存在着细微的不同，这是因为，……
	
	    \section{SQL引擎工作原理及对比}
	        \subsection{ISAM}
	        ISAM是一个定义明确且历经时间考验的数据表格管理方法，它在设计之时就考虑到……
	        \subsection{MyISAM}
	        MyISAM是MySQL的ISAM扩展格式和缺省的数据库引擎。除了提供ISAM里所没有的索……
	        \subsection{HEAP}
	        HEAP允许只驻留在内存里的临时表格。驻留在内存里让HEAP要比ISAM和MYISAM都快，……
	        \subsection{InnoDB}
	        InnoDB数据库引擎都是造就MySQL灵活性的技术的直接产品，……\cite{yuanli,duibi}
	
	    \section{目前SQL技术中所存在的不足}
	        （1）安全问题。……\par （2）效率问题。……
	
	    \section{总结和展望}
	    SQL技术作为现有库存管理技术的主力军，必然有他的优势之处，随着非关系数据库的扩大使用，会减少关系型数据库的安全问题。
	
	    \begin{thebibliography}{0}
	        \bibitem{Baidu}
	        SQL ．维基百科，2015-01-31
	        \bibitem{yuanli}
	        李武．姚珺．数据库原理及应用．哈尔滨：哈尔滨工程大学出版社，2011：179
	        \bibitem{duibi}
	        Wilson ． 浅谈My SQL引擎的对比，2015
	    \end{thebibliography}
	
	
	\end{document}
```
