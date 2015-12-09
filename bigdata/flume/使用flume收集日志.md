##使用flume收集日志

##安装：
---
apache网站下载 
apache-flume-1.6.0-bin.tar 解压即可

export JAVA_OPTS="-Xms1024m -Xmx1024m -XX:+UseParNewGC -XX:+UseConcMarkSweepGC -XX:-UseGCOverheadLimit"
##配置
---
客户端agent

```
# clientMainAgent
clientMainAgent.channels = c1
clientMainAgent.sources  = s1
clientMainAgent.sinks    = k1
# clientMainAgent Spooling Directory Source

clientMainAgent.sources.s1.type = exec
clientMainAgent.sources.s1.shell = /bin/bash -c
clientMainAgent.sources.s1.command = tail -F /data/logs/nginx/up.access.log 
clientMainAgent.sources.s1.channels = c1
clientMainAgent.sources.s1.threads = 5

# clientMainAgent FileChannel
clientMainAgent.channels.c1.type = memory
clientMainAgent.channels.c1.capacity = 100000
clientMainAgent.channels.c1.keep-alive = 30
clientMainAgent.channels.c1.transactionCapacity = 100
# clientMainAgent Sinks
# k1 sink
clientMainAgent.sinks.k1.channel = c1
clientMainAgent.sinks.k1.type = avro
clientMainAgent.sinks.k1.hostname = 192.168.194.135
clientMainAgent.sinks.k1.port = 6005
```

服务端：

```
a1.sources = r2 r5 a1.sinks = k2 k5 a1.channels = c2 c5a1.sources.r2.type = syslogtcpa1.sources.r2.port = 6002a1.sources.r2.host = 192.168.194.135a1.sources.r2.eventSize = 5000a1.sinks.k2.type = com.aweber.flume.sink.rabbitmq.RabbitMQSinka1.sinks.k2.host = 192.168.252.51a1.sinks.k2.port = 5672a1.sinks.k2.exchange = ex.scs2a1.sinks.k2.virtual-host = /a1.sinks.k2.username = guesta1.sinks.k2.password = 1122334455a1.sinks.k2.delivery-mode = 1a1.channels.c2.type = memorya1.channels.c2.capacity = 100000a1.channels.c2.keep-alive = 60a1.sources.r2.channels = c2a1.sinks.k2.channel = c2#####################a1.sources.r5.type = avroa1.sources.r5.port = 6005a1.sources.r5.bind = 192.168.194.135a1.sinks.k5.type = com.aweber.flume.sink.rabbitmq.RabbitMQSinka1.sinks.k5.host = 192.168.252.51a1.sinks.k5.port = 5672a1.sinks.k5.exchange = ex.scs3a1.sinks.k5.virtual-host = /a1.sinks.k5.username = guesta1.sinks.k5.password = 1122334455a1.sinks.k5.delivery-mode = 1a1.channels.c5.type = memorya1.channels.c5.capacity = 100000a1.channels.c5.keep-alive = 60a1.sources.r5.channels = c5a1.sinks.k5.channel = c5
```

###执行
nohup ./flume-ng agent --conf ../conf/   -f  ../conf/flume-conf.properties   -n clientMainAgent  -Dflume.root.logger=INFO   >/dev/null &


