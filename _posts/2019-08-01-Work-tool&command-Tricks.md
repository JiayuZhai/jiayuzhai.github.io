---
layout: post
title: Work tool and command tricks
---

## Shell tricks

查找
```bash
grep '[symbols]' [file]
```
计行数
```bash
wc -l
```

## Pandas tricks

类别统计个数
```python
df['col'].value_counts()
```

## Git tricks

查看branch
```bash
git branch
```

切换branch
```bash
git checkout [branch]
```

创建branch
```bash
git checkout [branch] #切换到要创建的branch的父节点
git checkout -b [new branch]
```

删除 local branch
```bash
git checkout [other branch]
git branch -d [branch]
```

删除远程branch
```bash
git push origin --delete [branch]
```

推local branch到远程
```bash
git push --set-upstream origin [branch]
```

压缩commit
```bash
git rebase -i HEAD~n #n is the last n commits to compress
#然后把除latest的commit pick -> squash
#保存退出
```

解决冲突
```bash
git mergetool
```

land code流程
```bash
# Start a new change set.  Should branch from master HEAD.
$ git checkout master
$ git pull
$ git checkout -b <branch-name>

# Edit and commit your change to your local git.
$ git add <files you want to commit>
$ git commit # Important: DO NOT include "--amend" for the first time.

# More edit and commit.  Subsequent commits SHOULD use "--amend"
# to merge all your changes into one atomic commit.
$ git add <files you want to commit>
$ git commit --amend

# When ready, send for code review.  Run git pull to update your code to HEAD.
# --rebase means to apply your change on top of HEAD.
# Add the reviewer github name (e.g. "yanghuachu") under reviewers
# Add "datavisor-fte" under subscribers (to cc everyone) if needed.
$ git pull --rebase origin master
# After you resolve the conflicts (if any), you are ready to send to our diff server.
$ arc diff
```