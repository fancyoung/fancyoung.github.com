---
layout: post
title: "将一切放在云端"
date: 2012-02-25 00:17
comments: true
categories: [Ruby]
---
> Github  
> Heroku  
> MongoHQ  
> UpYun  
> name.com  

一切在拖延症患者眼里都是障碍,
尤其是: 技术, 设计, 域名, 服务器.

## 技术
#### 语言
一个想法在脑子里几年了, 
首要问题是怎么做.  
从Java, PHP, Ruby一路走来, 
从Rails1, 2, 3, 中途好几次刚建好项目便放弃.  
到今天的3.2.1, 看上去最佳解决方案已经出炉. 
同时还要忍住去捯饬NodeJS的冲动. 

数据库用MongoDB, 
单是不用像MySQL一样migrate的特性, 
就让我深深爱上它.

#### 前端代码模板很有意思.
- HTML  
先前流行的是HAML, 
我也很喜欢它的格式.  
不过这回还是玩玩SLiM吧, 
虽然它的可读性不如前者.
- CSS  
三选一: SASS, SCSS, LESS.  
选定SASS.
一是因为之前用过比较熟, 
使用缩进的风格也是我喜欢的类型.  
一直不明白后来要推出SCSS这种不伦不类的东西.  
LESS偏向NodeJS系的, 以后有空再研究吧.
- JS  
CoffeeScript就先不考虑, 
JS是我最擅长的部分, 
就让我敲敲正常的代码吧.  
自从用jQuery后我就很少写真正的JS了, 
我恨jQuery!  
另外, UJS被Rails放弃也给我留下了一定的心理阴影.

#### 功能模块
我不是个NB的程序员, 我最喜欢做的事是用别人的轮子.  
与抄袭不同, 这一切都是开源的.  
我懂得欣赏它们, 也知道该如何更好的去用, 这大概算是我的一个优点.

- jQuery  
虽然我恨他, 但还是先用着吧.
怀念MooTools的日子.
- Mongoid  
Ruby里MongoDB的ODM(Object-Document-Mapper)框架.  
MongoMapper和Mongoid我选择了后者.  
- devise  
用户身份验证(Authentication)模块.  
- CarrierWave  
Rails的文件上传模块.  
其实Paperclip用的人更多, 不过不支持Mongoid.
- 图片处理  
图片处理肯定离不开ImageMagick, 
Ruby下的接口gem包有: RMagick和Mini magick.  
不过这回我打算使用又拍云(UpYun)存储图片, 
顺便就把图片处理也交给它做吧, 后面还会提到.

## 设计
还好有Bootstrip, 
有了它前期可以把更多的精力放在功能上.  
轻量级的Blueprint也是一个很不错的选择.
上天赐给我一名设计师吧!

## 域名
额...  
这个实在太重要了.  
想了几年终于想到一个还不错的域名, 
[iaieye.com](http://iaieye.com), 
这也是最近比较有动力的原因.

## 服务器
没有自己服务器, 
所以一切这么解决:  
- 代码交给Github   
Github就不介绍了, 最好, 没有之一.   
需要注意的是免费版不能加私密项目.  
国内最近有个GitCafe, 观望中.
- 项目放在Heroku  
- 数据库用MongoHQ  
免费16M, 先用着吧.
MongoLab免费240M, 
不过我喜欢前者的Icon.  
- 图片存到又拍云(UpYun)  
前段时间才发现国内已经有一些云服务了. 
又拍云的口碑不错, 还支持图片处理, 先用用看.  
盛大云仿佛也不错, 有云主机和MongoIC, 
不过备案是个大问题(有朋友推荐DNSPod来解决).

## 笔记
#### 配置文件里私密信息（尤其是密码不要进SVN）
- 用环境变量传递  
如: `uri: <%= ENV['USERNAME'] %>`

- 环境变量在Heroku里的设置  
添加: `$ heroku config:add USERNAME=fancyoung PASSWORD=123456 ......`  
查看: `heroku config`  
UpYun需要通过此方式配置  

#### MongoHQ配置
修改配置文件: `config/mongoid.yml`
```
...
production:
  uri: <%= ENV['MONGOHQ_URL'] %>
...
```

#### 发布到Heroku
`$ git push heroku master`

#### 绑定自己的域名
添加Heroku插件(Add-on): Custom Domain.   
Heroku里添加插件需要先用信用卡(需国际信用卡)认证.   

配置过程中, 发现3个IP都ping不通, 发现是被墙.   
最后用过设置CNAME的方式完成配置.   

## 参考
[Heroku绑定MongoHQ方法](http://devcenter.heroku.com/articles/mongohq)  
[用Heroku插件Custom Domain自定义域名](http://devcenter.heroku.com/articles/custom-domains)  
[配置Heroku上的变量](http://devcenter.heroku.com/articles/config-vars)  
