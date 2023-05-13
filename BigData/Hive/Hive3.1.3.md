# Hive3.1.3

## Hive 安装部署

- 解压安装包

- 配置环境变量

- 解决jar包冲突

  ```
  mv log4j-slf4j-impl-2.17.1.jar log4j-slf4j-impl-2.17.1.bak
  ```

- 上传`mysql-connector-java-5.1.37.jar`

- 创建配置文件 - `hive-site.xml`

- MySQL创建出元数据库，库名和配置文件`hive-site.xml`保持一致

- MySQL配置 - **见最开始的记录**

- 修改hive日志路径

  - 修改  `mv hive-log4j2.properties.template hive-log4j2.properties`  (template是模板文件不会加载)

    > 默认hive日志放在 `/tmp/$user/hive.log`
    >
    > > 生成方式：当天的日志存储在hive.log，零点的时候，会变成hive.log.xxxx-xx-xx，然后再生成一个新的hive.log
    > >
    > > > 这样的存储方式，可能会存在零点漂移问题，(Flume拦截器可以更正）
    >
    > 通过配置文件，修改hive日志的存储地址

  ```properties
  # hive-log4j2.properties
  
  status = INFO
  name = HiveLog4j2
  packages = org.apache.hadoop.hive.ql.log
  
  # list of properties
  property.hive.log.level = INFO
  property.hive.root.logger = DRFA
  # ----------------------修改这个信息，更改hive日志存储位置--------------------------------
  property.hive.log.dir = /opt/module/hive-3.1.2/logs     
  # -----------------------------------------------------------------------------------
  property.hive.log.file = hive.log
  property.hive.perflogger.log.level = INFO
  
  # list of all appenders
  appenders = console, DRFA
  
  ```

- 初始化元数据库

  ```
  bin/schematool -initSchema -dbType mysql -verbose
  ```

- 启动hive



## Hive 源码编译

### Remark

- 错误：`Exception in thread "main" java.lang.NoSuchMethod:` + **一些类**
  - 原因：依赖版本问题，根据后面的类，找出自那个依赖。

- 



















