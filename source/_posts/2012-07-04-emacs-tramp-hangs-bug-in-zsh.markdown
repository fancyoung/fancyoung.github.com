---
layout: post
title: "解决Emacs远程连接时卡住的bug"
date: 2012-07-04 00:14
comments: true
categories: [Emacs, 问题解决]
---

前几天终于买了Linode的VPS，配置过程中遇见一个灵异问题：  
Emacs无法远程SSH编辑文件，状态一直卡在`Tramp: Waiting for prompts from remote shell`。

折腾了好久，终于定位到zsh的配置oh-my-zsh上。  
最后查到原来Emacs Wiki上已经有解决方案，在`.zshrc`底部加上：
```
if [[ "$TERM" == "dumb" ]]
then
  unsetopt zle
  unsetopt prompt_cr
  unsetopt prompt_subst
  unfunction precmd
  unfunction preexec
  PS1='$ '
fi
```

参考：[TrampMode Troubleshooting](http://emacswiki.org/emacs/TrampMode#toc6)
