#kafka-manager 浏览器地址
```
http://localhost:9000
```
# kafka常用命令
## 查看所有topic列表
```
# docker 外部访问
docker exec broker1 kafka-topics.sh --list --zookeeper zoo1:2181,zoo2:2182,zoo3:2183  
```
## 查看指定topic信息
```
# docker 外部访问 名称为mytest-topic的topic
docker exec broker1 kafka-topics.sh --zookeeper zoo1:2181,zoo2:2182,zoo3:2183  --describe --topic mytest-topic
```
## 控制台向topic生产数据
```
docker exec -it broker1 kafka-console-producer.sh --broker-list broker1:9091,broker2:9092,broker3:9093 --topic mytest-topic
```
## 控制台消费topic的数据
```
docker exec -it broker1 kafka-console-consumer.sh --bootstrap-server broker1:9091 --topic mytest-topic --from-beginning
```
## 查看topic某分区偏移量最大（小）值
## 增加topic分区数
## 删除topic，慎用，只会删除zookeeper中的元数据，消息文件须手动删除
## 查看topic消费进度
