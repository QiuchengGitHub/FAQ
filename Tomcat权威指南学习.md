#Tomcat容器学习#
##重定向Web应用程序主目录（一个tomcat版本，多个tomcat实例，window版）##
该解决方案可以解决如下两个使用场景：

+ 实现Tomcat发行版与业务项目代码的松耦合
+ 实现一个Tomcat运行多个Tomcat实例，且各实例独享各自的JVM

假设我的tomcat版本存放在D:\java-dev\apache-tomcat-7.0.82-64bit目录中，即 CATALINA_HOME=D:\java-dev\apache-tomcat-7.0.82-64bit。

	注意Program Files之间的空格

现在，我想要在D:\java-dev\tomcatInstance目录中新建KXM、CMDB与PPS实例。

###1、建立目录结构###
建立KXM、CMDB与PPS的目录结构如下：

	--D:\java-dev\tomcatInstance
	  	--KXM
			--bin
			--conf
			--lib
			--logs
			--temp
			--webapps
				--kxd-aio-amdin
			--work
		--CMDB
			--bin
			--conf
			--lib
			--logs
			--temp
			--webapps
				--kxd-cmdb-admin
			--work
		--PPS
			--bin
			--conf
			--lib
			--logs
			--temp
			--webapps
				--kxd-pps-amdin
			--work

###2、server.xml配置###
方便起见，将apache-tomcat-7.0.82-64bit\conf目录中的文件拷贝到KXM\conf、CMDB\conf与PPS\conf中，然后分别修改各个实例conf目录下的server.xml文件，修改内容如下（各实例的配置端口不能冲突）：

1. HTTP/1.1的连接端口（默认为8080）；
2. AJP/1.3（SSL）的连接端口（默认为8009）；
3. Apache的侦听端口（默认为8443）；
4. 停止Tomcat的端口（默认为8005）；

###3、创建start.bat和shutdown.bat###
在各个Tomcat实例目录的\bin下分别创建start.bat和shutdown.bat

	注意其中带有for语句的是为了解决批处理中带有空格路径的问题，并且将实例名做相应变更

+ startup.bat

		rem startup.bat
		set CATALINA_BASE=D:\java-dev\tomcatInstance\CMDB
		for %%x in ("%CATALINA_BASE%") do set CATALINA_BASE=%%~sx
		set CATALINA_HOME=D:\java-dev\apache-tomcat-7.0.82-64bit
		for %%x in ("%CATALINA_HOME%") do set CATALINA_HOME=%%~sx
		call %CATALINA_HOME%\bin\startup.bat
+ shutdown.bat

		rem shutdown.bat
		set CATALINA_BASE=D:\java-dev\tomcatInstance\CMDB
		for %%x in ("%CATALINA_BASE%") do set CATALINA_BASE=%%~sx
		set CATALINA_HOME=D:\java-dev\apache-tomcat-7.0.82-64bit
		for %%x in ("%CATALINA_HOME%") do set CATALINA_HOME=%%~sx
		call %CATALINA_HOME%\bin\shutdown.bat

至此，一个tomcat版本，多个tomcat实例完成！

----

##在80端口上运行以非root用户运行Tomcat##
为了在非Windows操作系统的80端口上提供服务，确实需要JVM必须以root用户运行。但是，如果可以将JVM进程之外的信息从80端口传递给高于1024的端口（如8080端口），你们JVM就可以不必须以root用户运行。

Tomcat可以在8080端口上打开其web服务，且具有合适权限的其他用户将80端口TCP连接传递给Tomcat的8080端口。在任何给定的操作系统上，这都是一个非常顺手、通用的功能，因此有多种方法完成该项工作，在端口传递或网络过滤时，通常会使用这一功能。

Linux的内嵌iptables特性允许各种防火墙、网络过滤和信息传递，而且可以简单地将端口80的TCP连接传递给Tomcat。Iptables特性是Linux内核的特性，通常默认为enabled状态，并可使用iptables命令行工具进行配置。以root用户执行下列命令，检查Linux内核的这一特性是否处于enabled状态：

