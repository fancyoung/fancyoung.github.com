---
layout: post
title: "用Emacs远程编辑文件及相关笔记"
date: 2012-06-02 10:16
comments: true
categories: 
---

#### Emacs编辑远程文件
非常简单：`C-x C-f`后`/ssh:user@host#port:file`

由此可以推出一个小技巧：

#### Emacs编辑本地需要sudo的文件
`/ssh:root@locahost:file`

过程中可能会遇到的问题：

* 1  
问题：`ssh: connect to host localhost port 22: Connection refused`  
原因：没装openssh-server  
解决：安装即可

* 2  
问题：`ssh root@localhost`并输入密码后报`permission denied`  
原因：发现直接用`su`也不行（之前一直都只是sudo），因为没设root密码  
解决：`sudo passwd root`
