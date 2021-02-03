---
layout: post
title: Every command i need to search many times
---

总是记不住的命令

## SQL
```sql
# 更新
update table set columnA='' where condition;
# 插入
insert into table (columnA, columnB) values (valueA, valueB)
```

## timestamp

时间戳转时间字符串
```python
import datetime
datetime.datetime.fromtimestamp(second_timestamp).strftime('%Y-%m-%d %H:%M:%S')
```

时间字符串转时间戳
```python
import datetime
datetime.datetime.strptime('20210104_235959','%Y%m%d_%H%M%S').timestamp()
```
