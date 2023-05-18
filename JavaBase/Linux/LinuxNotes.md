# LinuxNotes

## Remark

- sz  文件  ：将文件从linux传到win。
- rz -E 文件 ：将文件从win传到linux。
- tar -zxvf **压缩包** -C **解压到的目录**
- mv   oldfilename  newfilename   (重命名)
- vim 操作
  - 
- grep 
  - grep -i 内容   (包含内容)
  - grep -v 内容   (不包含内同)










## vim编译器

- 命令模型

  - :set nohlsearch   删除高亮

  - :set noreadonly   取消只读

  - :set number/nonumber   显示/取消行号

  - gg ：文件首行
  - G : 文件末尾  (shift + g)

  - <span style="color:blue; font-weight:bold">ctl+b</span> ：上翻一页

  - ctl+f ：下翻一页

  - ctl+u ：上翻半页

  - <span style="color:blue; font-weight:bold">ctl+d</span> ：下翻半页

  - yy  复制当前行

  - y n y  复制当前行及以下共n行

  - p 粘贴
  - 







## 虚拟机网络配置 - 重点

- P19 - P22 : 后续看



## 系统管理  

### Linux 中的进程和服务  

- 计算机中， 一个正在执行的程序或命令， 被叫做“进程”（process）。
- 启动之后一只存在、 常驻内存的进程， 一般被称作“服务”（service）。  

### systemctl （CentOS 7 版本-重点掌握）

> 值得说明的是：CentOS 6 用的是service 服务管理

- 基本语法

  ```
  systemctl start|stop|restart|status 服务名
  ```

- 服务所在文件地址

  ```
  /usr/lib/systemd/system
  ```

- systemctl 设置后台服务的自启配置  

  ```
  systemctl list-unit-files         （功能描述： 查看服务开机启动状态）
  systemctl disable service_name    （功能描述： 关掉指定服务的自动启动）
  systemctl enable service_name     （功能描述： 开启指定服务的自动启动）
  ```

- 系统运行级别  -  见讲义 《6.6 系统运行级别》

### 关机重启命令

在linux领域内大多用在服务器上，很少遇到关机的操作。毕竟服务器上跑一个服务是永无止境的，除非特殊情况下，不得已才会关机。  

> 见讲义 《6.8 关机重启命令》

> 经验技巧：
>
> Linux 系统中为了提高磁盘的读写效率， 对磁盘采取了“预读迟写”操作方式。当用户保存文件时，Linux 核心并不一定立即将保存数据写入物理磁盘中，而是将数据保存在缓冲区中，等缓冲区满时再写入磁盘，这种方式可以极大的提高磁盘写入数据的效率。但是，也带来了安全隐患，如果数据还未写入磁盘时，系统掉电或者其他严重问题出现，则将导致数据丢失。使用 <span style="color:blue; font-weight:bold">sync</span> 指令可以立即将缓冲区的数据写入磁盘。  

## 常用基本命令 - 重点

### 帮助命令  

- man 获得帮助信息  
  - man [命令和配置文件]     （功能描述： 获得帮助信息）

- help 获得 shell 内置命令的帮助信息

  一部分基础功能的系统命令是直接内嵌在 shell 中的， 系统加载启动之后会随着 shell一起加载， 常驻系统内存中。 这部分命令被称为“内置（built-in） 命令”； 相应的其它命令被称为“外部命令”。  

  - help 命令（功能描述： 获得 shell 内置命令的帮助信息）  
  - type 命令  (查看命令是内部还是外部命令)

### 文件目录类

- pwd : print working directory  (打印工作目录)
  - 功能描述： 显示当前工作目录的绝对路径

- ls : list 列出目录内容  

  - ls -a  可以查看隐藏文件

  - ls -l   功能和 ll 一样

  - ls -al

    每行列出的信息依次是：文件类型与权限  链接数  文件属主  文件属组  文件大小(byte)  建立或最近修改的时间  文件名

    

