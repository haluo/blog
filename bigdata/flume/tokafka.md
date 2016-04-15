###tokafka

```
a1.sources = r9
a1.sinks = k91 k92
a1.channels = c91 c92 

a1.sources.r9.type = syslogtcp
a1.sources.r9.port = 6009
a1.sources.r9.host= 192.168.194.144
a1.sources.r9.eventSize = 5000
a1.sources.r9.channels = c91 c92


a1.channels.c91.type = memory
a1.channels.c91.capacity = 100000
a1.channels.c91.keep-alive = 60

a1.channels.c92.type = memory
a1.channels.c92.capacity = 100000
a1.channels.c92.keep-alive = 60

a1.sinks.k91.type = hdfs
a1.sinks.k91.hdfs.path = hdfs://192.168.194.141:8020/work/user/%Y/%m/%d
a1.sinks.k91.hdfs.filePrefix=user-%Y-%m-%d-%H
a1.sinks.k91.hdfs.useLocalTimeStamp = true
a1.sinks.k91.hdfs.writeFormat = Text
a1.sinks.k91.hdfs.fileType = CompressedStream
a1.sinks.k91.hdfs.rollInterval = 0
a1.sinks.k91.hdfs.rollSize = 1000000
a1.sinks.k91.hdfs.rollCount = 0
a1.sinks.k91.hdfs.batchSize = 1000
a1.sinks.k91.hdfs.txnEventMax = 1000
a1.sinks.k91.hdfs.callTimeout = 60000
a1.sinks.k91.hdfs.appendTimeout = 60000
a1.sinks.k91.hdfs.threadsPoolSize=15
a1.sinks.k91.hdfs.codeC=gzip
a1.sinks.k91.channel = c91

###老版本
#a1.sinks.k92.type = org.apache.flume.sink.kafka.KafkaSink
#a1.sinks.k92.metadata.broker.list=hadoop-lq-194-145:9092,hadoop-lq-194-149:9092,hadoop-lq-194-150:9092
#a1.sinks.k92.partition.key=0
#a1.sinks.k92.partitioner.class=org.apache.flume.plugins.SinglePartition
#a1.sinks.k92.serializer.class=kafka.serializer.StringEncoder
#a1.sinks.k92.request.required.acks=0
#a1.sinks.k92.max.message.size=1000000
#a1.sinks.k92.producer.type=sync
#a1.sinks.k92.custom.encoding=UTF-8
#a1.sinks.k92.custom.topic.name=test
#a1.sinks.k92.channel = c9

a1.sinks.k92.type=org.apache.flume.sink.kafka.KafkaSink
a1.sinks.k92.topic=flumetest
a1.sinks.k92.batch.size=1000
a1.sinks.k92.metadata.broker.list=hadoop-lq-194-145:9092,hadoop-lq-194-149:9092,hadoop-lq-194-150:9092
a1.sinks.k92.brokerList=hadoop-lq-194-145:9092,hadoop-lq-194-149:9092,hadoop-lq-194-150:9092
a1.sinks.k92.serializer.class=kafka.serializer.DefaultEncoder
a1.sinks.k92.producer.type=async
a1.sinks.k92.batch.num.messages=1000
a1.sinks.k92.queue.buffering.max.ms=1000
a1.sinks.k92.channel =c92

```