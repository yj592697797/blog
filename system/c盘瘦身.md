1. nuget缓存默认安装位置在c盘，随着项目进展，引用到依赖越多，占用c盘空间就越大

   `解决方案`：VS安装后修改Nuget缓存路径，[官方文档](https://docs.microsoft.com/zh-cn/nuget/consume-packages/managing-the-global-packages-and-cache-folders)

   `配置文件路径`：%AppData%\NuGet\NuGet.Config

   `原缓存路径`：%User%\.nuget\packages

   ```xml
   <configuration>
     ...
     <config>
   		<add key="globalPackagesFolder" value="E:\AppData\.nuget\packages" />
     </config>
   </configuration>
   ```

2. 虚拟内存分页文件默认分配在c盘，占用大量磁盘空间

   `解决方案`：设置到其他盘即可

3. 使用spaceSniffer分析磁盘占用清空