- cd : change directory 切换路径  
  - cd / cd ~     回到自己的家目录
  - cd -              回到上次所在的目录
  - cd -p           跳转到实际物理路径， 而非快捷方式路径
  - cd 相对路经 / 绝对路经
  - cd ..             回到上一级目录
  
- mkdir : make directory 建立目录  
  - <span style="color:blue; font-weight:bold">mkdir -p</span>   创建多层目录
  
- ~~rmdir~~ : remove directory 移除目录(删除一个空的目录) - 不经常用

- touch 创建空文件  
  - touch 文件名

- cp 复制文件或目录  

  - cp source dest         功能描述： 复制source文件到dest

  - cp -r   递归复制整个文件夹

    > 经验技巧 - 强制覆盖不提示的方法： \cp  

- rm 删除文件或目录  

  - rm -rf deleteFile      功能描述： 递归删除目录中所有内容

    -r    递归删除

    -f    强制执行删除

    -v    显示指令的详细执行过程

- mv 移动文件与目录或重命名  

  - mv oldNameFile newNameFile       （功能描述： 重命名）  
  - mv /temp/movefile /targetFolde    （功能描述： 移动文件）

- cat  more  less    查看文件内容
  
  > cat less 用的多，more 用的少
  
  - cat -n   显示内容的时候，显示行号， 包括空行。
  
- echo 输出内容到控制台  

  - echo  内容
  - echo  内容  >>  文件     (将内容追加到一个文件中)
  - cat   文件1  >>  文件2   (将文件1的内容追加到文件2中)

- head  显示文件头部内容

  - head 文件           （功能描述： 查看文件头10行内容）
  - <span style="color:blue; font-weight:bold">head -n</span> 5 文件   （功能描述： 查看文件头5行内容， 5可以是任意行数）


- tail 输出文件尾部内容  

  - tail 文件           （功能描述： 查看文件尾部10行内容）

  - tail -n 5 文件   （功能描述： 查看文件尾部5行内容， 5可以是任意行数）

  - <span style="color:blue; font-weight:bold">tail -f/F</span> 文件    （功能描述： 实时追踪该文档的所有更新） 

    > F 比 f 好用，一般用 F   - ？？？？？？？？？？？？？？

- `>` 输出重定向和 `>> `追加  
  - ls -l > 文件                 （功能描述：列表的内容写入文件 a.txt 中（覆盖写））  
  -  ls -l >> 文件              （功能描述： 列表的内容追加到文件 a.txt 的末尾）
  - cat 文件 1 > 文件 2   （功能描述： 将文件 1 的内容覆盖到文件 2）
  - cat 文件 1 >> 文件 2 （功能描述： 将文件 1 的内容追加到文件 2）
  - echo 内容 > 文件        覆盖
  - echo 内容 >> 文件      追加

- ln 软链接 
- history 查看已经执行过历史命令  
  - history

### 时间日期类



### 用户管理命令



### 用户组管理命令



### 文件权限类

#### 文件属性

> Linux系统是一种典型的多用户系统， 不同的用户处于不同的地位， 拥有不同的权限。为了保护系统的安全性， Linux系统对不同的用户访问同一文件（包括目录文件） 的权限做了不同的规定。 在Linux中我们可以使用ll或者ls -l命令来显示一个文件的属性以及文件所属的用户和组。  

- 从左到右的 10 个字符表示， 如图所示  

  <img src="./images/001.jpg" alt="image" style="zoom:70%;" />

  > 如果没有权限， 就会出现减号[ - ]而已。 从左至右用0-9这些数字来表示: 

  - 0 首位表示类型
    在Linux中第一个字符代表这个文件是目录、 文件或链接文件等等
    <span style="color:blue; font-weight:bold">\-</span> 代表文件，<span style="color:blue; font-weight:bold">d</span> 代表目录，<span style="color:blue; font-weight:bold">l</span> 链接文档(link file)
  - 第1-3位确定属主（该文件的所有者） 拥有该文件的权限。 ---User  
  - 第4-6位确定属组（所有者的同组用户） 拥有该文件的权限， ---Group  
  - 第7-9位确定其他用户拥有该文件的权限 ---Other  

