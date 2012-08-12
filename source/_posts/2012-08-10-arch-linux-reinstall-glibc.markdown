---
layout: post
title: "Arch升级失败后修复glibc记录"
date: 2012-08-10 00:27
comments: true
categories: [Arch Linux, 经验]
---
## 起因
`$ pacman -Syu`时提示错误，
因为Arch前段时间将`/lib`目录链到了`/usr/lib`，
见公告[The /lib directory becomes a symlink](http://www.archlinux.org/news/the-lib-directory-becomes-a-symlink/)。
当时没有看到这篇公告，而在网上搜到某贴说使用`--force`参数，
结果执行完后系统挂掉，因`glibc`不存在，所有命令行不可使用。

## 解决方法
- 从光盘启动Arch。
- `$ fdisk -l`查看磁盘状态，
我的系统分区为`/dev/sda6`。
- 创建目录：`$ mkdir /root/tmp_disk`。
- mount分区，我机子上是：`$ mount /dev/sda6 /root/tmp_disk`。
- 下载[相应的](http://www.archlinux.org/packages/?q=glibc)`glibc`安装包（网络或U盘，配置网络参考下面相关部分）,
我的为[x86_64 v2.16.0-2](http://www.archlinux.org/packages/core/x86_64/glibc/)，
所以`wget http://www.archlinux.org/packages/core/x86_64/glibc/download/`
- 安装`pacman -U glibc-2.16.0-2-x86_64.pkg.tar.xz -r /root/tmp_disk`
- `pacman -Su`

#### 注意

## 其它
#### 配置网络
用启动光盘进入系统后，需要配置网络来下载最新glibc。
配置`/etc/rc.conf`
```
interface=eth0
address=192.168.0.2
netmask=255.255.255.0
gateway=192.168.22.1
```
配置`/etc/resolv.conf`
```
nameserver 8.8.8.8
```
最后重启网络服务`$ /etc/rc.d/network restart`

#### 目录
`/lib`、`/lib64`皆应软链到`/usr/lib`目录。
在修复过程中查看`/lib`发现里面只有一个`modules`目录，
将其移至`/usr/lib`里后建立软链。
系统正常运行，但之后执行`pacman`后无法升级。
移除`/usr/lib/modules`目录后`$ pacman -Su`解决问题。

#### 时间错误的解决
遇到报错
```
******************* FILESYSTEM CHECK FAILED *************
* Please repair manually and reboot. Note that the root *
* filesystem is currently mounted read-only. To remount *
* it read-write type: mount -n -o remount,rw / *
* When you exit the mantenance shel the system will *
* reboot automatically. *
*********************************************************
```
因为BIOS时间设置有问题。

## 参考
[bug修复方案：How to re-install glibc?](https://bbs.archlinux.org/viewtopic.php?id=142459)

[Arch网络配置：Configuring Network](https://wiki.archlinux.org/index.php/Configuring_Network)
