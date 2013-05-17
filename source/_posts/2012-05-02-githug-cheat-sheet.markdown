---
layout: post
title: "Githug通关全攻略"
date: 2012-05-02 12:49
comments: true
categories: [Github]
---
[Githug](https://github.com/Gazler/githug)将git的入门与游戏相结合，太有意思了。  
游戏过程中少不了网上查找资料，man，难度4以后不停的hint。  
通关后对git的了解又加深了许多。  
取连接名时很是矛盾，写完博客后还是将链接中的walkthrough改为了cheat sheet。  
希望大家不需要使用到这篇博客吧。

因关卡随时处于更新状态，可能会稍有不同  
<del>- 最后更新时间2012-11-14</del>  
- 最后更新时间2013-05-17  

## 准备
安装Githug：`$ gem install githug`。  
安装完成后直接执行`$ githug`开始游戏，同一条命令进入下一关。  
`$ githug hint`查看过关提示，  
当操作错误无法过关时，可以`$ githug reset`重置当前关卡。

## 开始
#### 0
```
y
```
#### 1 初始化git项目
```
$ cd git_hug
$ git init
```
#### 2 stage一个文件
```
$ git add README
```
#### 3 提交已stage的文件
```
$ git commit -m '-'
```

<!--more-->

#### 4 配置git用户信息
```
$ git config user.name xxx
$ git config user.email xxx@gmail.com
```
或者直接在`.git/config`文件里添加
```
[user]
        name = xxx
        email = xxx@gmail.com
```
回答时分别输入`xxx`和`xxx@gmail.com`  
- 扩展  
使用`--global`参数修改本机全局设置
```
$ git config --global user.name = xxx
```
- 问题  
命令行里不要带等号`$ git config user.name = xxx`,
否则去文件里查时会发现等号变成值`name = =`。
(之前好像可以用的？待解决)

#### 5 检出一个已有项目
```
$ git clone https://github.com/Gazler/cloneme
```
#### 6 检出项目并重命名
```
$ git clone https://github.com/Gazler/cloneme my_cloned_repo
```
#### 7 配置忽略文件规则
在`.gitignore`文件里添加
```
*.swp
```
#### 8 查看状态
`$ git status`查看，
得到答案为`database.yml`
#### 9 删除文件
`$ git status`查看，发现被删文件名为`deleteme.rb`
```
$ git rm deleteme.rb
```
#### 10 将文件移出git但不删除文件
```
$ git rm --cached deleteme.rb
```
#### 11 保存项目当前状态但不提交（新，实用）
```
$ git stash
```
#### 12 重命名文件
```
$ git mv oldfile.txt newfile.txt
```
#### 13 查看提交历史
`$ git log`查看提交历史记录，答案为commit后长字符串的前7位
#### 14 tag
```
$ git tag 'new_tag'
```
#### 15 将新修改并入上一次提交
```
$ git add forgotten_file.rb
$ git commit --amend
```
写完注释后保存退出（vi是`:qw`，应该都会吧）
#### 16 unstage一个文件
```
$ git reset HEAD to_commit_second.rb
```
#### 17 取消上一次提交
```
$ git reset --soft HEAD^
```
#### 18 恢复文件修改
```
$ git checkout config.rb
```
#### 19 查看remote信息
`$ tail .git/config`查看remote信息，
答案为`my_remote_repo`
#### 20 查看remote链接
同上，答案为`https://github.com/githug/not_a_repo`
#### 21 pull
```
$ git pull origin master
```
#### 22 关联远程库(新项目必备)
```
$ git remote add origin https://github.com/githug/githug
```
#### 23 合并：rebase(与merge做对比)
```
$ git rebase origin/master
$ git push
```
#### 24 查看变动
通过`$ git diff app.rb`查看文件改动，  
显示行号为23，改动在下面第3行，所以答案为`26`。
#### 25 跟踪具体代码行作者
`$ git blame config.rb`查看修改记录，发现密码出现在第五行。
在这行的左边可以看到提交者为`Spider Man`（卖萌了）。
#### 26 新建分支
```
$ git branch test_code
```
#### 27 新建并进入分支
```
$ git checkout -b my_branch
```
#### 28 按标签检出
```
$ git checkout v1.2
```
#### 29 按版本编号检出至新分支
查看提交历史，找到第二条的id，输入时只需要输入前几位即可
```
$ git branch test_branch -v 7cd3aa021
```
#### 30 合并分支
```
$ git merge feature
```
#### 31 仅从分支合并指定提交
`$ git branch`查看分支列表，得到分支名。  
`$ git log new-feature`查看分支提交记录。
最后合并：
```
$ git cherry-pick ca32a6da
```
#### 32 修改历史提交日志
查看历史记录，发现错误在倒数第二次提交上
```
$ git rebase -i HEAD~2
```
进入编辑页面，将需要改动的行（第一行）的`pick`改为`reword`
（注意，只需要通过`reword`来标记，不要修改拼写）。
保存退出后在弹出的第二个窗口里修改拼写错误`commmit`改为`commit`。
#### 33 合并历史提交（清洁日志）
查看历史记录发现最后3次都为同一个文件的修改，可以合并
```
$ git rebase -i HEAD~3
```
将弹出编辑页的第2、3行的`pick`改为`squash`，
第二个弹出页直接保存退出即可。
#### 34 从分支合并时仅保存为一次提交
```
$ git merge --squash long-feature-branch
$ git commit -a -m 'merge branch long-feature-branch'
```
#### 35 更改历史提交顺序
查看历史记录发现最后两次提交顺序错误
```
$ git rebase -i HEAD~2
```
然后在弹出编辑页的前两行顺序调换。
#### 36 二叉树排错（很强大，侧面看出测试驱动重要性）
`$ git log --reverse -p prog.rb`查看最初一次为正确提交，版本号为`f608824888`
```
$ git bisect start
$ git bisect good f608824888
$ git bisect bad
$ git bisect run make test
//$ git reset
```
日志里`…… is the first bad commit`
所以回答`18ed2ac`
#### 37 仅stage一个文件的一部分
查看文件可知需要stage的是第二行（...the first feature）。
```
$ git add -p feature.rb
```
出现提示如何处理，输入`e`来编辑提交内容，  
在弹出编辑页面删除第5行（...the first feature），
因为不在本次stage操作内，保存退出。

#### 38 查看操作历史
```
$ git reflog
```
查看到日志第2行`...checkout: moving from solve_world_hunger to kill_the_batman...`
```
$ git checkout solve_world_hunger
```
#### 39 回滚某次提交历史
查看历史记录，发现倒数第二次提交需要取消
```
$ git revert HEAD~1
```
直接保存并退出
#### 40 通过操作日志，挽救`git reset --hard HEAD^`的误操作
`$ git reflog`查看日志，发现需要回覆至版本`804db65`(每次版本号可能不同)。
```
$ git checkout 804db65
```
#### 41 合并分支并处理冲突
```
$ git merge mybranch
```
编辑`poem.txt`文件，处理冲突
```
$ git add poem.txt
$ git ci -m 'merge mybranch`
```
#### 41
最后一关！！！
内容是什么，就留点悬念吧:)
