##elasticsearch安装

```
1.
使用官方JDK

2.
rpm --import https://packages.elastic.co/GPG-KEY-elasticsearch

3.
vi  /etc/yum.repos.d/elasticsearch.repo

[elasticsearch-2.x]
name=Elasticsearch repository for 2.x packages
baseurl=http://packages.elastic.co/elasticsearch/2.x/centos
gpgcheck=1
gpgkey=http://packages.elastic.co/GPG-KEY-elasticsearch
enabled=1

4.
yum -y install elasticsearch

```
###elasticsearch配置

```
创建数据目录
find / -type d  -maxdepth 1 -name 'data*' -exec mkdir {}/es \;
chmod -R 777 /data*/es

创建日志目录
mkdir -p  /data/logs/es
chmod -R 777 /data/logs/es

```
```
elasticsearch.yml配置：


cluster.name: aump
node.name: es-252.41

path.data: /data1/es,/data2/es,/data3/es,/data4/es,/data5/es,/data6/es,/data7/es,/data8/es,/data9/es,/data10/es,/data11/es,/data12/es

path.logs: /data/logs/es

network.host: 192.168.252.41

discovery.zen.ping.multicast.enabled: false

discovery.zen.minimum_master_nodes: 5

discovery.zen.ping.unicast.hosts:["192.168.252.41","192.168.252.42","192.168.252.43"]


script.inline: on
script.indexed: on

cluster.routing.allocation.allow_rebalance: indices_all_active
cluster.routing.allocation.cluster_concurrent_rebalance: 5
cluster.routing.allocation.node_concurrent_recoveries: 5

```

###插件

```
1. head 插件
elasticsearch/bin/plugin install mobz/elasticsearch-head

http://ip:9200/_plugin/head/ 可以查看显示效果

2.
plugin  install lmenezes/elasticsearch-kopf

3.IK中文分析

https://github.com/medcl/elasticsearch-analysis-ik

```

###优化
```
bin/elasticsearch.in.sh
中设置
ES_MIN_MEM=8g
ES_MAX_MEM=8g

```




###  线程池。 ping次数
```
threadpool.bulk.type: fixed
threadpool.bulk.size: 50
threadpool.bulk.queue_size: 1000

ping_retries: 20
```




