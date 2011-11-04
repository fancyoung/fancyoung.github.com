---
layout: post
title: "技术博客利器——Octopress"
date: 2011-11-04 12:59
comments: true
categories: 
---

## 常用命令
#### 注意  
有些机子上运行可能会报错，需要在命令前加上`bundle exec`

#### 添加文章  
```
$ rake new_post["title"]
```
运行后会通过`title`生成相关文件、链接，可在文件里修改显示出来的标题。  
`title`可以使用中文，会自动转化为拼音（个人不建议，因为链接会比较无意义）。  

```
$ rake generate       #发布文件到public目录
$ rake watch          #监控source和sass目录的变动
$ rake preview        #启动服务器并监控变动，通过http://localhost:4000预览
```

#### 发布  
```
$ rake generate
$ rake deploy
```

#### 保存源代码
因为发布的只是生成的静态页面，  
需要在项目里建立source分支用于保存整个项目源代码（配置、markdown文件等）。
```
$ git add .
$ git commit -m 'blog'
$ git push origin source
```

## 参考
[Octopress官方文档](http://octopress.org/docs/)  
[markdown语法](http://daringfireball.net/projects/markdown/syntax)
