---
layout: post
title: "Blueprint教程"
date: 2011-11-17 13:15
comments: true
categories: "前端"
---
（本文为官网教程翻译）
Blueprint是个好框架，本教程会深入介绍你可以用它来做什么，也会说到什么时候不适合用。

## Blueprint简介
Blueprint是一个CSS框架，为减少开发时间而设计。它可以构架起有坚实基础的CSS，其中包含合理的排版（typography）、可定制的网格(grid)、打印样式等。

但是Blueprint不是银弹，它适用于每个页面都需要独特的设计。在决定使用Blueprint前建议先看看Blueprint例子以决定是否适合你。你可以检出```tests```目录，里面例子展示大部分Blueprint样式。

“框架”这个词也许有些误导，Blueprint并不会建议你如何组织你的CSS文件。它更像一个工具箱，你可以从中选出你需要的。

## 结构概述
自下而上的看Blueprint：

CSS布局：
CSS reset: 移除浏览器的默认规则。
Typography: 默认提供一些漂亮的排版和颜色。
Grid: 提供一组样式来制作网格。

第二部分是脚本。你可以它来自定义框架，可以是列数、宽度等外观，还可以是路径、命名空间等。我们有两个脚本：
1. Compressor: 用于压缩和自定义源文件。
2. Validator: 用于验证Blueprint核心文件。

以上是简单介绍，接下来让我们进入细节。首先，我们看看CSS部分。然后我们再介绍脚本，以及如何通过它数和自定制框架。

## 设置Blueprint
为了使用Blueprint，你必须包含以下三个文件在你的HTML中：

- ```blueprint/screen.css```: 主要文件，页面展示的样式都在里面。
- ```blueprint/print.css```: 用于打印。
- ```blueprint/ie.css```: 用于IE浏览器下的校正。

在HTML中嵌入下面代码来引用（请确认路径正确）：
```
<link rel="stylesheet" href="css/blueprint/screen.css" type="text/css" media="screen, projection" />
<link rel="stylesheet" href="css/blueprint/print.css" type="text/css" media="print" /> 
<!--[if lt IE 8]>
  <link rel="stylesheet" href="css/blueprint/ie.css" type="text/css" media="screen, projection" />
<![endif]-->
```
（原文提示XHTML需要用"/>"结束标签，上面代码中我已经直接加上了）

## 使用Blueprint里的CSS
之前已经提过，Blueprint有三个布局，前两个布局，CSS reset和默认排版用于设置默认HTML样式。所以你不需要更改这两个文件。如果你想更改全局字体大小等，建议你写在自己的CSS文件里，以便将来更新Blueprint版本。

#### 排版相关class
While the typography of Blueprint mainly applies itself, there’s a few classes
provided. 下面是一个它们名字的列表和介绍它们的作用:


`.hide`  
隐藏元素

`.quiet`  
使字体颜色柔和

`.loud`  
黑色字体

`highlight`  
黄色背景

`.added`  
绿色背景

`.removed`  
红色背景

`.first`  
移除左侧margin/padding

`.last`  
移除右侧margin/padding

`.top`  
移除顶部margin/padding

`.bottom`  
移除底部margin/padding

#### 表格样式
Blueprint可以通过给输入元素加`.text`, `.title`类来控制，其中`.text`表示普通大小，`.title`提供一个大字体的输入框。

这里还有一些类可以用于成功或失败信息：

`div.error`  
建议一个失败框（红色）。

`div.notice`  
建议一个提示框（黄色）。

`div.success`  
建议一个成功框（绿色）。

#### 建立网格


## 参考
[Blueprint CSS Framework Tutorial(官方原文)](https://github.com/joshuaclayton/blueprint-css/wiki/Quick-start-tutorial)  
[官网](http://blueprintcss.org/)  
[Demo](http://blueprintcss.org/tests/)  
