---
layout: post
title: "技术博客利器——Octopress"
date: 2011-11-04 12:59
comments: true
categories: [Ruby]
---

## Octopress简介
> [Octopress](https://github.com/imathis/octopress) is a framework designed by Brandon Mathis for [Jekyll](https://github.com/mojombo/jekyll), the blog aware static site generator powering Github Pages.  

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

#### 首页只显示摘要
- 在文中加入`<!--more-->`来控制摘要截取位置
- 修改`_config.yml`里的`excerpt_link`控制链接文字

#### 部署到Github
操作步骤参考：[Deploying to Github Pages](http://octopress.org/docs/deploying/github/)  
如果你有自己的域名，可参考：[Github Page绑定自己域名](http://fancyoung.com/blog/host-to-github/)

## Bug Fix

#### 不能进行deploy(Github)  
问题：有次发现`$ rake deploy`不能发布，但是预览正常。检查github上source分支代码已更新，但master仍为老代码。  
原因：发现是因为代码是新从github下clone下来的，未进行初始化deploy。  
解决：需要执行`$ rake setup_github_pages`进行初始化。  
注意：rake操作应该在source分支下进行，若是刚从github里clone下来的，请先执行`$ git checkout source`。

#### 修改的样式preview时不生效
问题：预览时发现之前设置成功的自定义样式不生效，变回默认样式。  
解决：`$ rake generate`即可，会重新生成css。  

####  无法update octopress
每过一段时间，可能需要[更新一下Octopress版本](http://octopress.org/docs/updating/)，
问题：执行`$ git pull octopress master`时报错：`fatal: 'octopress' does not appear to be a git repository`
原因：没有相应远程分支（第一次生成博客的项目中才有？）。打开`.git/config`查看，应该不包含`[remote "octopress"]`块。
解决：手动添加，或者在命令行执行：`$ git remote add octopress https://github.com/imathis/octopress.git`

## 参考
[Octopress官方文档](http://octopress.org/docs/)  
[markdown语法](http://daringfireball.net/projects/markdown/syntax)
