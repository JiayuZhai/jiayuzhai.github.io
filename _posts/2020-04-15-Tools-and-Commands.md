---
layout: post
title: Work tool and command tricks 3.0
---

开源项目工具的介绍和docker相关命令。

## Tools
Kafka: 消息队列中间件，分布式架构，通过topic进行消息的生产和消费

Prometheus: 通过定义metric，来进行监控和发送告警的监控告警系统

Grafana: 监控界面，可以自定义监控项

F5: 硬件/虚拟硬件负载均衡

Spark streaming: 微批计算实现的流式计算

Flink: 实时的流式计算

## Commands
Docker外直接运行bash命令
```bash
docker exec container bash -c "hadoop fs -ls /path/of/a/file"
```

Mysql docker外直接运行bash命令
```bash
docker exec container bash -c "mysql -uuser -ppassword -e \"use db;select * from some_tables;\""
```
