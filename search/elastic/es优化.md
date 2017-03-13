##es优化

###系统层面:

```
1. swap:

# 这是永久修改
$ echo "vm.swappiness = 1" >> /etc/sysctl.conf

# 这是临时修改，服务器重启后失效
$ sysctl vm.swappiness=1
$ sudo swapoff -a
$ sudo swapon -a


2. Max Open File Descriptors 设置为32k~64k:


# max open file descriptors
$ cp /etc/security/limits.conf /etc/security/limits.conf.bak
$ cat /etc/security/limits.conf | grep -v "elasticsearch" > /tmp/system_limits.conf
$ echo "elasticsearch      hard    nofile      50000" >> /tmp/system_limits.conf

$ echo "elasticsearch      soft    nofile      50000" >> /tmp/system_limits.conf

$ mv /tmp/system_limits.conf /etc/security/limits.conf


3. configure the maximum map count:

set it permanently by modifying vm.max_map_count setting in your /etc/sysctl.conf
# virtual Memory
$ cp /etc/sysctl.conf /etc/sysctl.conf.bak
$ cat /etc/sysctl.conf | grep -v "vm.max_map_count" > /tmp/system_sysctl.conf
$ echo "vm.max_map_count=262144" >> /tmp/system_sysctl.conf
$ mv /tmp/system_sysctl.conf /etc/sysctl.conf

或者临时修改:
sysctl -w vm.max_map_count=262144
查看结果：
$ sysctl -a|grep vm.max_map_count
vm.max_map_count = 262144
```

###应用层面

```
1. ES_HEAP_SIZE=Xg  最大最小内存一致，并且不要超过32G
2. 设置 bootstrap.mlockall: true
3. 

```