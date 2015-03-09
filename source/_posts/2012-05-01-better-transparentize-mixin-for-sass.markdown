---
layout: post
title: "Sass中通过mixin封装透明背景模块"
date: 2012-05-01 22:51
comments: true
categories: [前端]
---
之前讲到过[CSS实现背景透明完美解决方案](/blog/css-background-transparency/)，  
在Sass里可以通过mixin将其封装起来。  

## 先回顾一下
```
/* 白色背景,透明度0.6 */
.alpha60 {
  background: rgb(255, 255, 255);
  background: rgba(255, 255, 255, 0.6);
  background: transparent\9;
  zoom: 1;
  filter:progid:DXImageTransform.Microsoft.gradient(startColorstr=#99ffffff, endColorstr=#99ffffff);
  -ms-filter: "progid:DXImageTransform.Microsoft.gradient(startColorstr=#99ffffff, endColorstr=#99ffffff)";
}
```

## 分析
需要做的工作有：  
- 颜色和透明值应该通过参数传入  
- 需要能计算出rgba值：`rgb(255, 255, 255)`  
- 需要计算出IE下的值`#99ffffff`  
- 封装成minix模块，以便调用

## 过程
Sass的文档不全，为了查找一些计算函数，我只好去源码里找。  
开始想寻求的是一个转十六进制的方法，结果发现`ie_hex_str`已经实现了。  
在这里贴段里面的实现代码，来看看Sass的计算功能：  

```
# Sass
alpha = (color.alpha * 255).round.to_s(16).rjust(2, '0')
# 等价于JS中的：
Math.round(0.6 * 255).toString(16);
```

最后的rjust方法，应该是空位补零。

非常有用的两个页面：
[函数源码](https://github.com/nex3/sass/blob/master/lib/sass/script/functions.rb)，
[在线调试Sass](http://sass-lang.com/try.html)

## 总结
最终代码如下：
```
@mixin better_transparentize($color, $alpha)
  $c: rgba($color, $alpha)
  $ie_c: ie_hex_str($c)
  background: rgba($color, 1)
  background: $c
  background: transparent\9
  zoom: 1
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr=#{$ie_c}, endColorstr=#{$ie_c})
  -ms-filter: "progid:DXImageTransform.Microsoft.gradient(startColorstr=#{$ie_c}, endColorstr=#{$ie_c})"
```
然后在需要的地方直接引用即可，如：
```
.box
  @include better_transparentize(white, .8)
```
