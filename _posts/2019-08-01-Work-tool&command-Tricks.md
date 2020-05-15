---
layout: post
title: Work tool and command tricks 1.0
---
Shell命令相关，python命令相关，pandas相关，git相关。
## Shell tricks

查找
```bash
grep '[symbols]' [file]
grep -h '[symbols]' [files] #多文件时不输出filename
```
计行数
```bash
wc -l
```
分割统计
```bash
awk -F "," '{print $1}' file.txt #用逗号分隔，第二个
awk -F "," '{ print $4 "\t" $5}' file.txt #用逗号分隔，第四个\t第五个
```

挂起job
```bash
nohup python test.py > log.txt & #挂起一个python job，并将stdout仅输出到log.txt中
```

分割文件
```bash
split -l 10000 file.txt #按行数分割，每10K行一个文件
split -b 500M file.txt #按size分割，每500M一个文件
```

字符串批量操作
```bash
sed -i "s/abcd/abce/g" *.txt # 将txt文件中的abcd替换为abce
```

## Python tricks

遍历目录下全部文件，处理后并重命名
```python
rawdir = '/path/to/dir'
for root,dirs,files in os.walk(rawdir):
    for f in files:
        source_file_path = os.path.join(root,f)
        target_file_path = source_file_path.replace('source','target')
        with open(source_file_path,'r') as fin:
            with open(target_file_path,'w') as fout:
                fout.write(func(fin))
```

Hash脱敏
```python
#default hash
hash(obj) # 输出为long，可以用hex()转换为十六进制str
#md5 hash
import hashlib
hashlib.md5(obj).hexdigest() #输出为str
```

URL decode
```python
#python2
import urllib
name = 'abcd' # make sure name is a str, not a unicode
name = urllib.unquote(name)
#python3
import urllib.parse
name = 'abcd'
name = urllib.parse.unquote(name)
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

同步master
```bash
git pull origin master
```

解决冲突
```bash
git mergetool
```

查看当前change
```bash
git diff
git diff [branch] #查看当前change与branch之间的diff
git diff [branch1] [branch2] #查看branch1与branch2之间的diff
```

查看commit的change
```bash
git show HEAD~0 #最新一个的diff
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