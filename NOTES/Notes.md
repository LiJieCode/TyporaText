#  Notes

## 常见字符集(Charset)

[一听就懂字符集、ASCII、GBK、UTF-8、Unicode、乱码、字符编码、解码问题的讲解_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1xD4y1y7yc/?spm_id_from=333.337.search-card.all.click&vd_source=5bc191bb37a56c995b0901fd3ad1baa5)

### 字符编码

​          

- **ASCII**字符集 0-127

  - **0**000 0000  -  **0**111 1111（第一位始终是0）
  - 只有英文，数字，符号，每一个占1个字节。

- **ISO-8859-1**字符集

  - 拉丁码表，别名：latin-1，用于显示欧洲使用的语言，包括荷兰，丹麦，德语，意大利语，西班牙语等
  - ISO-8859-1使用单字节编码，兼容ASCII编码

- **GBK**字符集(汉字内码扩展规范，国标)

  - 汉字编码字符集，包含了2万多个汉字等字符，GBK中的每一个中文字符编码成两个字节的形式存储。

    2个字节共16位

  - 注意：GDK兼容了ASCII字符集。英文和数字占一个字节，汉字占两个字节。

  - GDK规定：汉字的子一个字节的第一位必须是1。

    例如：我a你    编码： 1xxx xxxx xxxx xxxx 0xxx xxxx 1xxx xxxx xxxx xxxx

    ​                          解码：<span style="color:blue">1xxx xxxx xxxx xxxx</span> <span style="color:red">0xxx xxxx</span> <span style="color:blue">1xxx xxxx xxxx xxxx</span>

  - 汉字占2个字节，英文数字占1个字节。

- **Unicode**字符集(统一码，也叫万国码)

  - Unicode是国际组织制定的，可以容纳世界上所有的文字，符号的字符集。

  - UTF-32：用4个字节表示一个字符。（没有被接纳）

  - **UTF-8**字符集 —— <span style="color:red; font-weight:bold">最常用，最重要的一个字符集</span>

    - UTF-8是Unicode字符集的一种编码方案，采取<span style="color:blue; font-weight:bold">可变长编码方案</span>，共分四个长度区：1个字节，2个字节，3个字节，4个字节

    - 英文字符、数字等只占1个字节（兼容标准ASCII编码），汉字字符占用3个字节

    - UTF-8，编码和解码规则：

      <img src="./images/001.jpg" alt="image" style="zoom: 80%;" />

    - 注意：技术人员在开发时应该使用UTF-8编码。

    - 汉字占3个字节，英文数字占1个字节。

> 注意1：字符集编码时使用的字符集，和解码时使用的字符集必须一致，否则出现乱码。
>
> 注意2：英文、数字一般不会乱码，因为很多字符集都会兼容ASCII编码。









## SQL-创造数据

[我做了个小工具，帮你提升100倍开发效率！_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1eP411N7B7/?spm_id_from=333.1007.tianma.3-1-7.click&vd_source=5bc191bb37a56c995b0901fd3ad1baa5)

[代码生成 - SQL之父 (sqlfather.com)](https://www.sqlfather.com/)





## 端口号总结

> 内部通信端口：客户端访问
>
> Web服务端口：网页访问

- hdfs Web端口：9870（50070 hadoop2.x）
- 2nn web端访问地址 ：9868（50090 hadoop2.x）
- Yarn Web端口：8088
- 历史服务器 Web端口：19888
- hdfs 内部通信端口：8020、9000、9820(hadoop3.x 独有)
- Yarn 内部通信端口：8032
- 
- zookeeper 内部通信端口：2181
- kafka 内部通信端口：9092
- Hbase Web端口：16010
- Hive 内部通信端口：9083
- Flink Web端口：8081





## 各框架的配置文件

- 搭建集群顺序

  - hadoop / java

  - zookeeper

  - flume
  - kafka

  - hive / mysql

  > kafka 依赖于 zookeeper，故要先配置zookeeper。

- 配置文件

  - hadoop
    - etc/hadoop/
  - kafka
    - config/server.properties

  - hive

- 各框架启动

  - hadoop 

    `myhadoop.sh start`

  - zookeeper

    `myzookeeper.sh start`

  - kafka - 先启动zookeeper；

    `mykafka.sh start`

  - hbase - 不需要写脚本，需要先启动hadoop、zookeeper

    `start-hbase.sh`



## 服务相关

- 防火墙 ：firewalld

  ```shell
  systemctl start/stop/status/restart firewalld
  systemctl start/stop/status/restart firewalld.service
  
  # 开机自启动否？
  systemctl enable/disable firewalld.service
  ```

- 网络 ：NeteorkManager - CentOS7    (CentOS7之前是：network)

  ```shell
  systemctl start/stop/status/restart NeteorkManager 
  
  # 开机自启动否？
  systemctl enable/disable NeteorkManager 
  ```

  



