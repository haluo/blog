
### 怎样使用

-原生Scala<br/>
-支持多种语言java python 等<br/>

分别用java语言介绍spark core 和 spark streaming的使用：

一.Spark core使用方法

	1.初始化,创建JavaSparkContext
	SparkConf sparkConf = new SparkConf().setAppName(”test”);
	JavaSparkContext ctx = new JavaSparkContext(sparkConf);
	2.创建RDD，支持多种数据源创建RDD
	JavaRDD<String> lines = ctx.textFile(“hdfs://xx.xx/xx/xx”);
	3.针对RDD进行迭代
	JavaPairRDD<String, String> rtsdd = lines.mapToPair(
			new PairFunction<String, String, String>() {
				 @Override
						public Tuple2<String, String> call(String s) throws Exception {
					//转化逻辑  return new Tuple2()
				}
	});
	JavaPairRDD<String,Iterable<String>> gpdd=  rtsdd .groupByKey();
	4.执行动作(Action)输出
    saveAsHadoopFile
    Foreach(function….)

    5.退出
    执行完毕后调用ctx.stop();

二 spark-streaming的使用方法

	1.初始化，创建JavaStreamingContext
    Duration batchInterval = new Duration(100);
    JavaStreamingContext context = new JavaStreamingContext("spark://hadoop-lq-194-130:7077", "TraceExStreaming", batchInterval);
    2.接收数据源数据创建Dstream
    context.socketStrem(….);
    或者自定义Receiver:
    JavaReceiverInputDStream<String> CSR = context.receiverStream(new RabbitReceiver());
    3.迭代Dstream
    Api跟spark core基本一致,都是对Dstream执行 map ,filter,reduce 等等

	窗口操作

    Duration windowOfFiveMDuration = new Duration(60000*5);
            Duration slideDuration = new Duration(60000*3);
    JavaPairDStream<String,String>  pairDStream2 = pairDStream.window(windowOfFiveMDuration,slideDuration);
    <img src="http://7xkx1t.com1.z0.glb.clouddn.com/blogspark7.png">
	4.执行动作(Action)输出
    对dstream执行saveAsHadoopFiles，foreachRDD等
    5.开始执行
      context.start();
    context.awaitTermination();

三 提交任务

Spark core和spark streaming的提交方式完全一样  都是由spark-submit命令完成
	spark-submit \
	  --class org.apache.spark.examples.SparkPi \
	  --master spark://207.184.161.138:7077 \
	  --supervise
	  --executor-memory 20G \
	  --total-executor-cores 10 \
	  /path/to/examples.jar \

###性能优化

并行度

除非你为每一步操作都设置足够高的并行度，否则集群不会得到最大化的利用。对于”map”操作，Spark会根据文件的大小自动设置在每个文件上的任务数（尽管你可以通过SparkContext.textFile的可选参数，来控制它）；对于分布式的”reduce”操作，例如groupByKey和reduceByKey，它会使用最大一个父RDD分区数目作为分块数。你可以传递并行度作为第二个参数，或者设置系统属性: spark.default.parallelism来改变默认值。总的来说，在集群中，推荐在每个CPU Core上分配2-3个Tasks

缓存中间数据避免多次计算

RDD,DStreams允许开发者持久化或缓存数据到内存中。在RDD,DStream上使用persist()或cache()方法可以自动地持久化RDD或DStream中的RDD到内存中。并且这些 数据可以被这个集合（以及这个集合迭代出来的其他集合）的动作（action）重复利用。这个能力使后续的动作速度更快（通常快10倍以上）。数据仅仅是进行一次处理,用完即丢弃,就应该避免使用cache或persist

广播大变量

使用SparkContext中的广播功能（broadcast ）将公用的大的变量，以广播的形式供所有任务使用，减小任务的大小。
















