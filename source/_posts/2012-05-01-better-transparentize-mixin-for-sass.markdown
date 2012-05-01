---
layout: post
title: "Sass中通过mixin封装透明背景模块"
date: 2012-05-01 22:51
comments: true
categories: [前端]
---
之前讲到过[CSS实现背景透明完美解决方案](/blog/css-background-transparency/)，  
在Sass里可以通过mixin将其封装起来：

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
