---
layout: post
title: Mixed Content Fix Log on 2026-06-18
---

2026.06.18 晚
问题
1. 部署新应用，发现前端call后端API时报错Mixed Content。一个本来应该call https的接口，报错call了http。

解决方法
1. AI问诊，但是不断说是前端拼错了，要么是给nginx config加一堆配置项，但是改了半天还是不对。
2. 同时前端call其他api没有问题，就是一个list task的API会报这个错。
3. 检查和回顾架构。
    1. 单机docker部署。一个server-gateway做应用转发，其中这个应用转发到它的前端容器。
    2. 前端容器对/api/的请求转发到后端容器。
4. 对于报错的API，server-gateway收到请求，转到前端容器正常。
5. 前端容器中日志发现出现三次api，第一次是完整api，比如https://example.com/api/tasks?params，状态308；第二次是被去掉了/api的url，比如https://example.com/tasks?params，状态301；第三次是被去掉了/api和params的url，比如https://example.com/tasks，状态404。
6. 后端容器中日志发现，收到一条请求是/tasks?params，状态308。应该对应的是前端容器第一次。
7. 发现该API定义用的route是'/'，而buleprint本身是‘/tasks’，又因为Flask的**strict_slashes**，导致了https://example.com/api/tasks?params 被后端认为需要redirect（状态308），但是后端触发的redirect缺少了url的部分信息（/api/），因为被前端容器的nginx中转了一次。
8. 修改后端容器API，一致禁止直接用'/'，而是'/list'的方式，比如https://example.com/api/tasks/list?params。问题解决。

教训
1. Vibe coding的时候，后端这里注意太少，之前项目都是没有直接'/'这样用route的，应该把这个policy记录下来。
2. 应尽早检查容器日志来对nginx转发进行调试。早期以来AI自己修复问题，搞了太多轮都搞不定。

于 唐山 2026.06.18 晚
