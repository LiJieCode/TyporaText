# Hive-Note

## 一、Hive的执行过程

- **(*)一条 Hive SQL 语句怎么成为的MR/Spark程序？**

> 当我们使用CLI（命令行）或者jdbc（jdbc连接到Hive)将一条 SQL 语句传给Hive的diver时，driver会根据metastore和driver中的四个器，将sql转化成MR/Spark。
>
> 具体来说是，SQL经过**解析器**，转化成抽象语法树，再通过**编译器**形成逻辑执行计划，再通过**优化器**，形成优化后的逻辑执行计划，最后通过**执行器**，形成物理执行计划，也就Spark/MR。
>
> <img src="./images/003.jpg" alt="image" style="zoom:80%;" />

- **所有的 Hive 任务都会MapReduce执行吗？**

> 肯定不是的，对于简单的不需要聚合的SELECT 语句，不需要起MapReduce job，直接通过Fetch task获取数据。

## 二、Hive的优点和缺点

- **Hive 有哪些优点？**

> - Hive 避免了写MR代码
> - 可以处理大量级的数据（小数据就划不来了）
> - 可以支持用户自定义函数

- **Hive 有哪些缺点？**

> - 相比于MR代码，Hive SQL 表达能力有限（不支持循环，迭代。。。）
> - HIve的效率较低
> - Hive调优困难（粒度比较粗）

## 三、Hive 的内外表

- (*)Hive 内外表的区别？

> 对于Hive的内部表，使用删除语句删除表时，会把元数据和实际存储在HDFS的数据都会删除。
>
> 对于Hive的外部表，使用删除语句删除表时，只会删除元数据，实际存储在HDFS的数据还在。
>
> <span style='color:red; font-weight:bold'>备注：</span>其实在实际开发中也只是注重内外部表上述的区别。所以知道这一点就可以了。

- Hive 怎么创建外部表，用到哪个关键字？

> 用`external`关键字可以创建外部表。
>
> ```sql
> create external table_name(
> ...
> );
> ```

## 四、Hive 内置函数

- Hive 的聚合函数了解哪些，举例说几个？

> 参考手册地址：[LanguageManual UDF - Apache Hive - Apache Software Foundation](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF)
>
> - 内置聚合函数  
>
>   - <span style='color:blue; font-weight:bold'>count</span>
>
>     - `count(*)`：返回总行数，包括null值
>     - `count(expr)`：返回字段非空的行数
>     - `count(distinct expr)`：返回去重之后字段非空的行数
>
>     > <span style='color:red; font-weight:bold'>注意：</span>由于 COUNT DISTINCT 操作需要用一个Reduce Task 来完成， 这一个 Reduce 需要处理的数据量太大， 就会导致整个 Job 很难完成。一般 COUNT DISTINCT 使用、先 GROUP BY 再 COUNT 的方式替换，但是需要注意 group by 造成的数据倾斜问题.  
>
>   - <span style='color:blue; font-weight:bold'>sum、avg</span>
>
>     - `sum(expr)`：求和
>     - `sum(distinct expr)` ：去重求和
>
>   - <span style='color:blue; font-weight:bold'>min、max</span>
>
>   - <span style='color:blue; font-weight:bold'>collect_set(expr)</span>
>
>     - 返回消除了重复元素的数组，去重
>     - 通常和`concat_ws(separator, collect_set(expr))`
>
>   - <span style='color:blue; font-weight:bold'>collect_list(expr)</span>
>
>     - 返回允许重复元素的数组，不去重
>     - 通常和`concat_ws(separator, collect_list(expr))`

- (*)Hive 的炸裂函数了解吗？Explode()?

> 炸裂函数UDTF：`Explode()`
>
> - 函数功能：将 hive 一列中复杂的 Array 或者 Map 结构拆分成多行，<span style='color:blue; font-weight:bold'>explode的参数为数组</span>
> - `lateral view`  创建一个侧写表
> - 用法：`LATERAL VIEW udtf(expression) tableAlias AS columnAlias `
>
> ```sql
> # 举例：
> SELECT movie,
> 	   category_name
> FROM movie_info
> lateral VIEW 
> explode(split(category,",")) movie_info_tmp AS category_name;
> ```

