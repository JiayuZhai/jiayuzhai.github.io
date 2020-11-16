---
layout: post
title: HBase shell basic usage command
---

HBase shell: CLI for HBase

## 基本操作

status
version
table_help
whiami

## table操作

create
```
create <table_name>, <columnfamilyname>
```
list
```
list
```
describe
```
describe <table name>
```
disable
```
disable <tablename>
```
disable_all
```
disable_all<"matching regex"
```
enable
```
enable <tablename>
```
show_filters
```
show_filters
```
drop
```
drop <table name>
```
drop_all
```
drop_all<"regex">
```
is_enabled
```
is_enabled 'education'
```
alter
```
alter <tablename>, NAME=><column familyname>, VERSIONS=>5
```
alter_status
```
alter_status 'education'
```

## data操作
count
```
count <'tablename'>, CACHE =>1000
```
put
```
put <'tablename'>,<'rowname'>,<'columnvalue'>,<'value'>
```
get
```
get <'tablename'>, <'rowname'>, {< Additional parameters>}
```
delete
```
delete <'tablename'>,<'row name'>,<'column name'>
```
deleteall
```
deleteall <'tablename'>, <'rowname'>
```
truncate
```
truncate <tablename>
```
scan
```
scan <'tablename'>, {Optional parameters}
```
