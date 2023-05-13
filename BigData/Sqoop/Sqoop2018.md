# Sqoop-2018

## Remark

- Sqoop : sql to hadoop





## 第3章 Sqoop安装

- 下载地址：http://mirrors.hust.edu.cn/apache/sqoop/1.4.6/

- 上传安装包`sqoop-1.4.6.bin__hadoop-2.0.4-alpha.tar.gz`到虚拟机中

- 解压sqoop安装包到指定目录，如：

  ```shell
  tar -zxvf sqoop-1.4.6.bin__hadoop-2.0.4-alpha.tar.gz -C /opt/module/
  
  mv sqoop-1.4.6.bin__hadoop-2.0.4-alpha sqoop-1.4.6
  ```

- 修改配置文件

  Sqoop的配置文件与大多数大数据框架类似，在sqoop根目录下的conf目录中。

  - 重命名配置文件

    ```shell
    mv sqoop-env-template.sh sqoop-env.sh
    ```

  - 修改配置文件

    sqoop-env.sh

    ```sh
    export HADOOP_COMMON_HOME=/opt/module/hadoop-3.1.3
    export HADOOP_MAPRED_HOME=/opt/module/hadoop-3.1.3
    export HIVE_HOME=/opt/module/hive-3.1.2
    export ZOOKEEPER_HOME=/opt/module/zookeeper-3.5.7
    export ZOOCFGDIR=/opt/module/zookeeper-3.5.7
    export HBASE_HOME=/opt/module/hbase-2.4.11

- 拷贝JDBC驱动

  - 拷贝jdbc驱动到sqoop的lib目录下，如：

    ```shell
    cp /opt/software/mysql-connector-java-5.1.37.jar ./lib
    ```

- 验证 Sqoop  

  ```shell
  bin/sqoop help
  ```

- 测试 Sqoop 是否能够成功连接数据库  

  ```
  ./bin/sqoop list-databases --connect jdbc:mysql://l9z102:3306/ --username root --password li123...
  ```

## 第 4 章 Sqoop 的简单使用案例



###  导入数据



####  RDBMS到HDFS

- 全表导入

  ```shell
  bin/sqoop import \
  --connect jdbc:mysql://l9z102:3306/company \
  --username root \
  --password li123... \
  --table staff \
  --target-dir /user/company \
  --delete-target-dir \
  --num-mappers 1 \
  --fields-terminated-by "\t"
  ```

  > `--delete-target-dir \` 表示：如果目标目录存在，则先删除，
  >
  > 因为mr任务，要求hdfs目标目录不能存在

- 查询导入

  ```shell
  bin/sqoop import \
  --connect jdbc:mysql://l9z102:3306/company \
  --username root \
  --password li123... \
  --target-dir /user/company \
  --delete-target-dir \
  --num-mappers 1 \
  --fields-terminated-by "\t" \
  --query 'select name,sex from staff where id <=1 and $CONDITIONS;'
  
  --query "select name,sex from staff where id <=1 and \$CONDITIONS;"
  ```

  > 提示：must contain '$CONDITIONS' in WHERE clause.
  >
  > 如果query后使用的是双引号，则$CONDITIONS前必须加转移符，防止shell识别为自己的变量。
  >
  > `--query "select name,sex from staff where id <=1 and \$CONDITIONS;"`

- 导入指定列

  指定`id,sex`这两个列

  ```shell
  bin/sqoop import \
  --connect jdbc:mysql://l9z102:3306/company \
  --username root \
  --password li123... \
  --target-dir /user/company \
  --delete-target-dir \
  --num-mappers 1 \
  --fields-terminated-by "\t" \
  --columns id,sex \
  --table staff
  
  bin/sqoop import \
  --connect jdbc:mysql://l9z102:3306/company \
  --username root \
  --password li123... \
  --columns id,sex \
  --table staff  \
  --target-dir /user/company \
  --delete-target-dir \
  --num-mappers 1 \
  --fields-terminated-by "\t" 
  ```

  > 提示：columns中如果涉及到多列，用逗号分隔，分隔时不要添加空格

- 使用sqoop关键字筛选查询导入数据

  ```shell
  bin/sqoop import \
  --connect jdbc:mysql://l9z102:3306/company \
  --username root \
  --password li123... \
  --target-dir /user/company \
  --delete-target-dir \
  --num-mappers 1 \
  --fields-terminated-by "\t" \
  --table staff \
  --where "id=1"
  
  
  bin/sqoop import \
  --connect jdbc:mysql://l9z102:3306/company \
  --username root \
  --password li123... \
  --target-dir /user/company \
  --delete-target-dir \
  --num-mappers 1 \
  --fields-terminated-by "\t" \
  --table staff \
  --columns id,sex \
  --where "id=1"
  ```

  > --query 和 --where 不能同时使用。

#### RDBMS到Hive

```shell
bin/sqoop import \
--connect jdbc:mysql://l9z102:3306/company \
--username root \
--password li123... \
--table staff \
--num-mappers 1 \
--hive-import \
--fields-terminated-by "\t" \
--hive-overwrite \
--hive-table staff_hive
```

> 提示：该过程分为两步，
>
> ​			第一步将数据导入到HDFS，第一步默认的临时目录是/user/用户名/表名
>
> ​			第二步将导入到HDFS的数据迁移(复制到)到Hive仓库，会在hive默认数据库创建新的表staff_hive，将数据复制到这里。

#### RDBMS到Hbase

```shell
bin/sqoop import \
--connect jdbc:mysql://l9z102:3306/company \
--username root \
--password li123... \
--table staff \
--columns "id,name,sex" \
--column-family 'info' \
--hbase-create-table \
--hbase-row-key 'id' \
--hbase-table 'hbase_staff' \
--num-mappers 1 \
--split-by id
// 没导入成功？？？？？？？？？？？？？？？？？？？？？？？？？？？？？hbase版本太高？？？？？？？？？？？？
```

> 提示：sqoop1.4.6只支持HBase1.0.1之前的版本的自动创建HBase表的功能
>
> 解决方案：手动创建HBase表
>
> > `hbase> create 'hbase_staff,'info'`
> >
> > 在HBase中scan这张表得到如下内容
> >
> > `hbase> scan 'hbase_staff'`

### 导出数据

​        在Sqoop中，“导出”概念指：从大数据集群（HDFS，HIVE，HBASE）向非大数据集群（RDBMS）中传输数据，叫做：导出，即使用export关键字。

#### HIVE/HDFS到RDBMS

```shell
bin/sqoop export \
--connect jdbc:mysql://l9z102:3306/company \
--username root \
--password li123... \
--table staff \
--num-mappers 1 \
--export-dir /user/hive/warehouse/staff_hive \
--input-fields-terminated-by "\t"
```

> 提示：Mysql中如果表不存在，不会自动创建

### 脚本打包













