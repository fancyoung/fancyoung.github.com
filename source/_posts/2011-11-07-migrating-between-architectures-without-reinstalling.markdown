---
layout: post
title: "将Arch Linux从32位升到64位"
date: 2011-11-07 14:37
comments: true
categories: 
---

- 翻译自Arch Wiki：[Migrating Between Architectures Without Reinstalling](https://wiki.archlinux.org/index.php/Migrating_Between_Architectures_Without_Reinstalling)
- i686为32位，x86_64位64位

## 准备工作
### 确认为64位平台
如果你已经正在使用x86_64但是想安装i686，可以跳过此步。
为了运行64位软件，你的CPU必须支持64位。现在大部分CPU都支持64位。你可以通过运行一下命令来确认：
```
$ grep --color 'lm' /proc/cpuinfo
```
（原文中为```grep --color '\' /proc/cpuinfo```， 应该不对）
当CPU为x86_64平台时，输出结果里会出现高亮的 ```lm``` （“long mode”）。
注意不是```lahf_lm```，它和64位无关。

### 硬盘空间
在迁移过程中，```/var/cache/pacman/pkg```的大小将翻倍，请为此做好准备。这是假定cache里只有当前安装的包，就像```$ pacman -Sc```（clean）刚运行过一样。使用空间增长是因为所有包同时有i686和x86_64两个版本。
如果你没有足够的空间，可以使用[gparted](https://wiki.archlinux.org/index.php/Gparted)来调整相关分区大小，或者mount另一个分区到```/var/cache/pacman```。
在迁移过程中请不要移除老框架的软件包，知道完全升级成功。过早的移除会使你无法回退和还原变更。

### 电源支持
升级时间比较长，并且不可中断。根据你的 安装包大小及网络速度，你最好为此准备至少一个小时的升级时间（虽然你可以先把它们下载下来）。请保证你的电源稳定。

### 回退准备
如果迁移过程中失败，有些包可以帮助你解决此时的问题，但是需要你在迁移之前安装。详情可以参考后面的 #Troubleshooting 。
包[busybox](https://www.archlinux.org/packages/?name=busybox)可以用来还原变更。它不依赖于其他包，可以单独安装。通过下面命令可以安装32位（i686）的版本
```
$ pacman -S busybox
```
另一个包是[lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc)，在[Multilib](https://wiki.archlinux.org/index.php/Multilib_Project)的x86_64资源库里。这个只有当你从32位迁移至其它版本时才可能使用（It is probably only useful when migrating away from 32 bits）;无论如何你可能安全跳过这个包。你可以用这个包来运行32位程序，通过明确的调用```/lib/ld-linux-x86-32.so.2```。可用下面命令行安装。
```
$ pacman -S lib32-glibc
```

## 方法1：使用Arch LiveCD
1. 下载、刻录并启动64位Arch ISO LiveCD。
2. 配置LiveCD的网络，然后pacman用新的库。
3. 将现在的安装挂在到```/mnt```目录。如：```mount /dev/sda1 /mnt```
4. 使用下面的脚本来执行：升级本地pacman数据库、取得本地安装包列表并重新安装：
```
#!/bin/bash

MOUNTED_INSTALL='/mnt'
TEMP_FILE='/tmp/packages.list'

pacman --root $MOUNTED_INSTALL -Sy
pacman --root $MOUNTED_INSTALL -Qqet > $TEMP_FILE

for PKG in $(cat $TEMP_FILE) ; do
   pacman --root $MOUNTED_INSTALL -S $PKG --noconfirm
done

exit 0
```

## 方法2：从当前系统升级
### 准备
#### Cache old packages
> 注意：如果你有从AUR或第三方库的包，并且在新的平台里查询不到，pacman会告知找不到相应替代。将这些包记录下来，以便在升级成功后重新安装，并用```$ pacman -Rsn package_name```来卸载。

确保你现在的包都在你的cache里，下载它们（老平台的）以便回退。
```
$ pacman -Sw $(comm -23 <(pacman -Qq) <(pacman -Qmq))
```
或者用pacman-contrib包里的bacman来生成它们。
如果你是从32位迁移，现在可以安装32位的Busybox
```
$ pacman -S busybox
```

#### 更换pacman平台
编辑配置文件```/etc/pacman.conf```并且把```Architecture```从```auto```改为新值。你可以参考下面的sed命令：
For x86_64
```
$ sed -i -e s/'Architecture = auto'/'Architecture = x86_64'/g /etc/pacman.conf
```
For i686
```
$ sed -i -e s/'Architecture = auto'/'Architecture = i686'/g /etc/pacman.conf
```
手动移除Pacman软件仓库的数据库，强制同步新的软件仓库：
```
$ rm -rf /var/lib/pacman/sync/*   # remove existing repository cache
$ pacman -Sy                      # sync new architecture repositories
```

#### 下载新包
给所有当前安装包下载新平台版本
```
$ pacman -Sw $(pacman -Qq|sed '/^lib32-/ d')  # download new package versions
```
如果有些包不能下载，请删除它们。
如果是迁移到32位，安装32位的Busybox fallback now that Pacman has been configured with the 32-bit architecture:
```
$ pacman -S busybox
```
或者，如果是迁移到64位，安装lib-32-glibc fallback:
```
$ pacman -S lib32-glibc
```

### 安装包
#### 安装内核（64位）
将内核升级到64位（x86_64）很安全很简单：32位和64位的应用在64位内核下都能很好的运行。如果是从64位迁移至其它平台，leave the 64-bit kernel installed and running for now and skip this step.
用下面命令安装Arch Linux内核：
```
$ pacman -S linux
```
启动新的64位内核，并确认它运行x86_64平台：
```
$ uname -m
```

#### 控制台终端
现在切换到一个text-mode虚拟控制台（可以通过Ctrl+Alt+F1）来完成接下来的步骤。你可以使用SSH之类的伪终端，但不建议你这么做。有些包会被移除或者被替换，可能会导致X11桌面不稳定，以至于系统无法启动。

#### 安装Pacman
> 警告：一旦你开始升级pacman及相关依赖，便不能中断。Pacman及相关依赖必须在同一条命令行上同时安装。
```
$ pacman -S pacman glibc libfetch libarchive openssl acl attr xz-utils bzip2 zlib readline bash ncurses expat
```
Immediately following this command only Busybox, Bash and Pacman will be executable until the other packages are migrated below. 安装成功前不能重启。

#### 安装已存在的包
为新平台安装所有之前下载的替换。（此时可以休息休息，因为需要花费一段时间。）
```
$ pacman -S $(pacman -Qq)
```
For migration away from 64 bits, you may want to skip installing a 32-bit kernel in the command above, since the old 64-bit kernel will still run 32-bit programs.
完整这步迁移后，各方面都已经完成并且可以重启电脑。

### 清理
你现在可以移除Busybox和lib32-glibc。
```
$ pacman -Rcn busybox lib32-glibc
```
#### Makepkg compiler flags
升级中新版的```/etc/makepkg.conf```可能会被保存至```/etc/makepkg.conf.pacnew```。如果你以后要用[makepkg](https://wiki.archlinux.org/index.php/Makepkg)进行编译，你必须替换或修改老版本。
```
$ mv /etc/makepkg.conf /etc/makepkg.conf.backup && mv /etc/makepkg.conf.pacnew /etc/makepkg.conf
```
It might also be a good idea to just get a list of "new" additions to /etc. You can get a list with the following command:
```
$ find /etc/ -type f -name \*.pac\*
```

## 问题解决
在升级过程中，当glibc替换为新版本后，许多老版本的程序将不能运行。如果发生此类问题，你可以用[busybox](https://www.archlinux.org/packages/?name=busybox)和[lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc)来解决。

### Busybox
In Arch, Busybox is statically linked; it can run without any libraries. There are many commands available to you. For example, to extract an i686 version of Pacman from a cached package:
```
$ busybox tar xf /var/cache/pacman/pkg/pacman-3.3.2-1-i686.pkg.tar.gz -C <some folder>
```

### Lib32-glibc
Example run 32 bit /bin/ls:
```
$ /lib/ld-linux-x86-32.so.2 /bin/ls
```

## 其它
- [Migrate installation to new hardware](https://wiki.archlinux.org/index.php/Migrate_installation_to_new_hardware)
