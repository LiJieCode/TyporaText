# SparkKernelNotes

## 环境准备







## 组件通信







## 应用程序的执行



### Spark 任务调度概述  

一个 Spark 应用程序包括 Job、 Stage 以及 Task 三个概念：

-  Job 是以 Action 方法为界，遇到一个 Action 方法则触发一个 Job；
- Stage 是 Job 的子集，以 RDD 宽依赖(即 Shuffle)为界，遇到 Shuffle 做一次划分；
- Task 是 Stage 的子集，以并行度(分区数)来衡量，分区数是多少，则有多少个 task。

Spark 的任务调度总体来说分两路进行，一路是 Stage 级的调度，一路是 Task 级的调度，  





Driver 初始化 `SparkContext`过程中，会分别初始化 `DAGScheduler`、 `TaskScheduler`、`SchedulerBackend`以及 `HeartbeatReceiver`，并启动 `SchedulerBackend` 以及 `HeartbeatReceiver`。

`SchedulerBackend` 通过 `ApplicationMaster` 申请资源，并不断从 `TaskScheduler` 中拿到合适的 Task 分发到 Executor 执行。 

`HeartbeatReceiver` 负责接收 Executor 的心跳信息，监控 Executor的存活状况，并通知到 TaskScheduler。  

['hɑ:tbi:t]



## Shuffle 

- 存在宽依赖（Shuffle 依赖）就会shuffle

- Shuffle 必须会落盘

  > Shuffle 必须会落盘，只是落盘数据多少的问题，
  >
  > 优化也就在这里，我们要在不影响最终结果的情况下，尽量让shuffle落盘的数据量小，IO的效率就提升了。
  >
  > 
  >
  > 算子如果存在预聚合功能，就可以减少shuffle落盘数据量，就可以提升shuffle性能

- shuffle 发展

  - 普通的HashShuffle：下游有多少个task， 上游的每个task，就会落盘多少个文件。（M1*N）

  - 优化后的HashShuffle：一个Executor中的多个task的落盘文件放一起，（M2*N）

  - SortShuffle：每个Executor只落盘一个文件（这里的一个文件指定是最后落盘一个文件，中间会有多个临时文件，最后合并成这样的一个大文件），同时还会生成一个索引文件。下游task去读取文件时，先读取索引文件，找的属于自己数据的位置，在去实际的数据文件中读取相应位置的数据。

    sortshuffle解决了一些小文件的问题，但是他会进行sort排序，多多少少对行性能也会有影响。

    所以其实，某些情况下，对于一些简单的操作，可以不用排序，那就是

  - bypass SortShuffle：

    下游task要小于200；不能有预聚合算子；

    通过hash定位。

    此时上游 task 会为每个 下游的 task 都创建一个临时磁盘文件，并将数据按 key 进行hash ，然后根据 key 的 hash 值，将 key 写入对应的磁盘文件之中。

    （当然，写入磁盘文件时也是先写入内存缓冲，缓冲写满之后再溢写到磁盘文件的。）最后，同样会将所有临时磁盘文件都合并成一个磁盘文件，并创建一个单独的索引文件。  







