## java-tomcat docker file

### 安装java



``` 
FROM r1.d.qichecdn.com/centos:7.upstart

RUN set -x \
        &&  curl -v -j -k -L -H "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/7u79-b15/jdk-7u79-linux-x64.rpm > jdk-7u79-linux-x64.rpm \
                && rpm -ivh jdk-7u79-linux-x64.rpm \
                && rm -rf jdk-7u79-linux-x64.rpm


CMD ["/usr/sbin/init"]
```

### 安装tomcat和maven



	FROM  r1.d.qichecdn.com/java_1

	ADD http://soft.autohome.com.cn/app.tar.gz   /usr/local/

	ADD http://soft.autohome.com.cn/apache-maven-2.2.1-bin.tar.gz /usr/local/
	RUN  set -x \

	&& cd /usr/local/  \

	&&  tar -zxvf app.tar.gz \

	&&  tar -zxvf apache-maven-2.2.1-bin.tar.gz \

	&& echo 'export M2_HOME=/usr/local/apache-maven-2.2.1' >> /etc/profile \

	&& echo 'export PATH=$PATH:$M2_HOME/bin' >> /etc/profile \

	&& source /etc/profile \

	&& yum -y install git \

	&& mkdir -p  /root/.ssh 

	ENV M2_HOME /usr/local/apache-maven-2.2.1

	ENV PATH $PATH:$M2_HOME/bin

	ADD http://soft.autohome.com.cn/dockerapp  /etc/init.d/

	RUN chmod 755 /etc/init.d/dockerapp

	ADD http://soft.autohome.com.cn/dockerapp.service /lib/systemd/system/

	RUN chmod 754 /lib/systemd/system/dockerapp.service

	RUN systemctl enable dockerapp.service

	CMD ["/usr/sbin/init"]
	
###通过git下载代码
	FROM r1.d.qichecdn.com/j_108
	ADD http://soft.autohome.com.cn/id_rsa  /root/.ssh/
	ADD http://soft.autohome.com.cn/id_rsa.pub  /root/.ssh/
	ADD http://soft.autohome.com.cn/known_hosts  /root/.ssh/
	ENV  APP1_BASE  laker-web
	RUN set -x \
	&& chmod 600 /root/.ssh/id_rsa \
	&& git clone git@git.oschina.net:kavalla/laker.git  /usr/local/app/work/app1 \
	&& echo 'export APP1_BASE=laker-web' >> /etc/profile \
	&& source /etc/profile \
	&& cd /usr/local/app/ \
	&& ln -s  work/app1/$APP1_BASE/target/$APP1_BASE app1 
	CMD ["/usr/sbin/init"]





