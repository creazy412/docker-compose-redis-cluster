# docker-compose&手动操作redis-cluster
### 搭建集群

介绍完 Redis 集群分区规则之后，下面我们开始搭建 Redis 集群。搭建集群工作需要以下三个步骤：
1）准备节点。
2）节点握手。
3）分配槽。

节点规划
容器名称 | 容器 IP 地址 | 映射端口号 | 服务运行模式
---|---|---|---
redis-master1 | 172.50.0.2 | 6391->6391 | master
redis-master2 | 172.50.0.3 | 6392->6392 | master
redis-master3 | 172.50.0.4 | 6393->6393 | master
redis-slave1 | 172.30.0.2 | 6394->6394 | slave
redis-slave2 | 172.30.0.3 | 6395->6395 | slave
redis-slave3 | 172.30.0.4 | 6396->6396 | slave