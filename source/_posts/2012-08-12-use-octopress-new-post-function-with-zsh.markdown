---
layout: post
title: "Octopress在zsh下无法新建博客的问题"
date: 2012-08-12 16:50
comments: true
categories: [Octopress, 问题解决, Ruby]
---
执行：`$ rake new_post["arch-linux-reinstall-glibc.markdown"]`

报错：`zsh: no matches found: new_post[arch-linux-reinstall-glibc]`

原因：zsh中若出现‘*’, ‘(’, ‘|’, ‘<’, ‘[’, or ‘?’符号，则将其识别为查找文件名的通配符

快速解决：用引号括起来`$ rake "new_post[arch-linux-reinstall-glibc.markdown]"`

彻底解决：取消zsh的通配(GLOB),
在`.zshrc`中加入`alias rake="noglob rake"`

* * *

PS：在git回滚操作`git reset --soft HEAD^`时出现报错：
`zsh: no matches found HEAD^`，

也为同样原因，因为`^`也为正则中的符号，
需要转义为`git reset --soft HEAD\^`。

## 参考
[Not compatible with Zsh](https://github.com/imathis/octopress/issues/117)
