#关于mybatis batchinsert的问题#
---
##问题描述##
当我们在使用mybatis操作MySQL数据库时，我们可以这样实现批量插入：

	<insert id="batchInsert" parameterType="java.util.List">
  	INSERT INTO BAD_USER(ID, MSG_ID, ITEM_TYPE, ITEM_VALUE, ADD_TIME, UPDATE_TIME, DEL_FLAG) 
  	VALUES 
  	<foreach collection="list" item="item" index= "index" separator =",">
  	(#{item.id,jdbcType=VARCHAR},#{item.msgId,jdbcType=VARCHAR},#{item.itemType,jdbcType=VARCHAR},
  	#{item.itemValue,jdbcType=VARCHAR},#{item.addTime,jdbcType=TIMESTAMP},
  	#{item.updateTime,jdbcType=TIMESTAMP},#{item.delFlag,jdbcType=INTEGER})
    </foreach>
  </insert>

但是当使用mybatis操作oracle数据库时，则会报错：

	[05/07/18 11:25:08:008 CST] DubboServerHandler-172.30.49.47:20880-thread-4 ERROR filter.ExceptionFilter:  [DUBBO] Got unchecked and undeclared exception which called by 0:0:0:0:0:0:0:1. service: com.kxd.soc.defenseRobot.service.SocDefenseRobotService, method: addBadUsers, exception: org.springframework.jdbc.BadSqlGrammarException: 
	### Error updating database.  Cause: java.sql.SQLException: ORA-00933: SQL 命令未正确结束

	### The error may involve com.kxd.soc.defenseRobot.BadUserMapper.batchInsert-Inline
	### The error occurred while setting parameters
	### Cause: java.sql.SQLException: ORA-00933: SQL 命令未正确结束

	; bad SQL grammar []; nested exception is java.sql.SQLException: ORA-00933: SQL 命令未正确结束
	, dubbo version: 2.5.8, current host: 172.30.49.47
	org.springframework.jdbc.BadSqlGrammarException: 
	### Error updating database.  Cause: java.sql.SQLException: ORA-00933: SQL 命令未正确结束

	### The error may involve com.kxd.soc.defenseRobot.BadUserMapper.batchInsert-Inline
	### The error occurred while setting parameters
	### Cause: java.sql.SQLException: ORA-00933: SQL 命令未正确结束

	; bad SQL grammar []; nested exception is java.sql.SQLException: ORA-00933: SQL 命令未正确结束

	at org.springframework.jdbc.support.SQLStateSQLExceptionTranslator.doTranslate(SQLStateSQLExceptionTranslator.java:98)
	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:72)
	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:80)
	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:80)
	at org.mybatis.spring.MyBatisExceptionTranslator.translateExceptionIfPossible(MyBatisExceptionTranslator.java:71)
	at org.mybatis.spring.SqlSessionTemplate$SqlSessionInterceptor.invoke(SqlSessionTemplate.java:358)
	at com.sun.proxy.$Proxy17.insert(Unknown Source)
	at org.mybatis.spring.SqlSessionTemplate.insert(SqlSessionTemplate.java:232)
	at com.kxd.framework.core.dao.mybatis.DaoMyBatis.insert(DaoMyBatis.java:360)
	at com.kxd.soc.defenseRobot.dao.impl.BadUserDaoMyBatis.batchSave(BadUserDaoMyBatis.java:24)
	at com.kxd.soc.defenseRobot.SocDefenseRobotServiceImpl.addBadUsers(SocDefenseRobotServiceImpl.java:79)
	at com.alibaba.dubbo.common.bytecode.Wrapper12.invokeMethod(Wrapper12.java)
	at com.alibaba.dubbo.rpc.proxy.javassist.JavassistProxyFactory$1.doInvoke(JavassistProxyFactory.java:46)
	at com.alibaba.dubbo.rpc.proxy.AbstractProxyInvoker.invoke(AbstractProxyInvoker.java:72)
	at com.alibaba.dubbo.rpc.protocol.InvokerWrapper.invoke(InvokerWrapper.java:53)
	at com.alibaba.dubbo.rpc.filter.ExceptionFilter.invoke(ExceptionFilter.java:64)
	at com.alibaba.dubbo.rpc.protocol.ProtocolFilterWrapper$1.invoke(ProtocolFilterWrapper.java:91)
	at com.alibaba.dubbo.rpc.filter.TimeoutFilter.invoke(TimeoutFilter.java:42)
	at com.alibaba.dubbo.rpc.protocol.ProtocolFilterWrapper$1.invoke(ProtocolFilterWrapper.java:91)
	at com.alibaba.dubbo.monitor.support.MonitorFilter.invoke(MonitorFilter.java:75)
	at com.alibaba.dubbo.rpc.protocol.ProtocolFilterWrapper$1.invoke(ProtocolFilterWrapper.java:91)
	at com.alibaba.dubbo.rpc.protocol.dubbo.filter.TraceFilter.invoke(TraceFilter.java:78)
	at com.alibaba.dubbo.rpc.protocol.ProtocolFilterWrapper$1.invoke(ProtocolFilterWrapper.java:91)
	at com.alibaba.dubbo.rpc.filter.ContextFilter.invoke(ContextFilter.java:60)
	at com.alibaba.dubbo.rpc.protocol.ProtocolFilterWrapper$1.invoke(ProtocolFilterWrapper.java:91)
	at com.alibaba.dubbo.rpc.filter.GenericFilter.invoke(GenericFilter.java:132)
	at com.alibaba.dubbo.rpc.protocol.ProtocolFilterWrapper$1.invoke(ProtocolFilterWrapper.java:91)
	at com.alibaba.dubbo.rpc.filter.ClassLoaderFilter.invoke(ClassLoaderFilter.java:38)
	at com.alibaba.dubbo.rpc.protocol.ProtocolFilterWrapper$1.invoke(ProtocolFilterWrapper.java:91)
	at com.alibaba.dubbo.rpc.filter.EchoFilter.invoke(EchoFilter.java:38)
	at com.alibaba.dubbo.rpc.protocol.ProtocolFilterWrapper$1.invoke(ProtocolFilterWrapper.java:91)
	at com.alibaba.dubbo.rpc.protocol.dubbo.telnet.InvokeTelnetHandler.telnet(InvokeTelnetHandler.java:98)
	at com.alibaba.dubbo.remoting.telnet.support.TelnetHandlerAdapter.telnet(TelnetHandlerAdapter.java:54)
	at com.alibaba.dubbo.remoting.exchange.support.header.HeaderExchangeHandler.received(HeaderExchangeHandler.java:183)
	at com.alibaba.dubbo.remoting.transport.DecodeHandler.received(DecodeHandler.java:52)
	at com.alibaba.dubbo.remoting.transport.dispatcher.ChannelEventRunnable.run(ChannelEventRunnable.java:82)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
	at java.lang.Thread.run(Thread.java:745)
	Caused by: java.sql.SQLException: ORA-00933: SQL 命令未正确结束

	at oracle.jdbc.driver.SQLStateMapping.newSQLException(SQLStateMapping.java:74)
	at oracle.jdbc.driver.DatabaseError.newSQLException(DatabaseError.java:110)
	at oracle.jdbc.driver.DatabaseError.throwSqlException(DatabaseError.java:171)
	at oracle.jdbc.driver.T4CTTIoer.processError(T4CTTIoer.java:455)
	at oracle.jdbc.driver.T4CTTIoer.processError(T4CTTIoer.java:413)
	at oracle.jdbc.driver.T4C8Oall.receive(T4C8Oall.java:1030)
	at oracle.jdbc.driver.T4CPreparedStatement.doOall8(T4CPreparedStatement.java:194)
	at oracle.jdbc.driver.T4CPreparedStatement.executeForRows(T4CPreparedStatement.java:947)
	at oracle.jdbc.driver.OracleStatement.doExecuteWithTimeout(OracleStatement.java:1222)
	at oracle.jdbc.driver.OraclePreparedStatement.executeInternal(OraclePreparedStatement.java:3381)
	at oracle.jdbc.driver.OraclePreparedStatement.execute(OraclePreparedStatement.java:3482)
	at oracle.jdbc.driver.OraclePreparedStatementWrapper.execute(OraclePreparedStatementWrapper.java:1085)
	at org.apache.commons.dbcp.DelegatingPreparedStatement.execute(DelegatingPreparedStatement.java:172)
	at org.apache.commons.dbcp.DelegatingPreparedStatement.execute(DelegatingPreparedStatement.java:172)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:606)
	at org.apache.ibatis.logging.jdbc.PreparedStatementLogger.invoke(PreparedStatementLogger.java:45)
	at com.sun.proxy.$Proxy36.execute(Unknown Source)
	at org.apache.ibatis.executor.statement.PreparedStatementHandler.update(PreparedStatementHandler.java:22)
	at org.apache.ibatis.executor.statement.RoutingStatementHandler.update(RoutingStatementHandler.java:51)
	at org.apache.ibatis.executor.SimpleExecutor.doUpdate(SimpleExecutor.java:29)
	at org.apache.ibatis.executor.BaseExecutor.update(BaseExecutor.java:88)
	at org.apache.ibatis.executor.CachingExecutor.update(CachingExecutor.java:43)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:606)
	at org.apache.ibatis.plugin.Invocation.proceed(Invocation.java:31)
	at com.kxd.framework.core.dao.mybatis.plugin.CryptPlugin.interceptUpdate(CryptPlugin.java:130)
	at com.kxd.framework.core.dao.mybatis.plugin.CryptPlugin.intercept(CryptPlugin.java:64)
	at org.apache.ibatis.plugin.Plugin.invoke(Plugin.java:42)
	at com.sun.proxy.$Proxy34.update(Unknown Source)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.update(DefaultSqlSession.java:122)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.insert(DefaultSqlSession.java:111)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:606)
	at org.mybatis.spring.SqlSessionTemplate$SqlSessionInterceptor.invoke(SqlSessionTemplate.java:350)
	... 33 more