- Hive 怎么用 Explore() 实现侧写表？

> 见上；

- Hive 的窗口函数了解吗？

> 使用`over()`用来给聚合函数开窗

- (*)窗口函数中的排序函数有哪几种，他们的区别是什么？

> 

## 五、Hive 自定义函数

- (*)有没有写过 Hive 的自定义函数？

> 这个一定要有呀！具体过程见下；

- 说一说 Hive 的自定义函数的主要过程？

> 

- (*)Hive的函数：UDF、UDAF、UDTF的区别？

> UDF：单行进入，单行输出
>
> UDAF：多行进入，单行输出
>
> UDTF：单行输入，多行输出

## 六、Hive 如何解决数据倾斜

- (*)哪些操作会导致 Hive 的数据倾斜？
- (*)怎么解决 Hive 中的数据倾斜？
- (*)数据倾斜在MR中的哪一步产生的？
- (*)Hive 中有几种Join，都有什么作用？

## 七、Hive 如何处理小文件

- (*)Hive中小文件有哪些危害？
- (*)如何处理Hive中的小文件？

## 八、Hive的严格模式

- (*)介绍一下Hive的严格模式？

> - 不允许全表扫描所有分区，也就是查询**分区表**必须带有**分区过滤条件**。
> - 使用order by，必须使用limit。
> - 限制了笛卡尔积。
>
> 全局设置：
>
> - hive.mapred.mode = strict/nonstrict
> - 默认没有定义该变量，为非严格模式。
>
> 分开设置：
>
> - hive.strict.checks.no.partition.filter   
> - hive.strict.checks.orderby.no.limit 
> - hive.strict.checks.cartesian.product  

- Hive 的严格模式有几种，分别是什么？

> 参考上题；

## 九、Hive的分区

- (*)动态分区和静态分区的区别？
- 使用过动态分区吗？
- Hive3.x 中关于动态分区的新特性？

## 十、Hive的分桶

- 什么是 Hive 的分桶表？

> 见下；

- 说说对 Hive 桶表的理解？

