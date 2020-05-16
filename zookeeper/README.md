

# 安装前准备工作
## 创建zookeeper的网络
```
docker network create --driver bridge --subnet 172.35.0.0/25 --gateway 172.35.0.1  zook_kafka
```
## 查看网络
```
docker network ls
```
## 删除网络
```
docker network rm zook_kafka
```
