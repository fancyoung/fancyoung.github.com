---
layout: post
title: "bundle install时的一些灵异bug"
date: 2012-05-02 13:12
comments: true
categories: [Ruby, Bug]
---
升级博客后，在另一台电脑上无法启动了。

## 在新电脑上Octopress写博客时没法`$ bundle install`
#### 现象：
`$ bundle install`安装到fast-stemmer时报一大堆错，
无法继续。
#### 原因：
不详，可能是rvm里的bundle没升级
#### 解决
做了一通操作，不知怎么就好了。。。
其中包括：
```
$ rvm gem update
```
不过我2次都引发了下面几个问题

## `$ bundle install RedCloth`时报错
#### 现象:
无法make，出错提示为：
```
Building native extensions.  This could take a while...
ERROR:  Error installing RedCloth:
        ERROR: Failed to build gem native extension.
...
make: /bin/install: Command not found
...
```
#### 原因：
查看发现`/bin/install`文件不存在
#### 解决：
```
$ ln -s /usr/bin/install /bin/install
```
参考：[网上有人给出了解决方案](http://jgarber.lighthouseapp.com/projects/13054/tickets/245)


## `$ bundle install`时直接安装到了当前目录  
#### 现象：
安装成功后提示：
`Your bundle is complete! It was installed into ./fast-stemmer`
用git等版本控制的话，会发现有新目录
#### 原因：
发现不知什么时候冒出了个新文件`.bundle/config`，里面的配置将安装指到当前目录。
#### 解决：
```
# 直接删除配置，一般用不到
$ rm -rf .bundle
# 这个目录也删掉，当然目录名不一定是fast-stemmer，可能需要修改
$ rm -rf fast-stemmer
# 重新安装，完成
$ bundle install
```

## 最后祭出大招：重装
根本问题仿佛是更新后gem版本混乱，可以尝试
```
# xxx为某个gem名
$ gem list xxx
$ gem uninstall xxx
$ gem install xxx
```
也可以试试直接重装，这个很好使
```
$ rvm uninstall ruby-1.9.2-p290
$ rvm install ruby-1.9.2-p290
```
重装后记得重新bundle install啊
