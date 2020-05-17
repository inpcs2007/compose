

# 通过密码方式来访问redis的两种方式
## 通过配置文件conf存放redis的访问密码
```
requirepass redispwd
# redispwd 是redis访问时需要的密码 
```
## 通过命令配置实现redis的密码访问
```
command: redis-server --requirepass 123456 --appendonly yes
```

# 配追redis集群的网络环境
```
docker network create --driver bridge --subnet 172.36.0.0/25 --gateway 172.36.0.1  redis_cluster
```
