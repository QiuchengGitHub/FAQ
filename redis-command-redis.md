#Redis TIME命令#
##问题描述##
切换项目的redis资源后，重新启动，报错如下：

	严重: Servlet.service() for servlet [Spring MVC DispatcherServlet] in context with path [/kxd-soc-admin-war] threw exception
	com.kxd.framework.cache.redis.exception.KedisException: ERR unknown command 'TIME'
	at com.kxd.framework.cache.redis.operation.Operation.executeCallback(Operation.java:65)
	at com.kxd.framework.cache.redis.operation.Operation4Server.time(Operation4Server.java:30)
	at com.kxd.framework.cache.redis.operation.Operation4Server.timeOfCurrentTime(Operation4Server.java:24)
	at com.kxd.framework.session.store.RedisBackendStore.createSession(RedisBackendStore.java:71)
	at com.kxd.framework.session.RequestWrapper.createNewSession(RequestWrapper.java:156)
	at com.kxd.framework.session.RequestWrapper.getSession(RequestWrapper.java:87)
	at com.kxd.framework.session.RequestWrapper.getSession(RequestWrapper.java:70)
	at com.kxd.framework.session.RequestWrapper.getSession(RequestWrapper.java:66)
	at com.kxd.framework.web.util.SessionHelper.setSessionValue(SessionHelper.java:39)
	at com.kxd.kjw.framework.filter.WebFilter.requestFilter(WebFilter.java:51)
	at com.kxd.framework.web.filter.BaseFilter.doFilter(BaseFilter.java:136)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:241)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:208)
	at com.kxd.framework.web.filter.BaseFilter.doFilter(BaseFilter.java:196)
	at com.kxd.framework.web.filter.BaseFilter.doFilter(BaseFilter.java:137)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:241)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:208)
	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:88)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:76)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:241)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:208)
	at com.kxd.framework.session.SessionFilter.doFilter(SessionFilter.java:79)
	at org.springframework.web.filter.DelegatingFilterProxy.invokeDelegate(DelegatingFilterProxy.java:346)
	at org.springframework.web.filter.DelegatingFilterProxy.doFilter(DelegatingFilterProxy.java:259)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:241)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:208)
	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:219)
	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:110)
	at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:506)
	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:169)
	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:103)
	at org.apache.catalina.valves.AccessLogValve.invoke(AccessLogValve.java:962)
	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:116)
	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:445)
	at org.apache.coyote.http11.AbstractHttp11Processor.process(AbstractHttp11Processor.java:1115)
	at org.apache.coyote.AbstractProtocol$AbstractConnectionHandler.process(AbstractProtocol.java:637)
	at org.apache.tomcat.util.net.JIoEndpoint$SocketProcessor.run(JIoEndpoint.java:316)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
	at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61)
	at java.lang.Thread.run(Thread.java:744)

##问题分析##
抛出的异常信息倒是挺清晰的：
	
	ERR unknown command 'TIME'

即未知的命令TIME

##问题解决##
###TIME###
####TIME####
	返回当前服务器时间。
####可用版本：####
	>= 2.6.0
####时间复杂度：####
	O(1)
####返回值：####
	一个包含两个字符串的列表： 第一个字符串是当前时间(以 UNIX 时间戳格式表示)，而第二个字符串是当前这一秒钟已经逝去的微秒数。
####示例####
	redis> TIME
	1) "1332395997"
	2) "952581"
	redis> TIME
	1) "1332395997"
	2) "953148"