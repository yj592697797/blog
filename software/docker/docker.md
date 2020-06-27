## 开机自启

1. docker服务设置开机自启

   ```bash
   #查看已启动的服务
   systemctl list-units --type=service
   #查看是否设置开机启动
   systemctl list-unit-files | grep enable
   #设置开机启动
   systemctl enable docker.service
   #关闭开机启动
   systemctl disable docker.service
   ```

2. 容器设置自启

   ```bash
   docker run --restart=always ...
   ```

3. 如果容器已启动

   ```bash
   docker update --restart=always jenkins
   ```

   