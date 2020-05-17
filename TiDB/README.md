# 使用docker-compose来构建TiDB集群环境


# 快速部署 
## 下载 tidb-docker-compose
```
git clone https://github.com/pingcap/tidb-docker-compose.git
```
## 创建并启动集群
```
cd tidb-docker-compose && docker-compose pull && docker-compose up -d
```
## 访问集群
```
mysql -h 127.0.0.1 -P 4000 -u root
```
## 访问集群 Grafana 监控页面
```
http://localhost:3000 默认用户名和密码均为 admin
```
## 集群数据可视化：
```
http://localhost:8010
```

# 访问 Spark shell 并加载 TiSpark
## 向 TiDB 集群中插入一些样本数据
```
docker-compose exec tispark-master bash &&
cd /opt/spark/data/tispark-sample-data &&
mysql -h tidb -P 4000 -u root < dss.ddl
```
## 当样本数据加载到 TiDB 集群之后，可以使用 docker-compose exec tispark-master /opt/spark/bin/spark-shell 来访问 Spark shell。
```
docker-compose exec tispark-master /opt/spark/bin/spark-shell
```

```
...
Spark context available as 'sc' (master = local[*], app id = local-1527045927617).
Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.1.1
      /_/

Using Scala version 2.11.8 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_172)
Type in expressions to have them evaluated.
Type :help for more information.
```

```
scala> import org.apache.spark.sql.TiContext
...
scala> val ti = new TiContext(spark)
...
scala> ti.tidbMapDatabase("TPCH_001")
...
scala> spark.sql("select count(*) from lineitem").show
```

```
+--------+
|count(1)|
+--------+
|   60175|
+--------+
```

# 参考官方文档
https://github.com/pingcap/docs-cn/blob/release-3.0/deploy-test-cluster-using-docker-compose.md
