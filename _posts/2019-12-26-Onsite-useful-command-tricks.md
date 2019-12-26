---
layout: post
title: Onsite useful command tricks
---

## Docker

进入容器的bash
```bash
docker exec -it container bash
```

容器copy
```bash
docker cp local_file.txt hdfs-nn1:/mnt/client/upload/
docker cp hdfs-nn1:/mnt/client/upload/local_file.txt .
```

## HDFS
```bash
hadoop fs -ls /path/of/hdfs/file
hadoop fs -get /path/of/hdfs/file .
hadoop fs -put local_file.txt /path/of/hdfs/
hadoop fs -getmerge /path/of/hdfs/hadoop-file merged.json
hadoop fs -cp /path/of/source /path/of/target
hadoop fs -mv /path/of/source /path/of/target
hadoop fs -get -f /path/of/hdfs/file . # 强制覆盖
hadoop fs -put -f local_file.txt /path/of/hdfs/ # 强制覆盖
hadoop fs -rm /path/of/hdfs/file
hadoop fs -rm -r /path/of/hdfs/dir
```

## System

系统检查，进程检查
```bash
du -sh #检查文件大小
df -h #检查磁盘大小和占用情况
ls -ltr #按时间倒序
ps -ef #全部进程
ps -ef | grep name #包含关键词的进程
kill id #杀死进程
```

脚本锁
```bash
if [[ ! -f script_lock ]]; then
	touch .script_lock

	do_script

	rm .script_lock
else
	echo 'locking'
fi
```

## cron job
[Index](https://crontab.guru/)

[Examples](https://crontab.guru/examples.html)
