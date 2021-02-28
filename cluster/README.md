# Redis 集群模式

> 三主三从


## 运行


        docker-compose up

## 创建集群


                docker exec -it  cluster_master1_1 redis-cli --cluster create 172.16.238.10:6379 172.16.238.11:6379 172.16.238.12:6379 172.16.238.13:6379 172.16.238.14:6379 172.16.238.15:6379 --cluster-replicas 1


## 测试

进入父节点


        docker exec -it  cluster_master1_1 redis-cli -c


执行

        172.16.238.12:6379> info replication
        # Replication
        role:master
        connected_slaves:1
        slave0:ip=172.16.238.13,port=6379,state=online,offset=346,lag=0
        master_failover_state:no-failover
        master_replid:c890ced9bf3c21804c6c5863f0901a697fc2e587
        master_replid2:0000000000000000000000000000000000000000
        master_repl_offset:346
        second_repl_offset:-1
        repl_backlog_active:1
        repl_backlog_size:1048576
        repl_backlog_first_byte_offset:1
        repl_backlog_histlen:346
        172.16.238.12:6379> set k2 v1
        -> Redirected to slot [449] located at 172.16.238.10:6379
        OK
        172.16.238.10:6379>









结果类似即搭建成功

