---
layout: post
title: "CSS实现背景透明完美解决方案"
date: 2011-11-29 16:44
comments: true
categories: [前端, 翻译]
published: true
---

翻译自: [CSS Background Transparency Without Affecting Child Elements, Through RGBa And Filters](http://robertnyman.com/2010/01/11/css-background-transparency-without-affecting-child-elements-through-rgba-and-filters/)

当今的大部分网页设计都包含了半透明的元素.但用CSS实现想要的效果却没那么简单.

## 现存的问题
如果我们想要一个半透明背景,有两种实现方式:  
- 利用CSS和opacity属性  
- 建立一个24位PNG背景图片  
用opacity的问题除了
[需要通过麻烦的语法来兼容所有浏览器](http://robertnyman.com/2008/09/16/you-want-css-opacity-to-go-with-that-well-suit-yourself/),
还有不单该元素自身背景透明了,它的子元素也会透明.
所以里面所有的文字也是透明的,这一般不是想要的效果.
你可以做一些CSS trick,通过建立额外的元素来解决这个问题,但这种解决方案很恶心.

用PNG的问题是会额外增加HTTP请求,
而且图片比几行css代码要大得多-
尤其考虑到图片不能太小以避免
[IE下24位PNG图透明时引起的内存泄漏](http://robertnyman.com/2009/05/26/serious-memory-leak-issue-with-24-bit-png-images-with-alpha-transparency-in-internet-explorer/).

## 解决方案
这里提供一种方法:
[RGBa colors](http://en.wikipedia.org/wiki/RGBA_color_space).
它的美妙之处在于你可以通过设置RGB值和透明值,轻松的实现颜色透明.
代码如下:
```
.alpha60 {
  /* 用于不支持RGBa的浏览器 */
  background: rgb(0, 0, 0);
  /* RGBa, 透明度0.6 */
  background: rgba(0, 0, 0, 0.6);
}
```
透明将只对背景生效,很好很强大,对吧:)

### 继续
不幸的是IE不支持RGBa(IE678都不行).
幸运的是微软在2000年时疯狂的给IE加上了各种过滤器.
其中有一个是[渐变过滤器(the gradient filter)](http://msdn.microsoft.com/en-us/library/ms532997\(VS.85\).aspx),
我们只需要把开始结束都设置成一个颜色就可以了.
你现在会想,"那我们怎么将其透明呢?".
你只需要用16进制值来定义颜色就可以了.
下面是用渐变过滤器实现和上面同等透明效果的代码:
```
.alpha60 {
  filter:progid:DXImageTransform.Microsoft.gradient(startColorstr=#99000000, endColorstr=#99000000);
}
```
你可以看到定义里的8位16进制数字,
前两位代表透明度,接下来两位是红色,接着就是绿色和蓝色.
注意两位16进制颜色的范围是0~255(ff).
那我们怎么将`0.6`转化为16进制数呢?

这里就需要用到一些数学知识了.
基本上,我们只需要将需要的透明度(比如0.6)乘以255,再转化为16进制即可.
还有一个简单的办法是利用
[Google’s Search Features](http://www.google.com/help/features.html),
你只需要在Google里搜索
[0.6 * 255 in hex](http://www.google.se/search?q=0.6+*+255+in+hex)
就能得到答案.
不过Google计算器仿佛只能处理整数,而
[0.3 * 255 in hex](http://www.google.se/search?q=0.3+*+255+in+hex)
它便无法得出结果.

还有一种更快的方法就是利用JavaScript,
只需要在浏览器控制行里输入
```
Math.floor(0.6 * 255).toString(16);
```
便能得出结果.

### 整合
根据上面的方法,我们来写一个完整的实现:
```
.alpha60 {
  /* Fallback for web browsers that doesn't support RGBa */
  background: rgb(0, 0, 0);
  /* RGBa with 0.6 opacity */
  background: rgba(0, 0, 0, 0.6);
  /* For IE 5.5 - 7*/
  filter:progid:DXImageTransform.Microsoft.gradient(startColorstr=#99000000, endColorstr=#99000000);
  /* For IE 8*/
  -ms-filter: "progid:DXImageTransform.Microsoft.gradient(startColorstr=#99000000, endColorstr=#99000000)";
}
```
注意,我们还需要额外为IE定义`background: transparent`,
我们可以通过条件注释来解决.

## 浏览器支持
支持RGBa的有:  
- firefox 3+  
- Safari 2+  
- Opera 10  
IE过滤器支持IE5.5及以上版本.

所以这种方式几乎支持了所有浏览器.

### 感谢
Thanks to [RGBa Browser Support](http://css-tricks.com/rgba-browser-support/) and 
[Bulletproof, cross-browser RGBA backgrounds, today](http://leaverou.me/2009/02/bulletproof-cross-browser-rgba-backgrounds/) 
for the information and inspiration.

Thanks to [Emil Stenström](http://friendlybit.com/) and [Pelle Wessman](http://kodfabrik.se/) 
for coming up with countless alternatives for hex conversion, and explaining basic math to stupid me. 

## 译者总结
大家使用时可直接复制下面代码:
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
最后来个效果图,顺便试试jsfiddle的嵌入:  
{% jsfiddle nMKGs result,html,css %}

