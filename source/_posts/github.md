title: 我的 GitHub 入门笔记
date: 2017-03-02 01:41:00
desc: 
tags: [github] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/github.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/github.jpg
---

GitHub 是一个面向开源及私有软件项目的托管平台，因为只支持 Git 作为唯一的版本库格式进行托管，故名 GitHub。

<!-- more -->

GitHub 于 2008 年 4 月 10 日正式上线，除了 Git 代码仓库托管及基本的 Web 管理界面以外，还提供了订阅、讨论组、文本渲染、在线文件编辑器、协作图谱（报表）、代码片段分享（Gist）等功能。目前，其注册用户已经超过350万，托管版本数量也是非常之多，其中不乏知名开源项目 Ruby on Rails、jQuery、python 等。——百度百科


## 配置指南

### 配置SSH Key

#### 创建SSH Key。
在用户主目录下，看看有没有 .ssh 目录，如果有，再看看这个目录下有没有 id_rsa 和 id_rsa.pub 这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开 Shell（Windows 下打开 Git Bash），创建 SSH Key：

```bash
$ ssh-keygen -t rsa -C "youremail@example.com"
```


你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个 Key 也不是用于军事目的，所以也无需设置密码。

如果一切顺利的话，可以在用户主目录里找到 .ssh 目录，里面有 id_rsa 和 id_rsa.pub 两个文件，这两个就是 SSH Key 的秘钥对，id_rsa 是私钥，不能泄露出去，id_rsa.pub 是公钥，可以放心地告诉任何人。

#### GitHub端设置

打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意 Title，在 Key 文本框里粘贴 id_rsa.pub 文件的内容

点“Add Key”

### 本地配置

#### 安装git

```bash
$ sudo apt-get install git
```

#### 配置本地git

```bash
$ git config --global user.email "email@youremail.com"
$ git config --global user.name "yourname"
```

#### 关联远程库

在想关联的目录下

```bash
$ init
$ git remote add origin git@github.com:YOURID/YOURPROJECT.git
$ git push -u origin master
```

#### 日常维护

每次更新完以后，我们该怎么操作呢

```bash
$ git add -A
$ git commit -m "UPDATE ANOUCIATING"
$ git push origin master
```

## github的用处

1、共享操作一个工程

2、共享成果

~~3、炫耀自己的牛逼之处~~