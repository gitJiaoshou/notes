# redisCluster搭建

### 新建文件夹，用于放置配置文件
> mkdir config

### 将redis默认配置文件复制到新建的文件夹中
> cp redis.config config/

### 修改一下配置项
>   
    设置密码：requirepass testRedis
    守护进程模式启动：daemonize yes
    设置端口号：port：7001
    ip访问过滤：bind 0.0.0.0  
    快照:pidfile "redis_7001.pid"
    日志：logfile "redis_7001.log"
    日志等文件目录:dir ../data
    是否是cluster模式：cluster-enabled yes
    集群配置,xxx最好为端口号cluster-config-file nodesxxx.conf
    
### 将以上文件分配配置6个不同的端口号及日志名称

### 启动
> 分配启动6个配置文件 redis-server xxx.conf

### 配置分曹
> 到此redis集群已经启动，但是目前还不能使用。因为redis-cluster有分曹的概念。
> 分曹 redis-cli --cluster create 127.0.0.1:7001 127.0.0.1:7002 127.0.0.1:7003 127.0.0.1:7004 127.0.0.1:7005 127.0.0.1:7006 --cluster-replicas 1

### 设置密码
>   
    用命令设置（因为用配置文件配置密码，后面进行分曹配置的时候会报错)
    1. redis-cli -p 端口号
    2. config set requirepass testRedis