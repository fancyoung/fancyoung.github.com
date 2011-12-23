---
layout: post
title: "2012十大Web设计趋势"
date: 2011-12-15 15:03
comments: true
categories: [前端]
---
本不想取这么俗的标题, 
可原文正好推荐了10个.  
这回就不翻译原文, 
记点自己的看法.  

<!--more-->

#### 1. 响应式Web设计(Responsive Web Design)
简单的说就是动态适应当前各种分辨率及设备(电脑, Pad, 手机, ...)的页面方案.  
常用的有弹性布局. 另, "弹性图片"是个很有意思的东西.  
[什么是响应式Web设计？怎样进行？](http://beforweb.com/node/6)  
绝对是将来的方向, 
但考虑到技术和设计的实现复杂度, 
暂时还是用定宽网格吧.

#### 2. 固定导航条(Fixed-Position Navigation)
如果不是ie6不支持`position:fixed`,  
估计每个网站都会放几个固定元素.  
常见的有: 顶部导航条, 底部工具条, "回到顶部".

#### 3. 圆(Circles)
圆圆的东西总能戳中人们的萌点,  
比如: [columnfivemedia.com](http://columnfivemedia.com/)  
网站用了两种方式实现圆:  
顶部的两个圈圈用的是透明背景的png图,
中部并排的四个圈圈通过圆角实现
(只需将圆角设定大于宽/高的一半即可).  

这个网站有意思的还有将鼠标指到圈圈上时,图片会动起来.  
实现方法也非常简单,利用了CSS spirit.  
将一张静态图和一张动态图拼接成git图,
再通过CSS实现显示部分.  
(不用两张图是为了能同时加载, 以避免鼠标指上去时第二张图还没有加载.)
{% jsfiddle zr4ac result,html,css light 230px 420px %}

#### 4. 大矢量图(Big Vector Art)

#### 5. 多列菜单(Multi-Column Menus)

#### 6. jQuery/CSS3/HTML5动画(Animation)

#### 7. 缎带&横幅(Ribbons & Banner Graphics)
一秒钟网页立体化, 元素变卡片.  
可与固定位置配合使用(如:[RoR教程, 见右上角的"edge"](http://edgeguides.rubyonrails.org/getting_started.html)).  
你应该在某处已经看过了, 放几张图片例子:
[{% img http://www.webpagescreenshot.info/img/184189-1216201135658am.png %}](http://365psd.com/day/2-23/)
[{% img http://www.webpagescreenshot.info/img/491988-1216201135455am.png %}](http://365psd.com/day/2-183/)

#### 8. 自定义字体风格(Custom Font Faces)
这点就先不看了。人家只有26个字母，算上大小写也才52个。

#### 9. 信息可视化(Infographics)
没技术含量, 就不写了.
[数据之美：Infographics 终极探索](http://www.cnblogs.com/lhb25/archive/2011/03/19/1988526.html)
#### 10. 专注于简约(Focus on Simplicity)

#### 11. 视差滚动(Parallax Scrolling)
这个是我自己加的，因为实在太炫了。  
据说这是最经典的视差滚动：[Nike Better World](http://www.nikebetterworld.com/)  
每页都有很多创意元素：[某汽车网站](http://www.beetle.com/)  
从开发角度讲难度并不高，可能会有点点繁琐，  
我想它没排进前十的原因大约是对设计者要求太高。  
来份教程：[Behind The Scenes Of Nike Better World](http://coding.smashingmagazine.com/2011/07/12/behind-the-scenes-of-nike-better-world/)
## 参考
原文：[Web Design Trends in 2012](http://webdesignledger.com/tips/web-design-trends-in-2012)
