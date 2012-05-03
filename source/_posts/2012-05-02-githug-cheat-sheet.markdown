---
layout: post
title: "Githug通关全攻略"
date: 2012-05-02 12:49
comments: true
categories: 
---
[Githug](https://github.com/Gazler/githug)将git的入门与游戏相结合，太有意思了。  
游戏过程中少不了网上查找资料，man，难度4以后不停的hint。  
通关后对git的了解又加深了许多。  
取连接名时很是矛盾，写完博客后还是将链接中的walkthrough改为了cheat sheet。  
希望大家不需要使用到这篇博客吧。

## 准备
安装Githug：`$ gem install githug`。  
安装完成后直接执行`$ githug`开始游戏，同一条命令进入下一关。  
`$ github hint`查看过关提示，  
当操作错误无法过关时，可以`$ github reset`重置当前关卡。

## 开始
#### 0
```
y
```
#### 1
```
$ cd git_hug
$ git init
```
#### 2
```
$ touch README
$ git add README
```
#### 3
```
$ git ci -m '-'
```
#### 4
在`.git/config`文件里添加
```
[user]
        name = xxx
        email = xxx@gmail.com
```
回答时分别输入`xxx`和`xxx@gmail.com`
#### 5
```
$ git clone https://github.com/Gazler/cloneme
```
#### 6
```
$ git clone https://github.com/Gazler/cloneme my_cloned_repo
```
#### 7
在`.gitignore`文件里添加
```
*.swp
```
#### 8
`$ git st`查看，
得到答案为`database.yml`
#### 9
`$ git st`查看，发现被删文件名为`deleteme.rb`
```
$ git rm deleteme.rb
```
#### 10
```
$ git rm --cached deleteme.rb
```
#### 11
```
$ git mv oldfile.txt newfile.txt
```
#### 12
`$ git log`查看提交历史记录，答案为commit后长字符串的前7位
#### 13
```
$ git tag 'new_tag'
```
#### 14
```
$ git add forgotten_file.rb
$ git commit --amend
```
写完注释后保存退出（vi是`:qw`，应该都会吧）
#### 15
```
$ git reset HEAD to_commit_second.rb
```
#### 16
```
$ git checkout config.rb
```
#### 17
`$ tail .git/config`查看remote信息，
答案为`my_remote_repo`
#### 18
同上，答案为`https://github.com/githug/not_a_repo`
#### 19
```
$ git pull origin master
```
#### 20
```
$ git remote add origin https://github.com/githug/githug
```
#### 21
通过`$ git diff app.rb`查看文件改动，  
显示行号为23，改动在下面第3行，所以答案为`26`。
#### 22
`$ git blame config.rb`查看修改记录，发现密码出现在第五次提交。
在这行的左边可以看到答案为`Spider Man`（卖萌了）。
#### 23
```
$ git branch test_code
```
#### 24
```
$ git checkout -b my_branch
```
#### 25
查看提交历史，找到第二条的id，输入时只需要输入前几位即可
```
$ git branch test_branch -v 7cd3aa021
```
#### 26
```
$ git merge feature
```
#### 27
`$ git branch`查看分支列表，得到分支名。  
`$ git log new-feature`查看分支提交记录。
最后合并：
```
$ git cherry-pick ca32a6da
```
这个应该不是最优解。
#### 28
查看历史记录，发现错误在倒数第二次提交上
```
$ git rebase -i HEAD~2
```
进入编辑页面，将需要改动的行（第一行）的`pick`改为`reword`
（注意，只需要通过`reword`来标记，不要修改拼写）。
保存退出后在弹出的第二个窗口里修改拼写错误`commmit`改为`commit`。
#### 29
查看历史记录发现最后3次都为同一个文件的修改，可以合并
```
$ git rebase -i HEAD~3
```
将弹出编辑页的第2、3行的`pick`改为`squash`，
第二个弹出页直接保存退出即可。
#### 30
```
$ git merge --squash long-feature-branch
$ git commit -a -m 'merge branch long-feature-branch'
```
#### 31
查看历史记录发现最后两次提交顺序错误
```
$ git rebase -i HEAD~2
```
将弹出编辑页的前两行顺序调换。
#### 32
查看文件可知需要stage的是第二行（...the first feature）。
```
$ git add -p feature.rb
```
出现提示如何处理，输入`e`来编辑提交内容，  
在弹出编辑页面删除第5行（...the first feature），
因为不在本次stage操作内，保存退出。

#### 33
```
$ git reflog
```
查看到日志`...checkout: moving from solve_world_hunger to kill_the_batman...`
```
$ git checkout solve_world_hunger
```
#### 34
查看历史记录，发现倒数第二次提交需要取消
```
$ git revert HEAD~1
```
直接保存并退出
#### 35
最后一关！！！
内容是什么，就留点悬念吧:)
