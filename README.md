# rethinkdb 在线实验环境

## 软件简介

软件基本信息，License，所属的类别，作用，特点等。
RethinkDB是一个开源的分布式数据库，用于存储JSON文档，并轻松扩展到多台机器。它易于设置和学习，并具有一个简单但强大的查询语言，支持表连接，分组，聚合和功能。

所属类别是数据库

License:GNU Affero

特点：

1.启动快，性能高

2.提供性能与数据稳定性之间的精细调控

## 软件官网

https://rethinkdb.com/

## Dockerfile 使用方法

### 如何使用
使用安装在工作目录中的数据启动实例

映像的默认CMD是rethinkdb --bind all，因此RethinkDB守护程序将绑定到容器可用的所有网络接口（默认情况下，RethinkDB仅接受连接localhost）。
```
docker run --name some-rethink -v "$PWD:/data" -d rethinkdb
```
将实例连接到应用程序
```
docker run --name some-app --link some-rethink:rdb -d application-that-uses-rdb
```
连接到同一主机上的Web管理界面
```
$BROWSER "http://$(docker inspect --format \
  '{{ .NetworkSettings.IPAddress }}' some-rethink):8080"
  ```
通过SSH连接到远程/虚拟主机上的Web管理界面

remote远程用户@ hostname的别名在哪里？
```
# start port forwarding
ssh -fNTL localhost:8080:$(ssh remote "docker inspect --format \
  '{{ .NetworkSettings.IPAddress }}' some-rethink"):8080 remote

# open interface in browser
xdg-open http://localhost:8080

# stop port forwarding
kill $(lsof -t -i @localhost:8080 -sTCP:listen)
```
## 资源链接

- https://rethinkdb.com/
- http://www.oschina.net/p/rethinkdb
- https://hub.docker.com/_/rethinkdb/
