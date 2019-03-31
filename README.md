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

集群模式下存取数据
```
[root@16ad7957a8d9 config]# redis-cli -h 47.101.139.0 -p 6391 set li1 xiantao
(error) MOVED 14794 47.101.139.0:6393
[root@16ad7957a8d9 config]# redis-cli -c  -h 47.101.139.0 -p 6391 set li1 xiantao
OK
```

虚拟槽信息：
```
[root@16ad7957a8d9 config]# redis-cli -h 47.101.139.0 -p 6393 cluster slots
1) 1) (integer) 0
   2) (integer) 5461
   3) 1) "47.101.139.0"
      2) (integer) 6391
      3) "065329b3eab4fcbf8a3fdec7aaa94bfe8f1b2269"
   4) 1) "47.101.139.0"
      2) (integer) 6394
      3) "2ba30a5928ae25edbee86fbc1533f15e0ed741ca"
2) 1) (integer) 5462
   2) (integer) 10922
   3) 1) "47.101.139.0"
      2) (integer) 6392
      3) "2755de0227e31d0efa2165ad3aa31dd071df7533"
   4) 1) "47.101.139.0"
      2) (integer) 6395
      3) "385ac14823cbbfd70495f8ac144a707b0951416a"
3) 1) (integer) 10923
   2) (integer) 16383
   3) 1) "172.50.0.4"
      2) (integer) 6393
      3) "3d237dc9be6b8b02ae40f5034f889abfcecd9acd"
   4) 1) "47.101.139.0"
      2) (integer) 6396
      3) "cc5602da339f11df90a7957a6af88fc3fbb61831"
```