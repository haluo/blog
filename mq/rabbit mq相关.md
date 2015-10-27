## rabbit mq相关

安装



​		wget http://www.rabbitmq.com/releases/rabbitmq-server/v3.1.3/rabbitmq-server-3.1.3-1.noarch.rpm

​		rpm --import http://www.rabbitmq.com/rabbitmq-signing-key-public.asc

​		yum -y install rabbitmq-server-3.1.3-1.noarch.rpm

​		chkconfig rabbitmq-server on

​		rabbitmq-plugins enable rabbitmq_management

​		rabbitmq-plugins enable rabbitmq_management_agent



新增用户

​		rabbitmqctl  add_user  up   up123556 

设为超级管理员

​		rabbitmqctl  set_user_tags  up  administrator



主从配置：

​		nohup rabbitmq-server &

 		rabbitmqctl stop_app

 		rabbitmqctl reset

 		rabbitmqctl join_cluster rabbit@upex1

​	 	rabbitmqctl start_app



博客参考

​	安装：http://hmw.iteye.com/blog/2089111

​	权限：http://my.oschina.net/hncscwc/blog/262246?p={{page}}





















