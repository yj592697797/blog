##### 查看端口

​	`lsof -i:8000`   或者  `netstat -tunlp | grep 8000`

##### 查询端口是否对外开放

​	`firewall-cmd --query-port=6379/tcp`

##### 防火墙的使用

​	状态：`systemctl status firewalld`

​	开启：`systemctl start firewalld`

​	关闭：`systemctl stop firewalld`

​	若无法开启防火墙，先`systemctl unmask firewalld.service`然后`systemctl start firewalld.service`