- rwx 作用文件和目录的不同解释 

  - 作用到文件
    - r 代表可读(read)：可以读取， 查看。
    - w 代表可写(write)：可以修改，但是不代表可以删除该文件，删除一个文件的前提条件是对该文件所在的目录有写权限，才能删除该文件。
    - x 代表可执行(execute)：可以被系统执行。
  - 作用到目录：
    - r 代表可读(read)：可以读取，ls查看目录内容
    - w 代表可写(write)：可以修改，目录内创建文件+删除文件+重命名该目录
    - x 代表可执行(execute)：可以进入该目录  

#### 一些命令

- <span style="color:blue; font-weight:bold">chmod 改变权限</span>

  <img src="./images/002.jpg" alt="image" style="zoom:70%;" />

  - 第一种方式变更权限
    ```shell
    chmod {ugoa}{+-=}{rwx} 文件或目录
    # u:所有者 g:所有组 o:其他人 a:所有人(u、 g、 o 的总和)
    ```

  - 第二种方式变更权限
    ```shell
    chmod 421 文件或目录
    # r=4 w=2 x=1 rwx=4+2+1=7
    ```

- chown 改变所有者 
  - chown [选项] [最终用户] [文件或目录]        （功能描述： 改变文件或者目录的所有者）  
  - 选项 -R ：递归操作    (将整个目录内的文件都修改)

- chgrp 改变所属组 
  - chgrp [最终用户组] [文件或目录] （功能描述： 改变文件或者目录的所属组）

### 搜索查找类

- find 查找文件或者目录

  find 指令将从指定目录向下递归地遍历其各个子目录， 将满足条件的文件显示在终端。

  - find [搜索范围] [选项] 

    | 选项            | 功能                                                         |
    | --------------- | ------------------------------------------------------------ |
    | -name<查询内容> | 按照指定的文件名查找模式查找文件                             |
    | -user<用户名>   | 查找属于指定用户名所有文件                                   |
    | -size<文件大小> | 按照指定的文件大小查找文件,单位为: <br>b —— 块（512 字节） <br/>c —— 字节 <br/>w —— 字（2 字节） <br/>k —— 千字节 <br/>M —— 兆字节 <br/>G —— 吉字节 |

  - 根据名称查找指定目录下的*.txt文件

    ```shell
    find xiyou/ -name "*.txt"
    ```

  - 查找/home/目录下， 用户名称为-user的文件  

    ```shell
    find /home/ -user atguigu
    ```

  - 在/home目录下查找大于200m的文件（+n 大于 -n小于 n等于）  

    ```shell
    find /home -size +204800
    ```

- locate 快速定位文件路径

  > locate 指令利用事先建立的系统中所有文件名称及路径的 locate 数据库实现快速定位给定的文件。 
  >
  > Locate 指令无需遍历整个文件系统，查询速度较快。 为了保证查询结果的准确度，管理员必须定期更新 locate 时刻。  

- <span style="color:blue; font-weight:bold">grep 过滤查找及“|”管道符</span>

  - 管道符， “|”， 表示将前一个命令的处理结果输出传递给后面的命令处理  

  - grep 选项 查找内容 源文件  

  - 选项：-n   显示匹配行及行号。

  - 案例实操

    ```shell
    # 查找某文件在第几行
    ls | grep -n test
    
    ls | grep 内容
    # 内容可以是一部分字段，直接模糊查找
    ```

### 压缩解压类