![](https://i.imgur.com/YcYj3vV.jpg)

如果看到了相同或类似输出信息，那么你应该可使用iptables来传递Tomcat的端口连接了。如果你看到如下信息：

![](https://i.imgur.com/mwVkGqw.jpg)

这意味着iptables在内核中没有处于enabled状态，首先需要在内核中启用。

假定iptables已经开启，通过下列两条命令，你可以让80端口的所有TCP连接按机器配置寻址到所有网络目的地址：

	# iptables -t nat -I PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 8080
	# iptables -t nat -I PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 8080

这两条命令会在iptables的配置中增加必要的传递规则。它把机器上目的地为80端口的所有连接需重定向到8080端口的信息通知给内核。

如果你只想把机器配置的一个IP地址的连接传递给8080端口，那么可以在追加目的地址IP时选择性地使用--dst切换开关，如下所示：

	# iptables -t nat -I PREROUTING -p tcp --dst 192.169.1.100 --dport 80 -j REDIRECT --to-ports 8080
	# iptables -t nat -I OUTPUT -p tcp --dst 192.168.1.100 --dport 80 -j REDIRECT --to-ports 8080

实际运用中，只要将上述IP地址192.168.1.100变更为对应的服务器地址即可。

一旦增加成功，则可按下列方式查看结果：

	# iptables -t nat -L

此时，在80端口上发出的请求，Tomcat应该都能给收到。

	注意：重定向方法的缺点在于：为了显示真实的端口，Tomcat需要重写URL。假定你的网站是www.example.com。如果一个用户在其浏览器输入http://www.example.com/，那么依据web应用程序的内容而定，Tomcat会重写该地址，且该用户会在自己的浏览器位置看到http://www.example.com:8080/index.html。

Tomcat会认定请求来源于8080端口，因为它在8080端口上打开了web服务连接器，因此，无论何时发送重定向，它都会追加上端口号8080，除非你按照下列方式在server.xml连接器配置文件中增加proxyPort="80"属性：

	<Connector port="8080" protocol="HTTP/1.1" proxyPort="80" connectionTimeout="20000" redirectPort="8443" />

如果你安装的Tomcat就是充当了主页的功能，那么你也会想设置proxyName="hostname.example.com"。

关于如何让iptables正常工作并能使用其他哪些相关选项的内容，请参阅Linux iptables手册，以得到更多信息。至少在Linux上，这是Tomcat不采用root用户而应答80端口请求最简单的方法。

----
##Tomcat 6.0 server.xml元素清单##
<table>
	<tr>
		<th Style="width:10%">名称</th>
		<th Style="width:40%">功能</th>
		<th Style="width:25%">可出现于</th>
		<th Style="width:25%">可包含</th>
	</tr>
	<tr>
		<td>Server</td>
		<td>代表Tomcat自己</td>
		<td>顶层的XML元素。每个server.xml文件只能有一个这样的元素。</td>
		<td>Service、Listener，可选择性地包含GlobalNaming-Resources</td>
	</tr>
	<tr>
		<td>Service</td>
		<td>共享引擎（Engine）的分组连接器（Group Connector）</td>
		<td>一次或多次，而且每次的服务名都不同</td>
		<td>紧随Engine、Listener的一个或多个连接器（Connector）</td>
	</tr>
	<tr>
		<td>Executor</td>
		<td>可用于一个或多个Connector的共享线程池</td>
		<td>Service</td>
		<td>无</td>
	</tr>
	<tr>
		<td>Connector</td>
		<td>这是一个Web服务器或AJP服务器，或者是接收Tomcat要处理的请求的其他服务器</td>
		<td>Service</td>
		<td>Valve</td>
	</tr>
	<tr>
		<td>Engine</td>
		<td>处理所有请求</td>
		<td>Service</td>
		<td>Host、Realm、Valve、Listener和Cluster</td>
	</tr>
	<tr>
		<td>Cluster</td>
		<td>在多个Tomcat实例之间配置Tomcat的web应用程序集群</td>
		<td>Engine或Host</td>
		<td>Manager、Channel、Deployer、Valve、ClusterListener</td>
	</tr>
	<tr>
		<td>Host</td>
		<td>一台“虚拟主机”</td>
		<td>Engine</td>
		<td>Alias、Context、Realm、Valve、Listener、Cluster</td>
	</tr>
	<tr>
		<td>Host</td>
		<td>一台“虚拟主机”</td>
		<td>Engine</td>
		<td>Alias、Context、Realm、Valve、Listener、Cluster</td>
	</tr>
	<tr>
		<td>Alias</td>
		<td>主机Container的另一个全限定主机名</td>
		<td>Host</td>
		<td>None</td>
	</tr>
	<tr>
		<td>Context</td>
		<td>在Host内配置一个web应用程序</td>
		<td>Context</td>
		<td>Loader、Manager、Realm、Resources、ResourceLink、WatchedResource、Environment、Valve、Listener</td>
	</tr>
	<tr>
		<td>Realm</td>
		<td>设置用户和角色</td>
		<td>Engine、Host或Context</td>
		<td>无</td>
	</tr>
	<tr>
		<td>Valve</td>
		<td>处理过滤，运行为Tomcat的容器系统的一部分；用于各种目的，如日志、映射等</td>
		<td>Connector、Engine、Host、Context或Cluster</td>
		<td>无</td>
	</tr>
	<tr>
		<td>Manager</td>
		<td>配置应用程序会话实现的管理器</td>
		<td>Context或Cluster</td>
		<td>Store is the one and only nestable element,but only if you are using the PersistentManager</td>
	</tr>
	<tr>
		<td>Listener</td>
		<td>指定lifecycle监听器类，用于处理lifecycle</td>
		<td>Server、Service、Engine、Host或Context</td>
		<td>无</td>
	</tr>
	<tr>
		<td>Resources</td>
		<td>设定处理应用程序部署内容的实现类</td>
		<td>Context</td>
		<td>无</td>
	</tr>
	<tr>
		<td>Resource</td>
		<td>在全局（但单独的）JNDI或应用程序的JNDI context中定义单个的JNDI条目</td>
		<td>GlobalNaming-Resources或Context</td>
		<td>无</td>
	</tr>
	<tr>
		<td>ResourceEnvRef</td>
		<td>定义资源环境引用（ResourceEnvironment Reference），与Resource元素很相似</td>
		<td>GlobalNaming-Resources或Context</td>
		<td>无</td>
	</tr>
	<tr>
		<td>ResourceLink</td>
		<td>从全局（但独立的）JNDI context中连接JNDI资源到应用程序的JNDI context</td>
		<td>Context</td>
		<td>无</td>
	</tr>
	<tr>
		<td>WatchedResource</td>
		<td>如果修改的话，设定应用程序资源将触发一个context重载</td>
		<td>Context</td>
		<td>无</td>
	</tr>
	<tr>
		<td>GlobalNaming Resources</td>
		<td>定义全局的JNDI映射</td>
		<td>Server</td>
		<td>Environment、Resource、ResourceEnvRef、Transaction</td>
	</tr>
	<tr>
		<td>Environment settings</td>
		<td>定义环境设置</td>
		<td>GlobalNaming-Resources或Context</td>
		<td>无</td>
	</tr>
	<tr>
		<td>Store</td>
		<td>如果使用PersistentManager，则定义存储会话数据的位置</td>
		<td>Manager</td>
		<td>无</td>
	</tr>
	<tr>
		<td>Transaction settings</td>
		<td>设定UserTransaction</td>
		<td>GlobalNaming-Resource或Context</td>
		<td>无</td>
	</tr>
	<tr>
		<td>Channel</td>
		<td>配置用于集群的分组通信实现</td>
		<td>Cluster</td>
		<td>Membership、Sender、Receiver和Interceptor</td>
	</tr>
	<tr>
		<td>Membership</td>
		<td>为集群分组成员设定实现类</td>
		<td>Channel</td>
		<td>无</td>
	</tr>
	<tr>
		<td>Sender</td>
		<td>设定集群发送器实现类</td>
		<td>Channel</td>
		<td>可选择一个Transport</td>
	</tr>
	<tr>
		<td>Transport</td>
		<td>设定集群Sender的实现类和传输细节</td>
		<td>Sender</td>
		<td>无</td>
	</tr>
	<tr>
		<td>Receiver</td>
		<td>设定集群接收器（Receiver）的实现类和传输细节</td>
		<td>Channel</td>
		<td>无</td>
	</tr>
	<tr>
		<td>Interceptor</td>
		<td>设定集群消息拦截器的实现类</td>
		<td>Channel</td>
		<td>Member</td>
	</tr>
	<tr>
		<td>Member</td>
		<td>设定与压缩的Interceptor协同工作的静态成员</td>
		<td>Interceptor</td>
		<td>无</td>
	</tr>
	<tr>
		<td>Deployer</td>
		<td>设定集群部署器（deployer）实现类</td>
		<td>Cluster</td>
		<td>无</td>
	</tr>
	<tr>
		<td>ClusterListener</td>
		<td>设定接收Cluster时间的实现类</td>
		<td>Cluster</td>
		<td>无</td>
	</tr>
</table>