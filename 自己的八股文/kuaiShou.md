[(89条消息) 2023秋招——快手数据研发一、二面面经_柳小葱的博客-CSDN博客](https://blog.csdn.net/weixin_48077303/article/details/126716362)



##### 1、自我介绍一下

##### 2、Hive的存储引擎了解哪些？例如常用默认的textfile，还了解哪些？orcfile。textfile和orcfile有什么区别？行列存储？是行存储还是列存储？

- 存储格式：

TEXTFILE 、SEQUENCEFILE、(行)

ORC、PARQUET(parquet)    （列）

- 压缩格式：

gzip 压缩率高，解压和压缩速度一般，

bzip2 压缩率贼高，解压和压缩速度太慢

lzo 压缩率一般，压缩和解压速度较快

snappy 压缩率一般，压缩和解压速度贼快。

```
ods                textfile + gzip       （gzip压缩率高）

DIM  DWD DWS       orc+snappy            （snappy）
    
ADS                textfile 默认，不压缩
```



##### 3、Hive的order by和sort by有什么区别？以及distribute by 、cluster By  









##### 4、Hive的udf、udaf和udtf了解过吗？自己有没有写过udf？









##### 5、【SQL题】 一个login_in表，userid、login_time、ip，表数据量比较大，千万级甚至上亿级别。取出最近10条登录的数据（考虑上数据量巨大）。常规做法全局order by limit；对userid或ip用窗口函数做分区加编号再过滤，分区内login_time倒序排，之后再全局order by。怎么样用sort by的方式去实现？回答distribute by + sort by。

[(88条消息) Hive中Order by和Sort by的区别是什么?_Soyoger的博客-CSDN博客](https://soyoger.blog.csdn.net/article/details/79803882?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1-79803882-blog-79868329.235^v32^pc_relevant_yljh&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1-79803882-blog-79868329.235^v32^pc_relevant_yljh&utm_relevant_index=2)







##### 6、Hive表的内部表和外部表有什么区别？实际实习工作中有用到过吗？用的是内部表还是外部表？

内部表：

外部表：







##### 7、Hive中grouping sets、with cube等这些高级的函数有没有使用过？ 没有



8、Hive的优化点，怎么去写更优的Hive语句，如何去优化？在实习工作中有没有遇到过？





9、数据倾斜的解决方案？





##### 10、【SQL题】还是login_in表，统计登录的总条数和登录的总人数，考虑下数据量很大，一个人可能有多条登录数据。





##### 11、介绍一下HBase的一些特性。在删除HBase中的一个数据的时候，它什么时候真正的进行删除呢？当你进行删除操作，它是立马就把数据删除掉了吗？   不会





##### 12、【SQL题】还是login_in表，算总人数的时候会在Hive里面起几个MR。



13、Java平常写的多么？Java的HashMap和HashTable有什么区别？线程安全的Map是什么？实际用过ConcurrentHashMap吗？
14、抽象类与接口的区别？方法的默认实现？接口中可以定义常量么？
15、Java1.8的新特性你了解么？stream流了解吗？
16、Java线程写过吗？怎么写一个线程？实际项目中写过么？
17、线程池了解过吗？
18、ArrayList和LinkedList都用过吗？介绍一下？
19、现在有一个String的对象“ABCD”，如何将这个字符串反转生成一个新的字符串。
20、MySQL用过吧，它有什么引擎？InnoDB和MyISAM有什么区别？
21、MyISAM的一些索引，单列索引、组合索引、主键、唯一索引都什么区别？
22、Shell中统计一个文件的行数用什么指令？在Shell脚本中获取传入参数的总个数？
23、Shell中压缩一个文件夹，用什么指令？
24、SQL题，还是login_in表，加一个pay_info表，字段包括userid，pay_time，payment_amout。要求查出登录了但是未支付的总人数，一个用户也会有多条支付的数据。注意多条重复关联去重问题。
25、where和having有什么区别？
26、有了解过Flume、Kafka吗？
27、你是保研的还是考研的？
28、你的方向是大数据哪一块？离线还是数仓？