- tar打包

  - tar [选项] xxx.tar.gz 将要打包的内容

  - 选项内容

    | 选项 | 功能               |
    | ---- | ------------------ |
    | -c   | 产生.tar打包文件   |
    | -v   | 显示详细信息       |
    | -f   | 指定压缩后的文件名 |
    | -z   | 打包的同时压缩     |
    | -x   | 解压.tar包         |
    | -C   | 解压到指定目录     |

    - **压缩**多个文件  

      tar   **-zcvf**   houma.tar.gz   houge.txt bailongma.txt houge.txt

    - **压缩**目录  

      tar   **-zcvf**   xiyou.tar.gz   xiyou/  

    - **解压**到当前目录  

      tar   **-zxvf**   houma.tar.gz  

    - <span style="color:blue; font-weight:bold">解压到指定目录</span>

      tar   **-zxvf**   xiyou.tar.gz   **-C**   /opt  

- 其他见讲义 《7.8 压缩和解压类 》

### 磁盘查看和分区



### 进程管理

> 进程是正在执行的一个程序或命令，每一个进程都是一个运行的实体，都有自己的地址空间，并占用一定的系统资源。  

- ps 查看当前系统进程状态  

  - ps aux | grep xxx    （功能描述： 查看系统中所有进程）

  - ps -ef | grep xxx      （功能描述： 可以查看子父进程之间的关系）

    | 选项 | 功能                                        |
    | :--: | ------------------------------------------- |
    |  a   | 列出带有终端的所有用户的进程                |
    |  x   | 列出当前用户的所有进程， 包括没有终端的进程 |
    |  u   | 面向用户友好的显示风格                      |
    |  -e  | 列出所有进程                                |
    |  -u  | 列出某个用户关联的所有进程                  |
    |  -f  | 显示完整格式的进程列表                      |

  - ps aux 显示信息说明

    - USER：该进程是由哪个用户产生的
    - PID：进程的 ID 号
    - %CPU：该进程占用 CPU 资源的百分比， 占用越高， 进程越耗费资源；
    - %MEM：该进程占用物理内存的百分比， 占用越高， 进程越耗费资源；
    - VSZ：该进程占用虚拟内存的大小， 单位 KB；
    - RSS：该进程占用实际物理内存的大小， 单位 KB；
    - TTY：该进程是在哪个终端中运行的。 对于 CentOS 来说， tty1 是图形化终端，
    - tty2-tty6 是本地的字符界面终端。 pts/0-255 代表虚拟终端。
    - STAT：进程状态。常见的状态有：R：运行状态、S：睡眠状态、T：暂停状态、Z：僵尸状态、s：包含子进程、l：多线程、+：前台显示
    - START：该进程的启动时间  
    - TIME：该进程占用 CPU 的运算时间， 注意不是系统时间
    - COMMAND：产生此进程的命令名  

  - ps -ef 显示信息说明

    - UID：用户 ID

    - PID：进程 ID

    - PPID：父进程 ID

    - C：CPU 用于计算执行优先级的因子。数值越大，表明进程是 CPU 密集型运算，执行优先级会降低；数值越小，表明进程是 I/O 密集型运算，执行优先级会提高

    - STIME：进程启动的时间

    - TTY：完整的终端名称

    - TIME：CPU 时间

    - CMD：启动进程所用的命令和参数  

    > 如果想查看<span style="color:blue; font-weight:bold">进程的 CPU 占用率和内存占用率</span>， 可以使用 <span style="color:red; font-weight:bold">ps aux</span>;
    > 如果想查看<span style="color:blue; font-weight:bold">进程的父进程 ID</span> 可以使用 <span style="color:red; font-weight:bold">ps -ef</span>;

- kill 终止进程
  - <span style="color:blue; font-weight:bold">kill  -9 进程号</span>    （功能描述： 通过进程号杀死进程，-9 表示强迫进程立即停止）
  - killall  进程名称 （功能描述： 通过进程名称杀死进程， 也支持通配符， 这在系统因负载过大而变得很慢时很有用）

- pstree 查看进程树

  - pstree [选项]  

    - -p   显示进程的 PID
    - -u   显示进程的所属用户

    ```shell
    pstree -p
    pstree -u
    ```

