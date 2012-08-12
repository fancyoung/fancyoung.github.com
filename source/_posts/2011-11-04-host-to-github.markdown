---
layout: post
title: "Github Page绑定自己域名"
date: 2011-11-04 11:31
comments: true
categories: [Github]
---

<!--more-->

- 在项目根目录下建立一文件，名为`CNAME`，里面写上域名，如`fancyoung.com`
或者在命令行里执行：
```
$ echo 'fancyoung.com' >> source/CNAME
```
- 去自己的域名运营商（我是name.com）处修改:  
CNAME: www.fancyoung.com => fancyoung.github.com  
A: fancyoung.com => 207.97.227.245  

- 注意：  
文中fancyoung请替换为自己的域名  

[官方教程](http://pages.github.com/)
