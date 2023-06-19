# ClickHouse Notes



## 第一章





## 第 2 章 ClickHouse 的安装  

### 2.1 准备工作  

- 确定防火墙处于关闭状态  

- CentOS 取消打开文件数限制

  - 在 hadoop102 的 /etc/security/limits.conf 文件的末尾加入以下内容  

  - 在 hadoop102 的/etc/security/limits.d/20-nproc.conf 文件的末尾加入以下内容  

    ```
    * soft nofile 65536
    * hard nofile 65536
    * soft nproc 131072
    * hard nproc 131072
    ```

    > 未修改前：`ulimit -a`
    >
    > ![image](./images/001.jpg)
    >
    > 修改后：`ulimit -a`
    >
    > ![image](./images/002.jpg)

  - 这里只改了102机器上的文件，同步一下：

    ```shell
    sudo /home/lijzh/bin/xsync /etc/security/limits.conf
    
    sudo /home/lijzh/bin/xsync /etc/security/limits.d/20-nproc.conf
    ```

- 安装依赖  

  ```shell
   sudo yum install -y libtool
  
  sudo yum install -y *unixODBC*
  
  # 在102，、103、104上，分别执行上述命令
  ```

- CentOS 取消 SELINUX  

  ```shell
  sudo vim /etc/selinux/config
  # 修改：
  SELINUX=disabled
  # 注意：别改错了
  
  # 分发
  sudo /home/lijzh/bin/xsync /etc/selinux/config
  ```

  > 注意：这个配置后，一定要重启服务器
  >
  > 查看是否配置成功：`getenforce`

### 2.2 单机安装  

> 才单机安装，集群安装的话
>
> - 将安装包发放到其他服务器
> - 安装命令安装
> - 修改配置文件 / 发放配置文件
> - 有个问题：什么是集群安装？怎么联系到一起去呢？





- 安装目录对应关系

  ```shell
  bin/      /usr/bin/
  conf/     /etc/clickhouse-server/   (这个比较重要)
  #  /etc/clickhouse-server/config.xml
  # 在这个文件中，有 ClickHouse 的一些默认路径配置，比较重要的
  # 数据文件路径： <path>/var/lib/clickhouse/</path>
  # 日志文件路径： <log>/var/log/clickhouse-server/clickhouse-server.log</log>
  
  lib/      /var/lib/clickhouse
  log/      /var/1og/clickhouse
  ```

- 启动服务

  ```shell
  sudo clickhouse start/stop/restart
  ```

- 连接clickhouse

  ```shell
  clickhouse-client --password li123... -m
  ```

  





