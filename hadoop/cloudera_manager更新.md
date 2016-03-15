##cloudera manager安装和更新


###安装

```
vi /etc/yum.repos.d/cloudera-cdh5.repo


[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 6 x86_64
name=Cloudera Manager
baseurl=http://archive.cloudera.com/cm5/redhat/6/x86_64/cm/5/
gpgkey = http://archive.cloudera.com/cm5/redhat/6/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1


```
```
centos 7:

[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 7 x86_64                  
name=Cloudera Manager
baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5/
gpgkey =https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera    
gpgcheck = 1

```

####安装manager:
```
yum install cloudera-manager-daemons cloudera-manager-server
```

####安装agent:

```
yum install cloudera-manager-agent cloudera-manager-daemons -y
```



###更新

####1.停止服务

```
1.web界面停止集群服务和cm服务
2.停止service
service cloudera-scm-agent stop
service cloudera-scm-server stop
service cloudera-scm-server-db stop
```

####2.升级

```
yum clean all && yum upgrade 'cloudera-*'
```

####3.启动服务并进入界面检查



##CDH更新

http://www.cloudera.com/documentation/enterprise/latest/topics/install_upgrade_to_cdh56.html



