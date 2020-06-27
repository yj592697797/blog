## 前言

最近想熟悉和实践CentOS的使用，目前使用的电脑系统是win10，所以需要用到虚拟机。常用的`VMware Workstation`、`Oracle VM VirtualBox`，还有win10自带的`Hyper-V`。考虑到自己电脑性能的原因，果断选择了占资源更少的Hyper-V。

## 安装

1. 下载[CentOS](https://www.centos.org/centos-linux/)

2. 【控制面板】 -> 【程序和功能】 ->  【用或关闭Windows功能中】开启`Hyper-V`(已开启的跳过)，重启电脑

3. 打开【Hyper-V 管理器】，安装CentOS，

   *注意：*在安装CentOS时，中间有个界面是【软件选择】，千万不要选择Server with GUI（带GUI的服务器）！！！否则，安装后，无法启动。

4. 安装完成后，别急着重启，先在Hyper-V管理器中设置虚拟机网络，

   先后添加【Default Switch】、【内网】两个网络适配器，如果无内网适配器，去虚拟交换机管理器界面添加。然后在本机的【控制面板\所有控制面板项\网络连接】界面设置内网适配器的IP，如192.168.6.1

5. 启动虚拟机，进入虚拟机后，继续设置网络

   进到/etc/sysconfig/network-scripts里面将ifcfg-eth0复制一份改名为ifcfg-eth1，修改ifcfg-eth1，修改后的文件如下：

   ```config
   TYPE=Ethernet
   PROXY_METHOD=none
   BROWSER_ONLY=no
   BOOTPROTO=static #dhcp
   DEFROUTE=yes
   IPV4_FAILURE_FATAL=no
   IPV6INIT=yes
   IPV6_AUTOCONF=yes
   IPV6_DEFROUTE=yes
   IPV6_FAILURE_FATAL=no
   IPV6_ADDR_GEN_MODE=stable-privacy
   NAME=eth1
   UUID=6b2c17e5-40f0-46db-90e1-0f8bc0bae7d9
   DEVICE=eth1
   ONBOOT=yes
   
   IPADDR=192.168.6.100
   GATEWAY=192.168.6.1
   NETMASK=255.255.255.0
   DNS1=8.8.8.8
   DNS2=8.8.4.4
   ```

   ifcfg-eth0 -- 【Default Switch】-- 外网

   ifcfg-eth1 -- 【内网】 -- 内网

6. 重启网卡

   ```bash
   方法：nmcli c reload +网卡名
   
   例：nmcli c reload ens160
   
   如果不行，可尝试以下命令
   
   # 重载所有ifcfg或route到connection（不会立即生效）
   nmcli c reload  ifcfg-xxx
   # 重载指定ifcfg或route到connection（不会立即生效）
   nmcli c load /etc/sysconfig/network-scripts/ifcfg-ethX
   nmcli c load /etc/sysconfig/network-scripts/route-ethX
   # 立即生效connection，有3种方法
   nmcli c up ethX
   nmcli d reapply ethX
   nmcli d connect ethX
   ```

7. 测试网络环境

   测试外网

   ```bash
   ping www.baidu.com
   ```

   测试内网

   ```bash
   #物理机IP 192.168.0.103，关闭防火墙
   ping 192.168.0.103
   ```

## 后记

坑1、安装CentOS前，找了一篇教程，基本是一路【下一步】完事，结果出现无法启动的问题，百度后才知道，不能选择Server with GUI（带GUI的服务器）功能

坑2、外网内网配置，内网没调通！！！



