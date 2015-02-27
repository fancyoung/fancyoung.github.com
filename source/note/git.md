---
layout: page
title: "Git/Hg常见操作"
date: 2015-01-01 19:00
comments: true
sharing: true
footer: true
---
## git
对比stage的文件
`$ git diff --cached`

修改最后一次提交
`$ git commit --amend`

取消上一次的提交(未push前)
`$ git  reset --soft HEAD^`

恢复所有被修改的文件
`$ git checkout -f`

将文件移出版本管理，但不删除
`$ git rm --cached $file`

提交时显示修改记录(之前都是`$ git diff --cached` + `$ git ci -m`)
`$ git ci -v`

还原曾经被删除的文件
`git checkout $(git rev-list -n 1 HEAD -- "$file")^ -- "$file"`
http://stackoverflow.com/questions/953481/restore-a-deleted-file-in-a-git-repo

忽略mode权限(chmod)  
配置：`core.fileMode=false`， 如`git -c core.fileMode=false diff`
http://stackoverflow.com/questions/1580596/how-do-i-make-git-ignore-file-mode-chmod-changes

#### 查看历史 [详细](http://git-scm.com/book/zh/Git-%E5%9F%BA%E7%A1%80-%E6%9F%A5%E7%9C%8B%E6%8F%90%E4%BA%A4%E5%8E%86%E5%8F%B2)
限制历史条数
`$ git log -n 3`或`$ git log -3`

显示具体变动
`$ git log -p`

显示变动文件列表
`$ git log --name-only`,
`$ git log --name-only -1`,
`$ git log --name-only --oneline`

显示最近2次的具体变动
`$ git log -p -2`

简要显示增改行数统计
`$ git log --stat`

格式化输出
`$ git log --pretty=oneline` 
(可以为`oneline`, `short`, `full`, `fuller`, 或者自定制, 如`format:"%h - %an, %ar : %s"`)

过滤条件
`--graph`
`--since/after`/`--until/before`
`--author`
`--committer`
`--grep`
`--all-match`

#### 其他
连子模块一起更新
`$ git pull --recurse-submodules` (v1.7.3+)

放弃本地修改提交，强制与服务器同步
`$ git fetch origin`
`$ git reset --hard origin/master`

## hg
#### 查看历史
限制历史条数
`$ hg log -l 3`

显示修改文件
`$ hg log -v`

显示具体变动
`$ hg log -p`

查看具体版本
`$ hg log -r 652`
`$ hg log -r a7b97cdfac3c`
`$ hg log -r 652:654`
`$ hg log -r 650 -r 654`