##问题分析##
根本原因是Oracle不支持以下这种用法（而MySQL支持）：

	insert into BAD_USER (ID,MSG_ID,ITEM_TYPE,ITEM_VALUE,ADD_TIME,UPDATE_TIME,DEL_FLAG)
	VALUES('1','1','ip','10.0.0.1',CURRENT_DATE,CURRENT_DATE,0),('2','1','ip','10.0.0.1',CURRENT_DATE,CURRENT_DATE,0);

##问题解决##
###解决办法一###

	直接使用mybatis的batchinsert方法即可（个人印象中，mybatis的batchinsert只是循环调用，并不是真正的batch）。

###解决办法二###

	<insert id="batchSave" parameterType="java.util.List">
	  	BEGIN
	  	<foreach collection="list" item="item" index= "index" separator=";">
	  	INSERT INTO BAD_USER(ID, MSG_ID, ITEM_TYPE, ITEM_VALUE, ADD_TIME, UPDATE_TIME, DEL_FLAG) 
	  	VALUES 
	  	(#{item.id,jdbcType=VARCHAR},#{item.msgId,jdbcType=VARCHAR},#{item.itemType,jdbcType=VARCHAR},
	  	#{item.itemValue,jdbcType=VARCHAR},#{item.addTime,jdbcType=TIMESTAMP},
	  	#{item.updateTime,jdbcType=TIMESTAMP},#{item.delFlag,jdbcType=INTEGER})
	    </foreach>
	    ;END ;
	  </insert>