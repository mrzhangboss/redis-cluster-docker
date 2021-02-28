# Redis 主从模式

> 一主两从


## 运行


        docker-compose up

## 测试

进入父节点


        docker exec -it  master_master_1 redis-cli

执行

        127.0.0.1:6379> info replication
        # Replication
        role:master
        connected_slaves:2
        slave0:ip=192.168.64.3,port=6379,state=online,offset=224,lag=1
        slave1:ip=192.168.64.4,port=6379,state=online,offset=224,lag=1
        master_failover_state:no-failover
        master_replid:ede8d2ae5e3ee036aea587202b1aac1ac67f3dc5
        master_replid2:0000000000000000000000000000000000000000
        master_repl_offset:224
        second_repl_offset:-1
        repl_backlog_active:1
        repl_backlog_size:1048576
        repl_backlog_first_byte_offset:1
        repl_backlog_histlen:224
        127.0.0.1:6379> set k1 v1
        OK






进入子节点


        docker exec -it  master_slave_1 redis-cli

执行下面结果


        127.0.0.1:6379> keys *
        1) "k1"
        127.0.0.1:6379> get k1
        "v1"


结果类似即搭建成功


PS： 执行 `docker-compose stop master` 子集群还能响应，但是没法