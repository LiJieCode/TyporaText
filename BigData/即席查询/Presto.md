# Presto Notes

## Remark

- Presto 是一个开源的分布式SQL查询引擎，数据量支持GB-PB，主要用于处理秒级查询场景。
- 注意：虽然Presto可以解析SQL，但它不是一个标准的数据库。不是MySQL、Oracle的代替品，也不能用来处理在线事务(OLTP)
- Presto 不依赖于Yarn



## Presto 概述

### Presto 架构

<img src="./images/001.jpg" alt="image" style="zoom:72%;" />

### Presto 优缺点

<img src="./images/002.jpg" alt="image" style="zoom:67%;" />

> MR慢的原因：
>
> - 每个任务间的数据要轮盘，MapTask和ReduceTask之间的数据也要落盘
> - 数据还存在网络传输（网络传输：各服务器之间的数据交换）



## Predto 部署

### Presto Server安装



```shell
# 后台启动
xcall /opt/module/presto-server-0.196/bin/launcher start
# 关闭 Presto 服务
xcall /opt/module/presto-server-0.196/bin/launcher stop
```





### Presto命令行Client安装

- 启动presto客户端

```shell
./presto-cli --server l9z102:8881 --catalog hive --schema default
```



### Presto可视化Client安装

- 启动

  ```shell
  nohup bin/yanagishima-start.sh >y.log 2>&1 &
  ```

> Web地址：l9z102:7080



### Presto优化之数据存储

- Presto对`ORC`文件读取做了特定优化，因此在Hive中创建Presto使用的表时，建议采用ORC格式存储。相对于Parquet，Presto对ORC支持更好。

- 数据压缩可以减少节点间数据传输对IO带宽压力，对于即席查询需要快速解压，建议采用`Snappy压缩`。

> 如果Hive中的表要交给presto进行即席查询，那么建议选择：<span style="color:blue; font-weight:bold">ORC存储+snappy压缩</span>



### Presto优化之查询SQL

- 只选择使用的字段

- 过滤条件必须加上分区字段
- Group By语句优化

> 将Group By语句中字段按照每个字段distinct数据多少进行降序排列。（区分度大的放前面）

- Order by时使用Limit
- 使用Join语句时将大表放在左边



### 注意事项

- 字段名引用

> 避免和关键字冲突：MySQL对字段加**反引号`**、Presto对字段加**双引号**分割
>
> 当然，如果字段名称不是关键字，可以不加这个双引号。

- 时间函数

> 对于Timestamp，需要进行比较的时候，需要添加Timestamp关键字，而MySQL中对Timestamp可以直接进行比较。
>
> date、datetime，timestamp
>
> > 数仓中所有的时间都是字符串类型
>
> ```sql
> /*MySQL的写法*/
> SELECT t FROM a WHERE t > '2017-01-01 00:00:00'; 
> # mysql 中，时间和字符串可以比较，存在隐式转换。
> 
> 
> /*Presto中的写法*/
> SELECT t FROM a WHERE t > timestamp '2017-01-01 00:00:00';
> ```

- 不支持INSERT OVERWRITE语法
- PARQUET格式
