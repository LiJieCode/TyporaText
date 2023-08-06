# RocketMQ Notes

## Remark

- 消息队列有啥用？
  - 异步
  - 削峰限流







## 安装启动

### 安装

- 解压zip包
- 修改bin文件
- 修改conf文件

- 配置环境变量

  ```shell
  vim /etc/profile.d/my_env.sh
  
  # 增加
  # RocketMQ
  export NAMESRV_ADDR=l9z102:9876
  ```

  

### 启动

- 先启动NameServer <span style="color:red; font-weight:bold">（不能随便执行，注意路径）</span>

  ```shell
  cd /opt/module/rocketmq-4.9.2
  # 执行启动命令
  nohup sh bin/mqnamesrv &
  
  # 指定日志文件
  nohup sh bin/mqnamesrv > xxx.log &
  ```

  > 

- 再启动Broker（注意路径）

  ```shell
  cd /opt/module/rocketmq-4.9.2
  # 执行启动命令
  nohup sh bin/mqbroker -c conf/broker.conf &
  
  # 指定日志文件
  nohup sh bin/mqbroker -c conf/broker.conf > xxx.log &
  ```

  > 

- （可选）可视化jar包启动（注意jar包路径）

  ```shell
  # 进到下面路径
  cd /opt/software/rocketmq
  # 执行命令
  nohup java -jar rocketmq-dashboard-1.0.0.jar --server.port=8001 --rocketmq.config.namesrvAddr=127.0.0.1:9876 > dashboard.log &
  ```

  > web端可视化网址：l9z102:8001

## 快速上手

