# 基于binglog的方式构建mysql（5.7.17）的主从集群

## 数据库信息
### master数据库配置信息
```
账号：root
密码：root
端口（外）：33065
端口（内）：3306
```
### slave数据库配置信息
```
账号：root
密码：root
端口（外）：33066
端口（内）：3306
``` 

## 配置主从集群

### 配置 master 数据库
#### 查看master数据库中连接slave的状态
```
mysql> show slave status;
Empty set (0.00 sec)
```
#### 查看master数据库的状态
```
mysql> show master status;
+---------------------------+----------+--------------+------------------+-------------------+
| File                      | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
+---------------------------+----------+--------------+------------------+-------------------+
| replicas-mysql-bin.000003 |      154 |              | mysql            |                   |
+---------------------------+----------+--------------+------------------+-------------------+
1 row in set (0.00 sec)
```
### 配置 slave 数据库
#### 在slave数据库上运行master数据库的相关配置 sql 进行master-slave关联
```
CHANGE MASTER TO
    MASTER_HOST='mysql-master',
    MASTER_USER='root',
    MASTER_PASSWORD='root',
    MASTER_LOG_FILE='replicas-mysql-bin.000003',
    MASTER_LOG_POS=154;
```
#### 重启slave容器
```
mysql> show slave status\G;
*************************** 1. row ***************************
               Slave_IO_State: Waiting for master to send event
                  Master_Host: mysql-master
                  Master_User: root
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: replicas-mysql-bin.000003
          Read_Master_Log_Pos: 154
               Relay_Log_File: replicas-mysql-relay-bin.000003
                Relay_Log_Pos: 329
        Relay_Master_Log_File: replicas-mysql-bin.000003
             Slave_IO_Running: Yes
            Slave_SQL_Running: Yes
              Replicate_Do_DB: 
          Replicate_Ignore_DB: 
           Replicate_Do_Table: 
       Replicate_Ignore_Table: 
      Replicate_Wild_Do_Table: 
  Replicate_Wild_Ignore_Table: 
                   Last_Errno: 0
                   Last_Error: 
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 154
              Relay_Log_Space: 545
              Until_Condition: None
               Until_Log_File: 
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File: 
           Master_SSL_CA_Path: 
              Master_SSL_Cert: 
            Master_SSL_Cipher: 
               Master_SSL_Key: 
        Seconds_Behind_Master: 0
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 0
                Last_IO_Error: 
               Last_SQL_Errno: 0
               Last_SQL_Error: 
  Replicate_Ignore_Server_Ids: 
             Master_Server_Id: 100
                  Master_UUID: b9153d33-9b86-11ea-b04b-0242ac160003
             Master_Info_File: /var/lib/mysql/master.info
                    SQL_Delay: 0
          SQL_Remaining_Delay: NULL		
```

## 测试
### 在master数据库中创建测试表
```
use replicas_db;
SET FOREIGN_KEY_CHECKS=0;

-- ----------------------------
-- Table structure for course
-- ----------------------------
DROP TABLE IF EXISTS `course`;
CREATE TABLE `course` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(20) NOT NULL,
  `lesson_period` double(5,0) DEFAULT NULL,
  `score` double(10,0) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```
### 在slave数据库中的replicas_db下回有一个course表

## 参考资料
https://zhuanlan.zhihu.com/p/45193580

















