# 通过Docker Desktop 安装sandbox-hdp-3.0.1

## 安装命令
```
 sh docker-deploy-{HDPversion}.sh
```
## 拉取 docker 镜像（hortonworks/sandbox-hdp 和 hortonworks/sandbox-proxy）其中hdp为27.5G

## 重置ambari登录密码
通过docker Desktop 的sandbox-hdp的ctl进入docker容器，执行ambari重置命令
```
ambari-admin-password-reset
```
两次输入密码，完成本次密码重置工作。

## 使用浏览器访问网址
```
http://localhost:1080/
```
* 点击launch dashboard 进入ambari登录页面
* 使用admin登录，密码是重置时候输入的密码

完成整个hdp的安装工作，剩下就是正常使用层面。

# 参考链接
https://github.com/dounine/sandbox-hdp-3.0.1.git 

