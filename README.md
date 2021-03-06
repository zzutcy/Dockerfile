# Dockerfile

Jumpserver all in one Dockerfile

This project is only for Docker image build, this docker image we do not suggest you build in a product environment.

该项目仅仅是Jumpserver项目的docker镜像生成代码，我们不建议在生产环境下使用该镜像。

The main reasons are:

   - the database is in the docker too, and we suggest you use your own database by docker env.
   - lack of scalability
   - NO HA plan
   - some unknown problems

主要原因是：

   - 数据库在docker内，建议通过docker的环境变量去使用外部数据库
   - 几乎丧失的横向扩展能力
   - 没有HA的解决方案
   - 未知的一些问题

## How to start


```bash
docker run --name jms_server -dp 80:80 -p 2222:2222 jumpserver/jms_all:latest

```

使用外置mysql数据库和redis:

**设置环境变量：**

- BOOTSTRAP_TOKEN = nwv4RdXpM82LtSvmV

- DB_ENGINE = mysql
- DB_HOST = mysql_host
- DB_PORT = 3306
- DB_USER = xxx
- DB_PASSWORD = xxxx
- DB_NAME = jumpserver

- REDIS_HOST = 127.0.0.1
- REDIS_PORT = 3306
- REDIS_PASSWORD =

- JUMPSERVER_KEY_DIR=/config/guacamole/keys \
- GUACAMOLE_HOME=/config/guacamole \
- JUMPSERVER_SERVER=http://127.0.0.1:8080

- VOLUME /opt/jumpserver/data
- VOLUME /opt/coco/keys
- VOLUME /config/guacamole/keys
- VOLUME /var/lib/mysql


```bash
docker run --name jms_server -d \
  -v /opt/jumpserver:/opt/jumpserver/data
  -v /opt/coco:/opt/coco/keys
  -v /opt/guacamole:/config/guacamole/keys
  -v /opt/mysql:/var/lib/mysql
  -p 80:80 \
  -p 2222:2222 \
  -e BOOTSTRAP_TOKEN=nwv4RdXpM82LtSvmV \
  -e DB_ENGINE=mysql \
  -e DB_HOST=192.168.x.x \
  -e DB_PORT=3306 \
  -e DB_USER=root \
  -e DB_PASSWORD=xxx \
  -e DB_NAME=jumpserver \
  -e REDIS_HOST=192.168.x.x \
  -e REDIS_PORT=6379 \
  -e REDIS_PASSWORD=password \
  wojiushixiaobai/jumpserver:latest

```
