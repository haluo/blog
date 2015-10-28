
### 前言
前段时间将公司日志分析系统的实时分析由storm迁移到了spark-streaming,定时任务也全部换成了spark来计算。已经在线上跑了几个月
总体还算稳定。<br/>
公司用到spark版本是CDH的1.3.0。这里不讲spark的安装过程<br/>
demo 由java来实现 并没有选择原生的scala 代码：https://github.com/haluo/SparkDemoJava<br/>

### 简介

Spark是继Hadoop之后的新一代大数据分布式处理框架：
Apache顶级项目
2014大数据领域最活跃开源项目
应用  百度/阿里/腾讯/京东。。。

核心组件：
<img src="http://7xkx1t.com1.z0.glb.clouddn.com/blogspark1.png">
Spark core 用于Batch数据处理（对应于hadoop的map reduce）<br/>
Spark streaming用于处理实时的流数据(对应于storm)<br/>
Spark SQL通过JDBC API将Spark数据集暴露出去，而且还可以用传统的BI和可视化工具在Spark数据上执行类似SQL的查询<br/>
Spark MLlib: Spark机器学习库<br/>
Spark GraphX:是用于图计算和并行图计算的 新的（alpha）Spark API。<br/>

Spark core相对于hadoop mr:

1.基于内存的迭代计算，中间结果缓存在内存中<br/>
	-hadoop mr Shuffle 会有大量磁盘IO<br/>
	<img src="http://7xkx1t.com1.z0.glb.clouddn.com/blogspark2.png">
2.丰富的API（map reduce, group by ,sort by 等） 满足   不同的需求,编程更简单<br/>
	-hadoop mr只有map 和 reduce 太抽象<br/>
3. 分区相同的转换操作构成流水线在同一个task中完成，分区不同的转换需要shuffle.需要等前面的任务完成后才可以开始。<br/>
	- hadoop mr的所有reduce都需要等map执行完成后才能开始<br/>

Spark streaming相对于storm:

1.吞吐量高<br/>
2.将流拆成小的batch数据来处理流数据,实时性没storm好<br/>

###核心机制
Spark建立在统一抽象的RDD数据模型之上，使得它可以以基本一致的方式应对不同的大数据处理场景。

RDD：

弹性分布式数据集，可以让用户显式地将数据存储到磁盘和内存中，并能控制数据的分区。同时，RDD还提供了一组丰富的API来操作这些数据。
RDD作为数据结构，本质上是一个只读的分区记录集合。分区代表并行度,决定了task的个数。一个RDD可以包含多个分区，每个分区就是一个dataset片段。RDD可以相互依赖。

如果RDD的每个分区最多只能被一个Child RDD的一个分区使用，则称之为narrow dependency；若多个Child RDD分区都可以依赖，则称之为wide dependency。不同的操作依据其特性，可能会产生不同的依赖。(区分原因：窄依赖可以用类似于管道的方式操作,由同一个task完成减少shuffle，其次任务失败后恢复重新计算的需要)
<img src="http://7xkx1t.com1.z0.glb.clouddn.com/blogspark3.png">

Spark并非是将整个RDD一次性加载到内存中。Spark针对partition采用了LRU（Least Recently Used）机制。当一个新的RDD分区需要计算时，如果没有合适的空间存储，就会根据LRU策略，将最少访问的RDD分区弹出，除非这个新分区与最少访问 的分区属于同一个RDD.这也在一定程度上缓和了对内存的消耗。

RDD操作：

RDDs 支持 2 种类型的操作：转换(transformations) 从已经存在的数据集中创建一个新的数据集；动作(actions) 在数据集上进行计算之后返回一个值到驱动程序。

例如，map 是一个转换操作，它将每一个数据集元素传递给一个函数并且返回一个新的 RDD。另一方面，reduce 是一个动作，它使用相同的函数来聚合 RDD 的所有元素，并且将最终的结果返回到驱动程序(不过也有一个并行 reduceByKey 能返回一个分布式数据集)。

所有的转换(transformations)都是惰性(lazy)的，它们不会马上计算它们的结果。转换仅仅在这个时候计算：当动作(action) 需要一个结果返回给驱动程序的时候。这个设计能够让 Spark 运行得更加高效。


转换（transformations）：
map(func)，mapToPair(fun)，filter(func)，flatMap(func)，groupByKey([numTasks])，reduceByKey(func, [numTasks])等等

动作（action）：
Reduce, collect, count, saveAsTextFile, take, foreach 等等


运行流程：

SparkContext 连接cluster Manager (either Spark’s own standalone cluster manager or Mesos/YARN),<br/>
spark Application向Cluster Manager请求资源 executors (运行计算和存储数据的线程)<br/>
将程序Jar包或者python程序分发到executors<br/>
SparkContext发送tasks到executors上运行<br/>
<img src="http://7xkx1t.com1.z0.glb.clouddn.com/blogspark4.png">


####spark-streaming：
Dstream:

DStream是Spark Streaming的基础抽象，代表持续性的数据流和经过各种Spark操作后的结果数据流。在内部实现上，DStream由连续的RDD来表示。每个RDD含有一段时间间隔内的数据，如下图：
<img src="http://7xkx1t.com1.z0.glb.clouddn.com/blogspark5.png">
<img src="http://7xkx1t.com1.z0.glb.clouddn.com/blogspark6.png">









