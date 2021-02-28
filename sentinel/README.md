# Redis 哨兵模式

> 一主两从三哨兵


## 运行


        docker-compose up

## 测试

进入父节点


        docker exec -it  sentinel_master_1 redis-cli

执行

        127.0.0.1:6379> info replication
        # Replication
        role:master
        connected_slaves:2
        slave0:ip=192.168.176.3,port=6379,state=online,offset=56,lag=1
        slave1:ip=192.168.176.7,port=6379,state=online,offset=56,lag=0
        master_replid:529dec143388daa8abea944027f881e20951dde5
        master_replid2:0000000000000000000000000000000000000000
        master_repl_offset:56
        second_repl_offset:-1
        repl_backlog_active:1
        repl_backlog_size:1048576
        repl_backlog_first_byte_offset:1
        repl_backlog_histlen:56
        127.0.0.1:6379> set k1 v1
        OK







进入子节点


        docker exec -it  sentinel_slave1_1 redis-cli

执行下面结果


        127.0.0.1:6379> keys *
        1) "k1"
        127.0.0.1:6379> get k1
        "v1"


结果类似即搭建成功


PS： 执行 `docker-compose stop master` , slave1 或者2 会变成master，将master重新启动，master会变成slave



