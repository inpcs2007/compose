
# 命令
```
docker-compose dc-nexus3.yml up -d
```

## 获得管理员密码
```
docker exec -it nexus3 /bin/bash

cat /opt/sonatype/sonatype-work/nexus/admin.password
```

# 访问
## 访问浏览器地址
```
http://127.0.0.1:8089
```
