

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

