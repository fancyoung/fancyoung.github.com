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
