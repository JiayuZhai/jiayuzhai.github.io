---
layout: post
title: Excel Tricks
---

## Convert long Column to Date Column
```python
=TEXT((LEFT(B1,10)+8*3600)/86400+70*365+19,"yyyy-MM-DD HH:mm:ss")&" "&RIGHT(B1,3)
# 前十位是秒数，8*3600是GMT+8时差，86400是转date，70*365是excel的计时起点为1900年，+19是1900-1970的19个闰年，后三位为毫秒数
```
