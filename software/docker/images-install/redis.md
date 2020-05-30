## 基本

##### 从dock hub上查询redis

​	`docker search redis`

##### 拉取redis镜像

​	`docker pull redis`

##### 运行redis

​	`docker run --name myredis -d redis`

##### 进入镜像，并运行redis-cli

​	`docker exec -it myredis redis-cli -h localhost -p 6379`

## 高级

将redis容器端口映射、挂载配置文件、持久化数据

##### 1、创建配置文件目录、创建持久化目录

​	`mkdir /root/redis`

​	`mkdir /root/redis/data/`

##### 2、下载通用配置文件

​	`wget https://raw.githubusercontent.com/antirez/redis/6.0/redis.conf -O redis.conf`

##### 3、修改配置文件

```vim
#bind 127.0.0.1
protected-mode no
requirepass yourpass
```

##### 4、启动docker

​	`docker run -d --privileged=true -p 6379:6379 --restart always -v /root/redis/redis.conf:/etc/redis/redis.conf -v /root/redis/data:/data --name myredis redis redis-server /etc/redis/redis.conf --appendonly yes`

​	参数说明：

```
-d                                                  -> 以守护进程的方式启动容器
-p 6379:6379                                        -> 绑定宿主机端口
--name myredis                                      -> 指定容器名称
--restart always                                    -> 开机启动
--privileged=true                                   -> 提升容器内权限
-v /root/docker/redis/conf:/etc/redis/redis.conf    -> 映射配置文件
-v /root/docker/redis/data:/data                    -> 映射数据目录
--appendonly yes                                    -> 开启数据持久化
```