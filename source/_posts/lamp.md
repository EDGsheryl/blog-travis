title: LAMP 快速部署
date: 2017-12-23 02:05:45
desc: 
tags: [linux, sa] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/lamp.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/lamp.jpg
---

招新放题目上去的时候还要查来查去。。。如果可以写个脚本方便部署的话

<!-- more -->

其实也不会方便到哪里去 2333

## 说明

以下是当时操作的

## HISTORY
    1  apt update
    2  apt upgrade
    3  mkdir kernel && cd kernel
    4  apt install curl
    5  curl -O http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.14-rc1/linux-image-v4.14-rc1-generic_v4.14-rc1_amd64.deb
    6  ls
    7  dpkg -i linux-image-v4.14-rc1-generic_v4.14-rc1_amd64.deb 
    8  vim linux-image-v4.14-rc1-generic_v4.14-rc1_amd64.deb 
    9  rm linux-image-v4.14-rc1-generic_v4.14-rc1_amd64.deb 
    10  curl -O http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.14-rc1/linux-image-4.14.0-041400rc1-generic_4.14.0-041400rc1.201709162031_amd64.deb
    11  dpkg -i linux-image-4.14.0-041400rc1-generic_4.14.0-041400rc1.201709162031_amd64.deb 
    12  dpkg -l|grep linux-image
    13  apt purge linux-image-4.*
    14  apt purge linux-image-4.4.0-*
    15  dpkg -l|grep linux-image
    16  update-grub
    17  reboot
    18  echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
    19  echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
    20  sysctl -p
    21  sysctl net.ipv4.tcp_available_congestion_control
    22  sysctl net.ipv4.tcp_congestion_control
    23  lsmod | grep bbr
    24  curl pixiv.net
    25  apt install mysql-server
    26  apt install apache2
    27  apt install php7.0
    28  apt install php7.0-*
    29  cd /var/www/
    30  ls
    31  cd he
    32  cd html/
    33  ls
    34  vim index.php
    35  rm index.html 
    36  ls
    37  sudo /etc/init.d/apache2 restart
    38  sudo apt install libapache2-mod-php7.0
    39  history

## tips

- 升级 bbr 是为了防止服务器阻塞
- 一定最后安装 php
- 安装完 php 测试 phpinfo 否则会导致源码直接下载
- 如果 php 没解析说明没有安装 libapache2-mod-php7.0

## 脚本化

把 history 里的东西写进 1.sh 运行就行啦（我没试过 hhh）

    apt update
    apt upgrade
    apt install mysql-server
    apt install apache2
    apt install php7.0
    apt install php7.0-*
    apt install libapache2-mod-php7.0
    /etc/init.d/apache2 restart

然后新建一个 test.php，存入内容

	<?php
		phpinfo();
	?>

试试能不能用就可以辣

发现我当时打错了好多命令 还干了什么不可名状的操作 2333