- top 实时监控系统进程状态  

  见讲义  《7.10.4   top 实时监控系统进程状态  》

- netstat 显示网络状态和端口占用信息

  《7.10.5  netstat 显示网络状态和端口占用信息》

### crontab系统定时任务

- 重新启动 crond 服务  
  - systemctl  restart  crond

- crontab 定时任务设置

  - crontab [选项] 

    | 选项 | 功能                            |
    | ---- | ------------------------------- |
    | -e   | 编辑 crontab 定时任务           |
    | -l   | 查询 crontab 任务               |
    | -r   | 删除当前用户所有的 crontab 任务 |

- <span style="color:blue; font-weight:bold">执行 `crontab -e`</span>

  - 进入 crontab 编辑界面，会打开 vim 编辑你的工作。 

    \* * * * * 执行的任务

  |   项目    | 含义                 | 范围                              |
  | :-------: | -------------------- | --------------------------------- |
  | 第一个“*” | 一小时当中的第几分钟 | 0-59                              |
  | 第二个“*” | 一天当中的第几小时   | 0-23                              |
  | 第三个“*” | 一个月当中的第几天   | 1-31                              |
  | 第四个“*” | 一年当中的第几月     | 1-12                              |
  | 第五个“*” | 一周当中的星期几     | 0-7 （ 0 和 7 都 代 表 星 期 日） |

  - 特殊符号

  | 特殊符号 | 含义                                                         |
  | :------: | ------------------------------------------------------------ |
  |    *     | 代表任何时间。 比如第一个“ *” 就代表一小时中每分钟 都执行一次的意思。 |
  |    ,     | 代表不连续的时间。<br>比如“ 0 8,12,16 * * * 命令”，就代表 在每天的 8 点 0 分，12 点 0 分，16 点 0 分都执行一次命令 |
  |    -     | 代表连续的时间范围。 比如“0 5 * * 1-6 命令”， 代表在 周一到周六的凌晨 5 点 0 分执行命令 |
  |   */n    | 代表每隔多久执行一次。 比如“*/10 * * * * 命令”， 代表每隔 10 分钟就执行一遍命令 |

  - 特定时间执行命令

  |       时间        | 含义                                                         |
  | :---------------: | ------------------------------------------------------------ |
  | 45 22 * * * 命令  | 每天 22 点 45 分执行命令                                     |
  |  0 17 * * 1 命令  | 每周 1 的 17 点 0 分执行命令                                 |
  | 0 5 1,15 * * 命令 | 每月 1 号和 15 号的凌晨 5 点 0 分执行命令                    |
  | 40 4 * * 1-5 命令 | 每周一到周五的凌晨 4 点 40 分执行命令                        |
  | */10 4 * * * 命令 | 每天的凌晨 4 点， 每隔 10 分钟执行一次命令                   |
  | 0 0 1,15 * 1 命令 | 每月 1 号和 15 号， 每周 1 的 0 点 0 分都会执行命令。<br>注 意： 星期几和几号最好不要同时出现， 因为他们定义的都 是天。 非常容易让管理员混乱。 |

  - 案例实操  

    ```shell
    # 每隔 1 分钟， 向/root/bailongma.txt 文件中添加一个 11 的数字
    */1 * * * * /bin/echo ”11” >> /root/bailongma.txt
    ```



## 软件包管理





## 克隆虚拟机

> P20 

- 从现有虚拟机(<span style="color:red; font-weight:bold">关机状态</span>)克隆出新虚拟机， 右键选择管理=>克隆。

- 点击下一步

- 选择 虚拟机中的当前状态 或者 现有快照

- 选择<span style="color:red; font-weight:bold">创建完整克隆</span>

- 设置<span style="color:red; font-weight:bold">虚拟机名称</span>及<span style="color:red; font-weight:bold">存储位置</span>

- 等等等……等待克隆完成