> - 分桶表是对数据某个字段进行哈希取值，然后用哈希值对桶的个数取模，最后后放到不同文件中存储。
> - <span style='color:blue; font-weight:bold'>分桶表是分文件存储，分区表是分文件夹存储。</span>
>
> - 数据载到桶表时，会对字段取hash值，然后与桶的数量取模。把数据放到对应的文件中。物理上，每个桶就是表(或分区）目录里的一个文件，一个作业产生的桶(输出文件)和reduce任务个数相同。
>
> - 桶表专门用于抽样查询，是很专业性的，不是日常用来存储数据的表，需要抽样查询时，才创建和使用桶表。

## 十一、Hive数据的导入

- (*)你了解多少种Hive导入数据的方式？

> 主要用到的是这三种吧：
>
> - insert
> - load
> - put

- insert、load、put 都可以向 Hive 中导入数据，有什么区别吗？

> 

## 十二、Hive的数据类型

- (*)Hive 的集合数据类型有哪些？
- Hive 的集合数据类型有什么区别？
- 怎么构造 Hive 的集合数据类型？
- (*)Hive 的集合数据类型都分别怎么取值？

## 十三、Hive中四种排序

- (*)order by 和 sort by 的区别？
- 了解distribute by 和 cluster by 吗？

## 十四、Hive的存储和压缩

- (*)Hive 中的存储方式有哪些？

> TextFile（默认）、SequenceFile、ORC 、parquet

- Hive 中哪些存储方式是行式存储？哪些是列式存储？

> 行式存储：TextFile（默认）、SequenceFile
>
> 列式存储：ORC 、parquet

- (*)Hive 中的压缩方式，你了解哪些？

> 其实就是MR中的压缩方式：
>
> - gzip
> - bzip2
> - LZO
> - snappy

- (*)gzip 和 bzip2 有啥区别？

> 

- LZO 和 snappy 有啥区别？

> 

## 十五、Hive中的参数

- (*)说几个你了解的 Hive 中的参数？









### Hive 自定义函数

UDF ： GenericUDF             /dʒəˈnerɪk/    抽象类

```java
public class MyUDAF extends GenericUDF {

    @Override
    public ObjectInspector initialize(ObjectInspector[] arguments) throws UDFArgumentException {
        return null;
    }

    @Override
    public Object evaluate(DeferredObject[] arguments) throws HiveException {
        return null;
    }

    @Override
    public String getDisplayString(String[] children) {
        return null;
    }
}
```

UDTF ： GenericUDTF           抽象类

```java
public class MyUDAF extends GenericUDTF {
    
    @Override
    public void process(Object[] args) throws HiveException {
        
    }

    @Override
    public void close() throws HiveException {
        
    }
}
```

<span style='color:blue; font-weight:bold'>自定义函数的过程</span>

- 创建一个maven工程

- 导入依赖

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.apache.hive</groupId>
          <artifactId>hive-exec</artifactId>
          <version>3.1.2</version>
      </dependency>
  </dependencies>
  ```

- 创建一个类，继承GenericUDF（抽象类）

  ```java
  // 写java代码
  
  // 写完了
  ```

- 打jar包，上传服务器

在hive中使用自定义函数

- 将 jar 包添加到 hive 的 classpath  

  > <span style='color:red; font-weight:bold'>jar包放在`hive/lib`下，重启hive，就会扫面所有jar包</span>

  ```sql
  # 手动添加
  add jar /opt/module/hive-3.1.2/lib/hive-1-1.0-SNAPSHOT.jar
  ```

  > <span style='color:red; font-weight:bold'>上面手动添加的命令不好用，建议直接重启Hive</span>，再创建函数，再使用。

- 创建临时函数与开发好的 java class 关联  

  ```sql
  #      临时函数             函数名      类名
  create temporary function my_len as "com.atguigu.hive.MyStringLength";
  create temporary function my_len as "edu.lzu.hive.udf1.MyUDF";
  ```

- 在 HQL 中使用自定义的函数  

  ```sql
  >>> select my_len('joi');
  >>> 3
  ```

### Hive 如何解决数据倾斜

见下：

### Hive 如何处理小文件

见下：

### Hive的严格模式

- 

### Hive创建表

```sql
CREATE [EXTERNAL] TABLE [IF NOT EXISTS] table_name
[(col_name data_type [COMMENT col_comment], ...)]
[COMMENT table_comment]

[PARTITIONED BY (col_name data_type [COMMENT col_comment], ...)]
[CLUSTERED BY (col_name, col_name, ...)
[SORTED BY (col_name [ASC|DESC], ...)] INTO num_buckets BUCKETS]
[ROW FORMAT row_format]
[STORED AS file_format]
[LOCATION hdfs_path]
[TBLPROPERTIES (property_name=property_value, ...)]
[AS select_statement]
```

- `TBLPROPERTIES` 其他属性，比如压缩：`TBLPROPERTIES ('orc.compress' = 'snappy')`

- `[ROW FORMAT row_format]`

  ```sql
  row format delimited 
  	[FIELDS TERMINATED BY char] 
  	[COLLECTION ITEMS TERMINATED BY char]
  	[MAP KEYS TERMINATED BY char] 
  	[LINES TERMINATED BY char]
  | SERDE serde_name [WITH SERDEPROPERTIES (property_name=property_value,
  property_name=property_value, ...)]
  ```

  

### Hive的分区

- 创建分区表

  ```sql
  create table dept_partition(
      deptno int, 
      dname string, 
      loc string
  )
  partitioned by (day string)
  # partitioned by (day string, hour string)  # 二级分区
  row format delimited 
  	fields terminated by '\t';
  	
  # 注意：分区字段不能是表中已经存在的数据，可以将分区字段看作表的伪列。
  ```

- 加载数据

  ```sql
  load data local inpath '/dept.log' into table table1 partition(day='20200403');
  ```

- 增加分区

  ```sql
  alter table dept_partition add partition(day='20200404');
  # 增加多个分;
  alter table dept_partition add partition(day='20200404') partition(day='20200405');
  # 分区间不加','
  ```

- 删除分区

  ```sql
  alter table dept_partition drop partition(day='20200404')
  # 删除多个分区
  alter table dept_partition drop partition(day='20200404'),partition(day='20200404');
  # 分区间加','
  ```

- 查看表的分区

  ```sql
  show partitions talbe1;
  ```

- 把数据直接上传到分区目录上， 让分区表和数据产生关联的三种方式  <span style='color:blue; font-weight:bold'>（修复分区）</span>

  ```sql
  # 方法一：先创建分区表，再上传数据
  msck repair table partition_table_name;
  
  # 方法二：上传数据后，添加分区
  alter table partition_table_name 
  add partition(day='201709',hour='14');
  
  # 方法三：直接load到分区表中
  ```

- 静态分区，动态分区（不建议动态分区）

  ```sql
  insert into table1 partition(day='70') # 指明分区，属于静态分区
  select ...
  
  insert into table1 partition(day)      # 分区字段在select中，属于动态分区
  select ..., day from table2;
  # 上述语句，在动态分区是严格模式下，报错。
  ```

  > 两种修改方式：
  >
  > - 第一种：修改动态分区为非严格模式
  >
  >   ```sql
  >   hive.exec.dynamic.partition=false
  >   ```
  >
  > - 第二种：利用hive3.x新特性
  >
  >   ```sql
  >   insert into table1 # partition(day)   # 以查询的最后一个字段day为分区字段，属于动态分区
  >   select ..., day from table2;
  >   ```

- 动态分区的严格模式
  - 参数`hive.exec.dynamic.partition=true  ` 默认是true;
  
  > 动态分区默认是严格的，所以必须静态指明一个分区




### Hive的分桶

> <span style='color:blue; font-weight:bold'>分区针对的是数据的存储路径；分桶针对的是数据文件。  </span>

- 创建分桶表

  ```sql
  create table stu_buck(id int, name string)
  clustered by(id) into 4 buckets
  row format delimited fields terminated by '\t';
  ```

  > 分桶表的字段，必须是建表中的某一个字段，
  
  分桶字段的hash值求模



### Hive数据的导入导出

- insert into     元数据记录文件数，行数

  ```sql
  # 分区表的查询导入
  insert into table1 partition(day='')
  select ...
  ```

  

- load                元数据记录文件数

  ```sql
  load data [local] inpath 'path' [overwrite] into table student [partition (partcol1=val1,…)];
  ```

- put                  元数据什么都不记录



### Hive的数据类型

#### 集合数据类型

- array
  - 定义： `arr  array<string>`
  - 取值：`arr[0]`
  - 构造：`array(v1, v2, v3,...)   split()   collect_set()`
- map
  - 定义：`map1  map<int, string>`
  - 取值：`map1[key]`
  - 构造：`map(k1, v1, k2, v2, ...)`   `str_to_map(text, [delimiter1, delimiter2])`   delimiter1大分割，delimiter2分割每个K-V
- struct
  - 定义：`struct1  struct<id: int, name: string>`
  - 取值：`struct1.id`
  - 构造：`named_struct(name1, val1, name2, val2, ...)`

- 练习：

```sql
create table test(
    name string,
    friends array<string>,
    children map<string, int>,
    address struct<street:string, city:string>)
row format delimited 
fields terminated by ','
collection items terminated by '_'
map keys terminated by ':'
lines terminated by '\n';
```

```txt
songsong,bingbing_lili,xiao song:18_xiaoxiao song:19,hui long guan_beijing
yangyang,caicai_susu,xiao yang:18_xiaoxiao yang:19,chao yang_beijing
```



> 构造集合数据类型，见：[LanguageManual UDF - Apache Hive - Apache Software Foundation](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-ComplexTypeConstructors)
>
> > hive建表时，经常用到集合数据类型。

<img src="./images/002.jpg" alt="image" style="zoom:100%;" />

#### 基本数据类型

<img src="./images/001.jpg" alt="image" style="zoom:100%;" />



### Hive中四种排序

- Order By（全局排序，只有一个reducer） 

  - 

- Sort By（每个 Reduce 内部排序，分区内排序）  

  - 和distribute by 连用

- Distribute By（分区）  

  - map阶段，默认时**hash值**对**分区数**取余。

    > reduces的个数，为-1，自动划分
    >
    > 如果指定了reduces的个数，就按指定个数生成相应的分区，但数据量少时可能有空分区。

  - 自定义分区规则

  ```sql
  select * from table_name
  distribute by deptno sort by salary desc;
  
  
  select * from table_name
  distribute by deptno sort by deptno;  # 此时可以简化
  ```

> distribute by 和 sort by 连用，例如：
>
> - distribute by，部门分区
> - sort by，部门内薪水排序

- Cluster By  

  - 当distribute by ，sort by 的字段一样时，可以用cluster by

  - 排序只能是**升序**排序， 不能指定排序规则为 ASC 或者 DESC。  

    > 这种很少用，因为分区字段和排序字段一样，感觉很奇怪。

  ```sql
  select * from table_name
  distribute by deptno sort by deptno;  # 此时可以简化
  
  select * from table_name
  cluster by deptno;
  ```

```sql
# 查询结果写到文件中
insert overwrite local directory '/opt/module/data/sortby-result'
select * from emp sort by deptno desc;
```



### Hive的存储和压缩

#### 压缩

- gzip
  - 压缩比率高，
  - 压缩和解压速度一般
- bzip2
  - 压缩率贼高
  - 压缩和解压速度贼慢
- lzo
  - 压缩率一般
  - 解压和压缩比较快
- snappy
  - 压缩率一般
  - 解压和压缩比贼快

#### 存储

- textFile (默认)
- sequenceFile
- ORC
- parquet

> textFile、sequenceFile 是行式存储
>
> ORC、parquet 是列式存储

## Hive On Spark 调优

> 优化的前提一定是数据量很大，数据量很小没必要谈优化。
>
> 怎么看数据量
>
> ```sql
> desc formatted table_name; # 打印表的详细信息
> ```

### 集群规划





### 参数配置

- Yarn参数配置



- Spark参数配置





### Hive的计算引擎

[(88条消息) 大数据局执行引擎MR、Tez和Spark对比_tez和mr_清平乐的技术专栏的博客-CSDN博客](https://blog.csdn.net/ZZQHELLO2018/article/details/111593822)

#### 简介

- Hive引擎包括：默认MR、Tez、Spark

- 不更换引擎hive默认的是MR。

- `Hive on Spark`：Hive既负责存储元数据又负责SQL的解析优化，语法是HIver SQL语法，执行引擎变成了Spark，Spark负责采用RDD执行。

- `Spark on Hive`: Hive只负责存储元数据，Spark负责SQL解析优化，语法是Spark SQL语法，Spark负责采用RDD执行。

#### 区别

- MR 不擅长 DAG 计算，也就是多个应用程序存在依赖关系，后一个应用程序的输入依赖前一个的输出，这种情况下使用MR，会造成大量的IO操作。
- Tez和Spark都是以DAG方式处理数据。
- MR中，一个 SQL 转一个 mr 任务(job)。
- Spark中，一个会话是一个job，会话不结束，不会释放资源。





### Hive SQL  执行计划

- Explain



### 分组聚合优化

优化思路为map-side聚合。

所谓`map-side`聚合，就是在map端维护一个`hash table`，利用其完成分区内的部分聚合，然后将部分聚合的结果，发送至reduce端，完成最终的聚合。

<span style='color:blue; font-weight:bold'>map-side聚合能有效减少shuffle的数据量，提高分组聚合运算的效率</span>。

map-side 聚合相关的参数如下：

```sql
# 启用 map-side 聚合
set hive.map.aggr=true;  # (默认开启)

# hash table 占用 map 端内存的最大比例
set hive.map.aggr.hash.percentmemory=0.5;

# 用于检测源表是否适合 map-side 聚合的条数。
set hive.groupby.mapaggr.checkinterval=100000; # （10万）

# map-side 聚合所用的HashTable，占用map任务堆内存的最大比例，若超出该值，则会对 HashTable 进行一次flush。
set hive.map.aggr.hash.force.flush.memory.threshold=0.9;
```





###  Join优化

Hive拥有多种join算法，包括`common join`，`map join`，`SMB map join`

- **common join**

Map端负责读取参与join的表的数据，并按照关联字段进行分区，将其发送到Reduce端，Reduce端完成最终的join操作。

- **map join**

若大表和小表join，Map端就会缓存小表全部数据，然后扫描另外一张大表，在Map端完成关联操作。

要求表是：一大一小

```sql
# 启用 map join 自动转换
set hive.auto.convert.join = true;  # (默认为 true)
# 小表的阈值设置（默认 25M 以下认为是小表）：
set hive.mapjoin.smalltable.filesize = 25000000;    # (2千5百万 - 25M)

# common join 转map join 小表阈值
set hive.auto.convert.join.noconditionaltask.size = 10000000  # (1千万 - 10M)
```

- **Sort Merge Bucket Map Join**

解决的是：大表join大表

> 分区针对的是数据的存储路径；分桶针对的是数据文件。  
>
> <span style='color:red; font-weight:bold'>缺点</span>：准备工作比较麻烦，通用性不强，换张大表，需要再次分桶准备。

分桶表 - 分桶字段和桶数取模：Hive 的分桶采用<span style='color:blue; font-weight:bold'>对分桶字段的值进行哈希</span>，然后除以`桶的个数`求余的方式决定该条记录存放在哪个桶当中 。

若参与join的表均为分桶表，且关联字段为分桶字段，且分桶字段是有序的，且大表的分桶数量是小表分桶数量的整数倍。

此时，就可以以桶为单位，为每个Map分配任务了，Map端就无需再缓存小表的全表数据了，而只需缓存其所需的分桶。

```sql
# 启动Sort Merge Bucket Map Join优化
set hive.optimize.bucketmapjoin.sortedmerge=true;       # 默认fasle

# 使用自动转换 SMB Join 
set hive.auto.convert.sortmerge.join=true;              # 默认是true
```





### 数据倾斜优化

数据倾斜问题，通常是指参与计算的数据分布不均，即某个key或者某些key的数据量远超其他key，导致在shuffle阶段，大量相同key的数据被发往一个Reduce，进而导致该Reduce所需的时间远超其他Reduce，成为整个任务的瓶颈。

Hive中的数据倾斜常出现在`分组聚合`和`join操作`的场景中，下面分别介绍在上述两种场景下的优化思路。

- <span style='color:blue; font-weight:bold'>分组聚合导致数据倾斜 </span>

  > 根据分组字段进行分区

  - 启用 map-side 聚合  

    解释见：<span style='color:blue; font-weight:bold'>分组聚合优化</span>

  ```sql
  # 启用 map-side 聚合
  set hive.map.aggr=true;  # (默认开启)
  
  # hash table 占用 map 端内存的最大比例
  set hive.map.aggr.hash.percentmemory=0.5;
  
  # 用于检测源表是否适合 map-side 聚合的条数。
  set hive.groupby.mapaggr.checkinterval=100000; # （10万）
  
  # map-side 聚合所用的HashTable，占用map任务堆内存的最大比例，若超出该值，则会对 HashTable 进行一次flush。
  set hive.map.aggr.hash.force.flush.memory.threshold=0.9;
  ```

  - 启用 skew group by 优化

    当选项设定为 true，生成的查询计划会有两个 MR Job。 第一个 MR Job 中， Map 的输出结果会随机分布到 Reduce 中，每个 Reduce 做部分聚合操作，并输出结果，这样处理的结果是相同的 Group By Key 有可能被分发到不同的 Reduce 中，从而达到负载均衡的目的；第二个 MR Job 再根据预处理的数据结果按照 Group By Key 分布到 Reduce 中（这个过程可以保证相同的 Group By Key 被分布到同一个 Reduce 中），最后完成最终的聚合操作。  

  ```sql
  # 2 启用skew groupby优化
  set hive.groupby.skewindata = true;   # （默认关闭）
  ```

-  <span style='color:blue; font-weight:bold'>join导致数据倾斜</span>

  > 根据连接字段进行分区

  - 启用 map-side 聚合  
  - 启用 skew join 优化

  > 类似于 skew group by 分两个job，两次join。
  >
  > 需要注意的是，skew join 只支持 Inner Join。

  ```sql
  # 启用skew join优化
  set hive.optimize.skewjoin = true;  # 默认是false
  # 触发skew join的阈值，若某个key的行数超过该参数值，则触发
  set hive.skewjoin.key = 100000;   # (10万行)
  ```





### 任务并行度优化    map reduce个数

- Map个数

  Map端的并行度，也就是Map的个数。是由输入文件的`切片数`决定的。一般情况下，Map端的并行度无需手动调整。Map端的并行度相关参数如下：

  ```shell
  # blocksize 公式
  computeSliteSize(Math.max(minSize,Math.min(maxSize,blocksize))) = blocksize = 128M 
  ```

  > minSize = 1
  >
  > maxSize = long的最大值
  >
  > 降低map数，增大minSize
  >
  > 增加map数，减小maxSize

  ```sql
  # 可将多个小文件切片，合并为一个切片，进而由一个 map 任务处理  /kəmˈbaɪn/
  set hive.input.format = org.apache.hadoop.hive.ql.io.CombineHiveInputFormat;   # 默认就是
  
  # 一个切片的最大值
  set mapreduce.input.fileinputformat.split.maxsize = 256000000;
  set mapreduce.input.fileinputformat.split.minsize = 1;
  ```

- Reduce 个数

  Reduce端的并行度，相对来说，**更需要关注**。默认情况下，Hive会根据Reduce端输入数据的大小，估算一个Reduce并行度。但是在某些情况下，其估计值不一定是最合适的，故需要人为调整其并行度。Reduce并行度相关参数如下：

  ```sql
  # 指定Reduce端并行度，默认值为-1，表示用户未指定
  set mapreduce.job.reduces;
  # Reduce 端并行度最大值
  set hive.exec.reducers.max;  # 1009
  # 单个Reduce Task计算的数据量，用于估算Reduce并行度
  set hive.exec.reducers.bytes.per.reducer;  # 256M
  ```

  > Reduce端并行度的确定逻辑为，若指定参数`mapreduce.job.reduces`的值为一个非负整数，则Reduce并行度为指定值。
  >
  > 否则，Hive会自行估算Reduce并行度，估算逻辑如下：和`单个Reduce Task计算的数据量`以及`Reduce 端并行度最大值`的一个关系式。

- <span style='color:blue; font-weight:bold'>Job的并行度</span>

  ```sql
  # 参数hive.exec.parallel可以控制一个sql中多个可并行执行的job的运行方式，
  # 当hive.exec.parallel为true的时候,同一个sql中可以并行执行的job会并发的执行；
  # 而参数hive.exec.parallel.thread.number就是控制对于同一个sql来说同时可以运行的job的最大值,该参数默认为8.
  
  set hive.exec.parallel=true;
  set hive.exec.parallel.thread.number=32;
  ```

  



### 小文件合并优化

小文件合并优化，分为两个方面，分别是Map端输入的小文件合并，和Reduce端输出的小文件合并。

-  Map 端输入文件合并

  合并Map端输入的小文件，是指将多个小文件划分到一个切片中，进而由一个Map Task去处理。目的是防止为单个小文件启动一个Map Task，浪费计算资源。相关参数为：

  ```sql
  # 可将多个小文件切片，合并为一个切片，进而由一个 map 任务处理
  set hive.input.format = org.apache.hadoop.hive.ql.io.CombineHiveInputFormat;   # 默认就是
  
  # map-only 
  SET hive.merge.mapfiles = true;  # 默认true
  ```

- Reduce 端输出文件合并

  合并Reduce端输出的小文件，是指将多个小文件合并成大文件。目的是减少HDFS小文件数量。

  相关参数为：

  ```sql
  # 开启合并 Hive on Spark 任务输出的小文件
  set hive.merge.sparkfiles = true;           # 默认false
  
  # 开启合并 Hive on MR 任务输出的小文件
  set hive.merge.mapredfiles = true;          # 默认false
  
  # 合并大小， 默认 256M
  SET hive.merge.size.per.task = 268435456;
  # 当输出文件的平均大小小于该值时，启动一个独立的 map-reduce 任务进行文件 merge
  SET hive.merge.smallfiles.avgsize = 16000000;  # 默认 16M
  ```



