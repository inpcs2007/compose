

# 安装前准备工作
## 创建zookeeper的网络
```
docker network create --subnet=172.35.0.0/16 zoo_kafka
```
## 查看网络
```
docker network ls
```
## 删除网络
```
docker network rm zoo_kafka
```
