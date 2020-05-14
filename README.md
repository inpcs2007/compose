## 介绍

本项目是使用docker-compose构建中间件的项目，将会通过一个个的样例，可以容易的将各个中间件组件构建起来，包括：

* Gitlab（源代码管理）
* Mysql（关系数据库）
* Redis（Nosql数据库）
* jenkins（CI/CD）

## 目录结构
```
└── compose                   -- 项目目录
    ├── LICENSE               -- Apache License 2.0
    ├── README.md
    ├── gitlab                -- 中间件名称
    │   ├── README.md         -- 中间件的介绍文档
    │   ├── config            -- 中间件配置目录
    │   ├── docker-compse.yml --docker-compse编排文件
    └── redis
```

## 案例背景

docker已经成为快速构建环境的必要条件，但是怎么快速构建中间件都很分散在网路上，有时候找到但是不可用。
基于这样的考虑，所以才有了本项目同时也是用于个人日常使用的一个快速查找的知识库。

## 参考资料



