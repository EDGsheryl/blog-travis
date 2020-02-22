title: Archlinux 安装指北
date: 2018-06-17 09:41:56
desc: 
tags: [linux] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/arch/title.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/arch/title.jpg
---

这是一份 Archlinux 安装指北

<!-- more -->

## 下载镜像

从官方网站获取镜像，似乎被墙了？
[https://www.archlinux.org/](https://www.archlinux.org/)

## 启动镜像

VMware 没有 Arch 的选项，所以我们只能选择 Linux 内核 4.X 更高。

如果是对实体机安装，则需要其他工具，比如 LinuxLive USB Creator

## 选择 Boot Arch Linux (x86_64)

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/arch/QQ%E6%88%AA%E5%9B%BE20180617073025.png)

## 磁盘分区

查看块设备
```bash
lsblk
```

然后发现是 sda，那么我们直接对 `/dev/sda` 进行分区
```bash
fdisk /dev/sda
```

按 n 新建分区，根据对应操作即可。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/arch/QQ%E6%88%AA%E5%9B%BE20180617074247.png)

## 挂载硬盘

如果有其他分区 也需要挂载
```bash
mkfs.ext4 /dev/sda
mount /dev/sda /mnt
```
## 安装基本工具

```bash
pacstrap /mnt base base-devel
```


## 一些设置

生成一个 fstab 文件来规定磁盘分区、块设备，或者远程文件系统是如何挂载进文件系统中的。
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

进入 chroot 环境，这样可以为当前进程以及子进程切换当前根目录。
```bash
arch-chroot /mnt
```

设置时间
```bash
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
hwclock --systohc --utc
```

设置语言
```bash
nano /etc/locale.gen 
```
然后将 en_US UTF8 这行注释掉，或者是换成你想要的语言。（推荐英语）

```bash
locale-gen
echo LANG=en_US.UTF-8 > /etc/locale.conf
export LANG=en_US.UTF-8
```

## 主机名

```bash
echo <主机名> > /etc/hostname
```

接着向 `/etc/hosts` 文件添加 hosts 条目。

```text
#<ip-address>	<hostname.domain.org>	<hostname>
127.0.0.1	localhost.localdomain	localhost
::1		localhost.localdomain	localhost
127.0.1.1	<主机名>.localdomain	<主机名>
```

## 设置 root 密码

```bash
passwd
```

## 安装 GRUB 引导

```bash
pacman -S grub os-prober
grub-install --target=i386-pc /dev/sdX    # sdX 为目标磁盘
grub-mkconfig -o /boot/grub/grub.cfg
```

## 快结束辣

```bash
exit # 回到安装环境
umount -R /mnt
reboot
```

到这里，系统其实已经装好啦。

## 启动网络

```bash
ip link
```

yournetworkname 在那个方括号前面
```bash
vi /etc/systemd/network/yournetworkname.network
```

添加下述内容
```text
[Match]
name=en*
[Network]
DHCP=yes
```

```bash
systemctl restart systemd-networkd
systemctl enable systemd-networkd
```

将下面这两句话加进 /etc/resolv.conf 中

```text
nameserver 8.8.8.8
nameserver 8.8.4.4
```

## 安装驱动

```bash
pacman -S <驱动包>
```
官方支持的驱动包：
- 通用：xf86-video-vesa
- 因特尔系：xf86-video-intel
- AMD/ATI 系：xf86-video-ati
- nVidia 系：
	GeForce 400 及更新系列：nvidia
	2006 至 2010 年间 GeForce 8000/9000、ION 和 100-300 系列 [NV5x, NV8x, NV9x and NVAx]：nvidia-340xx
	2004 至 2006 年间 GeForce 6000/7000 系列 [NV4x and NV6x]：nvidia-304xx

## 安装桌面环境

```bash
pacman -S xorg xorg-server
pacman -S gnome gnome-extra
systemctl start gdm.service
systemctl enable gdm.service
```

如果 systemctl start gdm.service 死机了 建议重启 qwq
