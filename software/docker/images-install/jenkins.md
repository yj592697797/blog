## 安装

```bash
docker run -d -p 8080:8080 -p 50000:50000 \
           -v jenkins_home:/var/jenkins_home \
           -v /etc/localtime:/etc/localtime \
           --name jenkins jenkins/jenkins
```

- `-d` 后台运行镜像
- `-p 8080:8080 -p 50000:50000` 端口映射
- `-v jenkins_home:/var/jenkins_home` jenkins数据卷
- `-v /etc/localtime:/etc/localtime` 让容器的时间与宿主一致
- `--name jenkins jenkins/jenkins` 容器名称

容器运行后，即可访问[jenkins主页](*host:8080*)，顺利的话，一路下一步即可完成初始化工作

## 排错

1. 初始化时，提示`离线`，使用docker logs jenkins tail -50查看到异常`java.net.UnknownHostException:updates.jenkins.io`，看异常信息是不能解析主机，通过如下方法解决，参考https://blog.yeefire.com/2020_03/docker_DNS_resolve.html

   1）未开启IP转发功能，通过命令查看，返回no，则未开启

   ```bash
   #查看是否开启IP转发功能
   sudo firewall-cmd --query-masquerade
   
   #开启
   sudo firewall-cmd --add-masquerade --permanent && sudo firewall-cmd --reload
   ```

   2）配置正确的DNS

   ```bash
   #查看dns配置
   cat /etc/resolv.conf	
   #查看当前网络连接
   sudo nmcli connection
   #设置dns
   sudo nmcli connection modify ethernet-eth0(你的网卡连接名) ipv4.dns=114.114.114.114
   #重启网卡
   sudo nmcli connection up ethernet-eth0(你的网卡名)
   ```

   3）强制Docker使用自定义的DNS

   ```bash
   vim /etc/docker/daemon.json
   ```

   ```json
   {
       "dns": ["114.114.114.114"]
   }
   ```

   

2. 插件安装失败或者慢，切换插件源

   /pluginManager/advanced

   最下面的【升级站点】，改为：https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/update-center.json