- 开机修改系统相关配置  -  重要

  > 注意：使用 <span style="color:red; font-weight:bold">root 用户</span>

  - 修改 IP 地址

    ```shell
    vim /etc/sysconfig/network-scripts/ifcfg-ens33
    
    # 网络服务的重启
    systemctl restart network
    systemctl restart NetworManager
    ```

  - 修改主机名  

    ```shell
    vim /etc/hostname    （需要重启reboot）
    
    hostnamectl set-hostname 主机名
    ```

  > LINUX系统：vim /etc/hosts    hosts 配置文件（主机名称映射）
  >
  > WINDOW系统：C:\Windows\System32\drivers\etc\hosts      hosts 配置文件





## SHELL编程

- `ps -ef | grep file_to_kafka | grep -v grep | awk '{print \$2}' | xargs -n1 kill -9`
  - awk 把字符串按照空格切割
  - xargs -n1 反向传参
  -  `\$2` 表示获取当前结果的第二个结果

```shell
#!/bin/bash

$(  命令  ) ：命令替换(系统函数调用)，将命令的结果看作“字符”



```

### 变量





### 运算符





### 条件判断





### 流程控制









### read 读取控制台输入

基本语法  

- read   (选项)   (参数)  

  - 选项：

    -p： 指定读取值时的提示符；

    -t：  指定读取值时等待的时间（秒） 如果  -t  不加表示一直等待参数

  - 参数：

    变量： 指定读取值的变量名  

```shell
#!/bin/bash

read -t 10 -p "请输入您的芳名：" name
echo "welcome, $name"

```

### 函数

#### 系统函数  

1、basename

基本语法 - **将最后一个/后的字符串剪切出来**

- basename   [ string/pathname ]   [suffix] 

  功能描述： basename 命令会删掉所有的前缀包括最后一个（‘/’） 字符， 然后将字符串显示出来。

  - basename 可以理解为取路径里的文件名称

  - 选项：
    suffix 为后缀；如果 suffix 被指定了， basename 会将 pathname 或 string 中的 suffix 去掉。  

```shell
basename /root/scripts/hello.sh
# 输出：hello.sh

basename /root/scripts/hello.sh .sh
# 输出：hello
```

2、dirname 

基本语法 - **将最后一个/前的字符串剪切出来**

- dirname 文件绝对路径 

  功能描述： 从给定的包含绝对路径的文件名中去除文件名（非目录的部分） ， 然后返回剩下的路径（目录的部分） 

  - dirname 可以理解为取文件路径的绝对路径名称  

```shell
dirname /root/scripts/hello.sh
# 输出：/root/scripts/

dirname /root/scripts/nsoghoa
# 输出：/root/scripts/
```

3、综合案例

```shell
#!/bin/bash

echo '===============$n================='
# echo "script name : $0"
# echo "script name : $(basename $0)"
echo "script name : $(basename $0 .sh)"
# 这样写的，是绝对安全的，因为dirname只是一个剪切功能
echo "script path : $(cd $(dirname $0); pwd)"
# echo "script path : $(dirname $0)"
echo 1st parameter : $1
echo 2nd parameter : $2


echo '===============$#================='
echo parameter numbers : $#

echo '==========$*=========='
echo $*

echo '==========$@=========='
echo $@
```

#### 自定义函数

基本语法

```shell
[ function ] funname[()]
{
	Action;
	[return int;]
}  
```

经验技巧

（1） 必须在调用函数地方之前， 先声明函数， shell 脚本是逐行运行。 不会像其它语言一样先编译。

（2） 函数返回值， 只能通过$?系统变量获得， 可以显示加： return 返回， 如果不加， 将以最后一条命令运行结果， 作为返回值。 

​          return 后跟数值 n(0-255)  

案例实践

```shell
#!/bin/bash

function add(){
        s=$[$1+$2]
        echo "$1 + $2 = $s"
}

read -p "请输入第一个整数：" a
read -p "请输入第二个整数：" b

add $a $b
```

### 综合案例



























