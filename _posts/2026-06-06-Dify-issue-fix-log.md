---
layout: post
title: Dify Issue Fix Log on 2026-06-05
---

2026.06.05 晚
操作
1. docker build部署应用，导致服务器OOM，卡死。重启服务器。

问题
1. 重启后发现Dify无法访问，容器组里许多容器在不停重启。

解决方法
1. 首先从log中发现，基本都指向db容器无法访问。检查db容器log，发现问题log
    ```
    PostgreSQL Database directory appears to contain a database; Skipping initialization

    2026-06-05 17:18:07.068 UTC [1] LOG:  starting PostgreSQL 15.14 on x86_64-pc-linux-musl, compiled by gcc (Alpine 14.2.0) 14.2.0, 64-bit
    2026-06-05 17:18:07.071 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
    2026-06-05 17:18:07.071 UTC [1] LOG:  listening on IPv6 address "::", port 5432
    2026-06-05 17:18:07.076 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
    2026-06-05 17:18:07.081 UTC [29] LOG:  database system was shut down at 2026-06-05 16:35:18 UTC
    2026-06-05 17:18:07.081 UTC [29] LOG:  invalid primary checkpoint record
    2026-06-05 17:18:07.082 UTC [29] PANIC:  could not locate a valid checkpoint record
    2026-06-05 17:18:07.741 UTC [1] LOG:  startup process (PID 29) was terminated by signal 6: Aborted
    2026-06-05 17:18:07.741 UTC [1] LOG:  aborting startup due to startup process failure
    2026-06-05 17:18:07.742 UTC [1] LOG:  database system is shut down
    ```
2. 应该是服务器重启，导致postgres的数据损坏，找解决办法
    1. `docker run --rm -it --volumes-from 【容器名】 postgres:15-alpine bash` 新起一个新容器，用相同的volume
    2. `su postgres`
    3. `pg_resetwal -f /var/lib/postgresql/data/pgdata`
    4. 看到：`Write-ahead log reset`
    5. exit退出容器
    6. 重启postgres容器
3. 但是修复后仍不正常，表现为db服务一直unhealthy。而且服务器存在两个db服务，docker-db-1和docker-db-postgres-1。初步认为是在几个月前升级dify版本的时候留了东西下来。
4. docker-compose down下掉所有容器，但db容器都没有停掉。
5. 重启db容器发现network不存在了，但是前面docker-compose down把network删掉了。
6. 重新docker compose up -d 启动所有容器和网络，重新连回两个db的network到docker-default。仍unhealthy。
7. exec进db容器，检查healthy api，发现无问题。
8. 其他容器报错network issue找不到db服务。
9. 没有其他思路，最终决定手动删掉db容器，然后docker compose up -d 重新启动，结果重启的容器中没有db容器。
10. 检查.env和.env.example，发现不一致。初步认为是在几个月前升级dify版本的时候留了东西下来。.env用的旧版本中没有db服务。在用新版docker-compose.yaml down掉容器时，未down掉旧的db容器。歪打正着保留了db容器，让dify服务正常工作。
11. 备份.env和volume文件夹，用.env.example重做.env。在彻底删掉旧容器后，重新启动所有容器，db容器正常启动，并healthy了。
12. 但是dify前端无法用admin账号登陆，提示用户名或密码错误。
13. 检查db中数据，发现数据比较旧。有些近几天的改动不见了，比如api-key不见了。而且没有找到我的admin账号。
14. 无法找回密码，因为数据不存在，这个账号被认为不存在。
15. 借用其他账号，用api修改密码 `docker exec -it docker-api-1 flask reset-password`
16. 登陆并给自己的原来账号发邀请。
17. 发现密码重试错误过多，被锁了。
18. 去redis清楚锁定状态 `docker exec -it docker-redis-1 redis-cli` `DEL login_error_rate_limit:admin@dify.com`
19. 重启登陆成功。发现数据丢了一些，比如workflow log和workflow-api-key。但是最重要的新的worflow还在，虽然第一次登陆进去发现工作流为空，但是从已发布中发现了草稿，重新发布。生成新的api-key，替换应用中的api-key。
20. 检查应用是否正常，发现正常。


教训
1. 定期备份.env和volume文件夹，还有最重要的工作流DSL文件，避免数据丢失。
2. 升级dify版本，要完全按照官方文档操作，避免留下的东西。
3. 检查任何不对的地方，提前发现问题。

于 唐山 2026.06.06 晚
