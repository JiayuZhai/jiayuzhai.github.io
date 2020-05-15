---
layout: post
title: Regex frequently used sheet
---
关于正则表达式cheatsheet。

## BRE

纯文本
```shell
test
```

特殊字符
```shell
\. \* \[ \] \^ \$ \{ \} \\ \+ \? \| \( \) \/# .*[]^${}\+?|() 
```

锚字符
```shell
^test$ #行首行尾
```

点字符
```shell
t.st # test 
t.st # tst (x) 
```

字符组
```shell
[012abc] #包含
[^012abc] #排除
```

区间
```shell
[0-9a-zA-Z]
```

特殊字符组
```shell
[[:alpha:]] # 任意字母
[[:alnum:]] # 任意字母数字
[[:blank:]] # 任意空格或制表符
[[:digit:]] # 任意0-9数字
[[:lower:]] # 任意小写字母
[[:print:]] # 任意可打印字符
[[:punct:]] # 任意标点
[[:space:]] # 任意空白字符
[[:upper:]] # 任意大写字母
```

星号
```shell
te*st # test; tst; teeeeest 零次或多次
```
## ERE
问号
```shell
te?st # test; tst; 零次或一次
```

加号
```shell
te+st # test; teeeeest; 一次或多次
```

花括号
```shell
te{1,2}st #指定出现次数
```

管道符号（逻辑或）
```shell
test|trial #逻辑或
```

表达式分组
```shell
(test)? # test 出现零次或一次
(c|b)a(b|t) #cab;cat;bab;bat
```

## 应用
中国手机号
```shell
^1([358][0-9]|4[579]|66|7[0135678]|9[89])[0-9]{8}$
```
邮箱
```shell
^([a-zA-Z0-9_\-\.\+]+)@([a-zA-Z0-9_\-\.]+)\.([a-zA-Z]){2,5}$
```
含中文邮箱
```shell
^([a-zA-Z0-9\u4e00-\u9fa5_\-\.\+]+)@([a-zA-Z0-9_\-\.]+)\.([a-zA-Z]){2,5}$
```
