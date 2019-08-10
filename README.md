## 当前版本
V1.0.0

**快速部署rongwan工具，请参考。**

结构图
```lua
rongwan-docker-dev-tools
├── mongo
├    └── setup
├    └── docker-compose.yml -- mongodb
├    └── Dockerfile
├── tools
├    └── db
├    ├    └── 1schema.sql
├    ├    └── Dockerfile
├    └── docker-compose.yml -- mysql\zookeeper\redis\minio
```

### 环境说明
- mongodb 
- mysql 5.7
- zookeeper 3.4+
- redis 3.2+ 
- minio

```
# 本地测试环境 IP调整

127.0.0.1	rongwan-eureka
127.0.0.1     rongwan-mysql
127.0.0.1	rongwan-zookeeper
127.0.0.1	rongwan-redis
127.0.0.1	rongwan-minio

```

```
# 1. 使用docker-compose 宿主机不需要配置host来发现
# 2. 无需修改源码，根目录  docker-compose up -d即可
# 3. 等待服务启动
# 附件使用命令
# docker ps
# docker ps -a
# docker stop 【CONTAINER ID】或者【NAMES】
# docker rm【CONTAINER ID】或者【NAMES】
# docker exec -it bigdata-mysql bash
# 进入容器：docker exec -it 容器i /bin/bash
# 进入mysql容器：mysql -u root -p 然后输入密码，quit退出，容器退出exit
# 同步时间：docker cp /etc/localtime 容器i:/etc/

# 附件使用命令
# docker-compose down --rmi all -v 删除所有容器[危险操作]
# docker-compose start|stop [项目名称] 单启动和关闭指定项目
# docker-compose logs -f  [项目名称]   实时查看指定项目日志
# docker-compose rm [项目名称]  删除停止的服务（服务里的容器）
# docker-compose build service_a 用来创建或重新创建服务使用的镜像。创建一个镜像名叫service_a
# docker images 查看所有镜像文件
# docker ps -n 10 查看



docker images往往不知不觉就占满了硬盘空间，为了清理冗余的image，可采用以下方法：
1.进入root权限
sudo su
2.停止所有的container，这样才能够删除其中的images：
docker stop $(docker ps -a -q)
如果想要删除所有container的话再加一个指令：
docker rm $(docker ps -a -q)
3.查看当前有些什么images
docker images
4.删除images，通过image的id来指定删除谁
docker rmi <image id>
想要删除untagged images，也就是那些id为<None>的image的话可以用
docker rmi $(docker images | grep "^<none>" | awk "{print $3}")
要删除全部image的话
docker rmi $(docker images -q)

```
