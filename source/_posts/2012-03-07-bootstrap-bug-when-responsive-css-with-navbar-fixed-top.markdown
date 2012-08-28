---
layout: post
title: "Bootstrap使用响应式设计(Responsive design)时导航条上部有空白的解决方案"
date: 2012-03-07 17:32
comments: true
categories: [Bootstrap, 问题解决]
---

#### 原因
Bug出现需要同时满足以下3个条件:  
- 顶部导航条navbar使用class`navbar-fixed-top`  
- 参考Bootstrap官方网站, 给body添加样式`padding-top: 60px;`  
- 使用响应式(Responsive design), 并且处在此状态下(默认为宽度<=980时触发)  

#### 解决方案1
给此段样式加上条件  
```
@media (min-width: 981px) {
    body {
        padding-top: 60px;
    }
}
```

#### 解决方案2
将bootstrap-responsive.css放在body样式之后  
```
<link href="../css/bootstrap.css" rel="stylesheet">
<style type="text/css">
      body {
        padding-top: 60px;
      }
</style>
<link href="../css/bootstrap-responsive.css" rel="stylesheet">
```
Rails3.2的Asset Pipeline就更方便了，放在import中即可（我用的是Sass）
```
@import compass
$baseFontSize: 15px
@import compass_twitter_bootstrap
body
  padding-top: 60px
@import compass_twitter_bootstrap_responsive
```

#### 结论
我在某项目中因为使用的是customize出来的单个css文件, 所以采用了解决方案1.  
在另一RoR项目中考虑使用解决方案2.

#### 参考
[navbar-fixed-top breaks when using responsive css](https://github.com/twitter/bootstrap/issues/1570)
