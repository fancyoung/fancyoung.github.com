---
layout: post
title: "技术博客利器——Octopress"
date: 2011-11-04 12:59
comments: true
categories: [Ruby]
---

## Octopress简介
> Octopress is a framework designed by Brandon Mathis for Jekyll, the blog aware static site generator powering Github Pages.  

<!--more-->

#### 优点
用文件方式储存数据，无需数据库  
以静态方式发布，可直接挂在github等地方  
用markdown格式写博客  
可以轻松的配置和发布

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

## 更多设置
#### 添加"关于我"
在`source`下新建`about`目录，并在里面添加`index.markdown`文件。  
编辑导航条`source/_includes/custom/navigation.html`  
注意:`index.markdown`文件需要加上头，否则会找不到。  



## Bug Fix

#### 不能进行deploy  
问题：有次发现`$ rake deploy`不能发布，但是预览正常。检查github上source分支代码已更新，但master仍为老代码。  
原因：发现是因为代码是新从github下clone下来的，未进行初始化deploy。  
解决：需要执行`$ rake setup_github_pages`进行初始化。  
注意：rake操作应该在source分支下进行，若是刚从github里clone下来的，请先执行`$ git checkout source`。

## 参考
[Octopress官方文档](http://octopress.org/docs/)  
[markdown语法](http://daringfireball.net/projects/markdown/syntax)
