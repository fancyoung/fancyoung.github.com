---
layout: page
title: "Linux常用命令"
date: 2015-01-01 19:00
comments: true
sharing: true
footer: true
---
`Alt + .`
插入上一个命令的最后一个参数

`$ wc -l`
统计行数，常配合其它命令使用

`$ du -sh dirname`
查看某目录大小

`$ scp frompath username@xxx.xxx.xxx:/path/on/server`
与远程之间传文件

`grep -R 关键字 目录`
在目录所有文件里搜索关键字（`-Rn`为显示行号， `-Rl`为仅显示文件名）

## 进阶命令

`$ history | awk '{print $2}' | sort | uniq -c | sort -rn | head`
查看常用命令 

## 网络
`$ netstat -anp |awk '{print $6}'|sort|uniq -c |sort -rn`
查看SYN数量

`$ netstat -an | grep SYN | awk '{print $5}' | awk -F: '{print $1}' | sort | uniq -c | sort -nr | more`
查看最高的ip

## 权限
`$ cat /etc/passwd`
查看所有用户列表

`$ cat /etc/group`
查看所有组

`$ group`
查看当前用户所在组（后面加用户名可查相应组）

## 其它工具

### 截屏 scrot
`$ scrot path/filename`

`-s`鼠标选定区域，
`-bs`抓取窗口，
`-cd 10`延时10秒

### screen
- 进入screen前：
查看 `$ screen -ls`
以某名新建 `$ screen -S session_name`
进入某名 `$ screen -r session_name`
kill `$ screen -X -S session_name quit`
attach未detached的 `$ screen -r -D session_name`
协同操作 `$screen -x session_name`

`su`进别人账户用screen报错`Cannot open your terminal '/dev/pts/1'`，
执行`$ script /dev/null`解决。

- 进入后
前缀默认`Ctrl-a`，因为键冲突，我改成`Ctrl-o`。
编辑`.screenrc`，添加行`escape ^oo`

查看子窗口列表`w`，
杀死子窗口`k`，
挂起screen`d`，
子窗口间切换`n/p`,
分屏`S`，
分屏间切换`Tab`

## 其他
[15 个鲜为人知的Unix命令](http://www.admin10000.com/document/4655.html)

