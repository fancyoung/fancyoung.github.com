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
第三个布局是网格，是一个给你网站建立各样网格的工具。记住网格背后的大部分CSS都可以自定义（下面会讲到）。在这个部分我会使用默认设置。

默认网格有24列，每列宽30px，边距(margin)10px。总共宽为950px，适合1024x768的分辨率。如果你想要更窄的设计，可以看下面自定义网格一节。

怎么用Blueprint来建立网格呢？新建一个`<div/>`来代表一列，并且给它加一个`.span-x`的class。比如，如果你想要一个三列的布局，两窄一宽，并且包含头尾，可以参考下面的代码:
```
<div class="container">
  <div class="span-24">
    头部
  </div>

  <div class="span-4">
    第一列
  </div>
  <div class="span-16">
    中间列
  </div>
  <div class="span-4 last">
    最后一列
  </div>
 
  <div class="span-24">
    尾部
  </div>
</div>
```
此外，还有两个class你应该知道。首先，每个Blueprint页面应该包含在一个class为`.container`的div里，一般紧跟在body标签后。

第二，每行的最后一列（默认24列），应该用class`.last`来移除右侧的边距(margin)。可以参考`tests/parts/`里的例子。这些文件告诉了你Blueprint的网格能做些什么。

这里是一个其他网格相关class的快速概述：  
`.append-x`
附加（在后面加）x条空列。  
`.prepend-x`
追加（在前面）x条空列。  
`.push-x`
推送x列到左侧。可用于切换列。  
`.pull-x`
推送x列到右侧。可用于切换列。  
`.border`
列右侧加分界线。  
`.colborder`
建立新列，分界线在中部。  
`.clear`
换行，无论是否有空。  
`.showgrid`
给容器或列添加后能看见网格和基线。 

在这个列表中，`x`用于append/prepend时范围是1-23，用于push/pull时是1-24。如果你自定义了新的列数，这个范围会随之变化。

下面是另一个例子，包含4列等宽，前两列间有分界线，后两列间也有，4列的中间有段空白。
```
<div class="container">
  <div class="span-5 border">
    第一列
  </div>
  <div class="span-5 append-4">
    第二列
  </div>
  <div class="span-5 border">
    第三列
  </div>
  <div class="span-5 last">
    第四列
  </div>
</div>
```

你也可以通过嵌套列来实现想要的布局。下面例子展现的是页面左半部有四个长方形，两上两下，右半部有一个长方形。
```
<div class="container">
  <div class="span-12">
    <div class="span-6">
      左上
    </div>
    <div class="span-6 last">
      右上
    </div>
    <div class="span-6">
      左下
    </div>
    <div class="span-6 last">
      右下
    </div>
  </div>
  <div class="span-12 last">
    另一块
  </div>
</div>
```
如果不理解可以在浏览器里尝试上面的代码。想看更过的如何使用class的例子，请看`/tests/parts/grid.html`。

## 脚本
Blueprint有两个脚本：一个用于压缩和自定义CSS，另一个是验证核心CSS文件，以免你修改了某些文件。

#### 验证器(The Validator)
验证器的工作很简单——检查Blueprint核心CSS里的文件。脚本使用配套版本的W3C CSS验证器来完成。为了运行，你需要安装Ruby。然后你可以运行`$ ruby validate.rb`。

请注意Blueprint有几个验证错误。它们是已知的，来自于几个为了保持浏览器一致性的CSS hack。

#### 压缩器(The Compressor)
你的HTML里引用压缩版的核心CSS文件时，当你做过修改，需要重新压缩。这是压缩器脚本的作用。

另外，你可以在这里自定义网格。为了自定义网格，需要使用一个特殊的设置文件，当你运行压缩器时，就会生成新的CSS。新压缩的文件将会使用你的设置。

你之需要重新运行脚本来重新压缩。这会解析核心CSS文件并在blueprint文件夹里生成新文件。与验证器一样，需要安装Ruby。在`lib`目录里执行`$ ruby compress.rb`。

执行这个文件会将`blueprint/src`下的文件合并成三个文件：`ie.css`, `print.css`, `screen.css`。  
但是你可以通过加参数来改变行为。执行`$ ruby compress.rb -h`查看你可以使用的基本参数。

#### 自定义设置
你可以阅读`lib/compress.rb`里的文档来学习如何自定义设置。

## 参考
[Blueprint CSS Framework Tutorial(官方原文)](https://github.com/joshuaclayton/blueprint-css/wiki/Quick-start-tutorial)  
[官网](http://blueprintcss.org/)  
[Demo](http://blueprintcss.org/tests/)  
