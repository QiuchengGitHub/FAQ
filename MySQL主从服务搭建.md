#MySQL实现主从复制#
##一、准备工作##
1.两个虚拟机：我这里用的是CentOS5.5，IP地址分别是192.168.1.101 和192.168.1.105；

　　　　　　　101做主服务器，105做从服务器（都已经安装相同版本的Mysql）；

2.本机环境：Apache+PHP+MySQL

##二、原理##
mysql要做到主从复制，其实依靠的是二进制日志，即：假设主服务器叫A，从服务器叫B；主从复制就是
B跟着A学，A做什么，B就做什么。那么B怎么同步A的动作呢？现在A有一个日志功能，把自己所做的增删改查的动作全都记录在日志中，B只需要拿到这份日志，照着日志上面的动作施加到自己身上就可以了。这样就实现了主从复制。
###扩展###
	MYSQL还有一种日志叫做：慢日志
	可以设置一个时间，那么所有执行时间超过这个时间的SQL都会被记录下来。这样就可以通过慢日志快速的找到网站中SQL的瓶颈来进行优化。

##三、实现步骤##
###第一步###
首先修改mysql的配置文件，使其支持二进制日志功能。

打开主服务器的mysql配置文件：my.conf

代码：# vi /etc/my.cnf

加入如下三行代码：

![](https://i.imgur.com/nnMG8xZ.png)

参数解释：

+ log-bin=mysql-bin  //将mysql二进制日志取名为mysql-bin
+ binlog_format=mixed //二进制日志的格式，有三种：statement/row/mixed,具体分别不多做解释，这里使用mixed
+ server-id=101 //为服务器设置一个独一无二的id便于区分，这里使用ip地址的最后一位充当server-id

 

配置完成，:wq 保存，重启mysql

重启mysql命令：# service mysqld restart

同样的，进入从服务器，配置从服务器的my.cnf,重复步骤1即可，

唯一的区别是，server-id要改成从服务器的ip尾位，即server-id=105;其他两项是一样的，保存，并重启mySQL；

###第二步###
在主服务器上为从服务器分配一个账号，就像一把钥匙，从服务器拿着这个钥匙，才能到主服务器上来共享主服务器的日志文件。

进入主服务器的mysql界面，

命令： # mysql -u root -p 111111     //我这里mysql账号是root，密码是111111

在mysql操作界面下，输入下面一行命令：

GRANT replication slave ON *.* TO 'slave'@'%' IDENTIFIED BY '111111';
 
![](https://i.imgur.com/1HpRiwF.png)

###第三步###
查看主服务器BIN日志的信息（执行完之后记录下这两值，然后在配置完从服务器之前不要对主服务器进行任何操作，因为每次操作数据库时这两值会发生改变）

![](https://i.imgur.com/OPCorSU.png)

注意:如果输入上面命令显示为空的话说明你配置文件中的log-bin=mysql-bin   (你需要找到注释掉的log-bin将其配置好即可)

###第四步###
设置从服务器

进入从服务器mysql

命令： # mysql -u root -p111111

关闭slave（如果你以前配置过主从的话，一定要先关闭）

命令：stop slave;

开始配置：

输入下面代码即可：

![](https://i.imgur.com/iY7i3Sl.png)

参数解释：

+ MASTER_HOST  :  设置要连接的主服务器的ip地址
+ MASTER_USER  :  设置要连接的主服务器的用户名
+ MASTER_PASSWORD  :  设置要连接的主服务器的密码
+ MASTER_LOG_FILE  :  设置要连接的主服务器的bin日志的日志名称，即第3步得到的信息
+ MASTER_LOG_POS  :  设置要连接的主服务器的bin日志的记录位置，即第3步得到的信息，（这里注意，最后一项不需要加引号。否则配置失败）

先在从服务器配置完成，启动从服务器：

命令： start slave;

![](https://i.imgur.com/L8RJnwO.png)

###第五步###
查看是否配置成功：

命令： show slave status;

![](https://i.imgur.com/CdGEc2G.png)

上面两项均为yes，说明配置成功，否则，请重复前面的步骤。

或者

mysql> show slave status\G命令查看

+ Slave_IO_Running: Yes
+ Slave_SQL_Running: Yes

这两个参数是不是都为yes,如果不是的话需要按照上面的步骤从新配置slave服务