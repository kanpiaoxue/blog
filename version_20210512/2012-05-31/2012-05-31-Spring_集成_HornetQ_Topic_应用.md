#Spring 集成 HornetQ Topic 应用
###发表时间：2012-05-31
###分类：Spring,HornetQ
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1545642" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1545642</a>

---

<p>用HornetQ和Spring3做了一个简单的小例子，client发送指定的json串，经由HornetQ，由Server接收。</p>
<p>&nbsp;</p>
<p>--------------------- client code -----------------------------------</p>
<p>spring 配置文件:</p>
<p> </p>
<pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:util="http://www.springframework.org/schema/util"
        xmlns:jee="http://www.springframework.org/schema/jee" xmlns:lang="http://www.springframework.org/schema/lang"
        xmlns:jms="http://www.springframework.org/schema/jms" xmlns:aop="http://www.springframework.org/schema/aop"
        xmlns:tx="http://www.springframework.org/schema/tx" xmlns:context="http://www.springframework.org/schema/context"

        xsi:schemaLocation="
http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util-3.0.xsd
http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-3.0.xsd
http://www.springframework.org/schema/lang http://www.springframework.org/schema/lang/spring-lang-3.0.xsd
http://www.springframework.org/schema/jms http://www.springframework.org/schema/jms/spring-jms-3.0.xsd
http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.0.xsd
http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.0.xsd"&gt;


        &lt;bean id="messageTopic" class="org.hornetq.api.jms.HornetQJMSClient"
                factory-method="createTopic"&gt;
                &lt;constructor-arg value="com.wanmei.bitask.input.initialize.topic" /&gt;
        &lt;/bean&gt;

        &lt;bean id="transportConfiguration" class="org.hornetq.api.core.TransportConfiguration"&gt;
                &lt;constructor-arg
                        value="org.hornetq.core.remoting.impl.netty.NettyConnectorFactory" /&gt;
                &lt;constructor-arg&gt;
                        &lt;map key-type="java.lang.String" value-type="java.lang.Object"&gt;
                                &lt;entry key="host" value="192.168.123.74"&gt;&lt;/entry&gt;
                                &lt;entry key="port" value="5445"&gt;&lt;/entry&gt;
                        &lt;/map&gt;
                &lt;/constructor-arg&gt;
        &lt;/bean&gt;

        &lt;bean id="connectionFactory" class="org.hornetq.api.jms.HornetQJMSClient"
                factory-method="createConnectionFactoryWithoutHA"&gt;
                &lt;constructor-arg type="org.hornetq.api.jms.JMSFactoryType"
                        value="CF" /&gt;
                &lt;constructor-arg ref="transportConfiguration" /&gt;
        &lt;/bean&gt;

        &lt;bean id="jmsTemplate" class="org.springframework.jms.core.JmsTemplate"&gt;
                &lt;property name="connectionFactory" ref="connectionFactory" /&gt;
                &lt;property name="pubSubDomain" value="true" /&gt;      
        &lt;/bean&gt;

        &lt;bean id="service" class="com.wanmei.service.impl.ServiceImpl"&gt;
                &lt;property name="jmsTemplate" ref="jmsTemplate" /&gt;
                &lt;property name="topic" ref="messageTopic" /&gt;
        &lt;/bean&gt;


        
&lt;/beans&gt;</pre>
<p>&nbsp;</p>
<p>java类的实现：</p>
<p>&nbsp;</p>
<p> </p>
<pre name="code" class="java">public class ServiceImpl implements Service {
	private static final Logger logger = Logger.getLogger(ServiceImpl.class);
	private JmsTemplate jmsTemplate;
	private Topic topic;

	/*
	 * (non-Javadoc)
	 * 
	 * @see com.wanmei.service.Service#sendMessage(java.util.List)
	 */
	@Override
	public boolean sendMessage(List&lt;TaskMessage&gt; messageList) {
		return sendTopic(messageList);
	}

	// ------------------ private method

	private boolean sendTopic(List&lt;TaskMessage&gt; messageList) {
		try {
			for (TaskMessage msg : messageList) {
				Gson gson = new Gson();
				final String msgJson = gson.toJson(msg);
				logger.info("start to send topic to " + topic.getTopicName()
						+ ", message : " + msgJson);
				jmsTemplate.send(topic, new MessageCreator() {

					@Override
					public Message createMessage(Session session)
							throws JMSException {
						TextMessage message = session
								.createTextMessage(msgJson);
						return message;
					}
				});
			}
			return true;
		} catch (Exception e) {
			logger.error("Error: send topic failure:" + e.getMessage(), e);
			return false;
		}
	}

	// ------------------ setter / getter
	/**
	 * @return the jmsTemplate
	 */
	public JmsTemplate getJmsTemplate() {
		return jmsTemplate;
	}

	/**
	 * @param jmsTemplate
	 *            the jmsTemplate to set
	 */
	public void setJmsTemplate(JmsTemplate jmsTemplate) {
		this.jmsTemplate = jmsTemplate;
	}

	/**
	 * @return the logger
	 */
	public static Logger getLogger() {
		return logger;
	}

	/**
	 * @return the topic
	 */
	public Topic getTopic() {
		return topic;
	}

	/**
	 * @param topic
	 *            the topic to set
	 */
	public void setTopic(Topic topic) {
		this.topic = topic;
	}

}
</pre>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p> </p>
<p>--------------------- server code -----------------------------------</p>
<p>spring 配置文件:</p>
<p>&nbsp;</p>
<p> </p>
<pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:util="http://www.springframework.org/schema/util"
	xmlns:jee="http://www.springframework.org/schema/jee" xmlns:lang="http://www.springframework.org/schema/lang"
	xmlns:jms="http://www.springframework.org/schema/jms" xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:tx="http://www.springframework.org/schema/tx" xmlns:context="http://www.springframework.org/schema/context"

	xsi:schemaLocation="
http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util-3.0.xsd
http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-3.0.xsd
http://www.springframework.org/schema/lang http://www.springframework.org/schema/lang/spring-lang-3.0.xsd
http://www.springframework.org/schema/jms http://www.springframework.org/schema/jms/spring-jms-3.0.xsd
http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.0.xsd
http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.0.xsd"&gt;


	&lt;bean id="messageTopic" class="org.hornetq.api.jms.HornetQJMSClient"
		factory-method="createTopic"&gt;
		&lt;constructor-arg value="com.wanmei.bitask.input.initialize.topic" /&gt;
	&lt;/bean&gt;

	&lt;bean id="transportConfiguration" class="org.hornetq.api.core.TransportConfiguration"&gt;
		&lt;constructor-arg
			value="org.hornetq.core.remoting.impl.netty.NettyConnectorFactory" /&gt;
		&lt;constructor-arg&gt;
			&lt;map key-type="java.lang.String" value-type="java.lang.Object"&gt;
				&lt;entry key="host" value="192.168.123.74"&gt;&lt;/entry&gt;
				&lt;entry key="port" value="5445"&gt;&lt;/entry&gt;
			&lt;/map&gt;
		&lt;/constructor-arg&gt;
	&lt;/bean&gt;

	&lt;bean id="connectionFactory" class="org.hornetq.api.jms.HornetQJMSClient"
		factory-method="createConnectionFactoryWithoutHA"&gt;
		&lt;constructor-arg type="org.hornetq.api.jms.JMSFactoryType"
			value="CF" /&gt;
		&lt;constructor-arg ref="transportConfiguration" /&gt;
	&lt;/bean&gt;

	&lt;!-- this is the Message Driven POJO (MDP) --&gt;
	&lt;bean id="messageListener" class="com.wanmei.service.MessageListenerImpl"&gt;
		&lt;property name="jdbcTemplate" ref="bitaskJdbcTemplate" /&gt;
	&lt;/bean&gt;

	&lt;!-- and this is the message listener container --&gt;
	&lt;bean id="jmsContainer"
		class="org.springframework.jms.listener.DefaultMessageListenerContainer"&gt;
		&lt;property name="connectionFactory" ref="connectionFactory" /&gt;
		&lt;property name="destination" ref="messageTopic" /&gt;
		&lt;property name="messageListener" ref="messageListener" /&gt;
	&lt;/bean&gt;


	&lt;!-- jdbc start --&gt;
	&lt;bean id="bitaskDataSource" class="org.apache.commons.dbcp.BasicDataSource"
		destroy-method="close"&gt;
		&lt;property name="driverClassName" value="oracle.jdbc.driver.OracleDriver" /&gt;
		&lt;property name="url" value="jdbc:oracle:thin:@192.168.182.129:1521:wmdw" /&gt;
		&lt;property name="username" value="bitask" /&gt;
		&lt;property name="password" value="bitask" /&gt;
		&lt;property name="validationQuery" value="select * from dual" /&gt;
	&lt;/bean&gt;


	&lt;bean id="bitaskJdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate"&gt;
		&lt;property name="dataSource" ref="bitaskDataSource" /&gt;
	&lt;/bean&gt;

	&lt;bean id="transactionManager_jdbcTemplate"
		class="org.springframework.jdbc.datasource.DataSourceTransactionManager"&gt;
		&lt;property name="dataSource" ref="bitaskDataSource" /&gt;
	&lt;/bean&gt;

	&lt;aop:config&gt;
		&lt;aop:advisor pointcut="execution(* com.wanmei.service.*Impl*.*(..))"
			advice-ref="txAdvice_jdbcTemplate" /&gt;
	&lt;/aop:config&gt;

	&lt;tx:advice id="txAdvice_jdbcTemplate" transaction-manager="transactionManager_jdbcTemplate"&gt;
		&lt;tx:attributes&gt;
			&lt;tx:method name="change*" propagation="REQUIRED" /&gt;
			&lt;tx:method name="update*" propagation="REQUIRED" /&gt;
			&lt;tx:method name="merge*" propagation="REQUIRED" /&gt;
			&lt;tx:method name="get*" read-only="true" /&gt;
			&lt;tx:method name="save*" propagation="REQUIRED" /&gt;
			&lt;tx:method name="add*" propagation="REQUIRED" /&gt;
			&lt;tx:method name="delete*" propagation="REQUIRED" /&gt;
			&lt;tx:method name="remove*" propagation="REQUIRED" /&gt;
			&lt;tx:method name="hidden*" propagation="REQUIRED" /&gt;
		&lt;/tx:attributes&gt;
	&lt;/tx:advice&gt;

	&lt;!-- &lt;bean id="lobHandler" class="org.springframework.jdbc.support.lob.DefaultLobHandler" 
		lazy-init="true"/&gt; --&gt;

	&lt;!-- jdbc end --&gt;


&lt;/beans&gt;</pre>
<p>&nbsp;</p>
<p> </p>
<p>java类的实现：</p>
<p>&nbsp;</p>
<p> </p>
<pre name="code" class="java">public class MessageListenerImpl implements MessageListener {
	private static Logger logger = Logger.getLogger(MessageListenerImpl.class);
	private JdbcTemplate jdbcTemplate;

	/*
	 * (non-Javadoc)
	 * 
	 * @see javax.jms.MessageListener#onMessage(javax.jms.Message)
	 */
	@Override
	public void onMessage(Message objMsg) {
		TextMessage msg = (TextMessage) objMsg;
		try {
			String json = msg.getText();
			logger.info("receive message : " + json);
			doJson(json);
		} catch (JMSException e) {
			logger.error(
					"Error: receive message from topic failure: "
							+ e.getMessage(), e);
		}
	}

	// ------------------ private method
	private void doJson(String json) {
		Gson gson = new Gson();
		TaskMessage message = gson.fromJson(json, TaskMessage.class);
		if (checkValid(message)) {
			updateProcRun(message);
		} else {
			logger.error("Error: found null value in message.");
		}

	}

	private void updateProcRun(final TaskMessage msg) {
		StringBuilder builder = new StringBuilder();
		builder.append(" update task_proc_run ")
				.append(" set task_status = ?, ").append(" reload = ?, ")
				.append(" ignore_type = ?, ").append(" initial_type = ?, ")
				.append(" last_modified = sysdate, ")
				.append(" exec_message = ? ")
				.append(" where proc_time = to_date(?,'yyyy-mm-dd') ")
				.append(" and proc_name = ? ")
				.append(" and data_source_name = ? ");
				

		int count = jdbcTemplate.update(builder.toString(),
				new PreparedStatementSetter() {

					@Override
					public void setValues(PreparedStatement ps)
							throws SQLException {
						ps.setInt(1, msg.getTaskStatus());
						ps.setString(2, msg.getReload());
						ps.setInt(3, msg.getIgnoreType());
						ps.setInt(4, msg.getInitialType());
						ps.setString(5, msg.getExecMessage());
						ps.setString(6, msg.getProcTime());
						ps.setString(7, msg.getProcName());
						ps.setString(8, msg.getDataSourceName());

					}
				});
		if (1 == count) {
			logger.info("update task_proc_run successfully. " + msg);
		} else {
			logger.error("update task_proc_run failure: " + msg);
		}

	}

	private static boolean checkValid(TaskMessage msg) {

		if (isNull(msg.getProcName()) || isNull(msg.getProcTime())
				|| isNull(msg.getDataSourceName())
				|| isNull(msg.getIgnoreType()) || isNull(msg.getInitialType())
				|| isNull(msg.getTaskStatus()) || isNull(msg.getExecMessage())
				|| isNull(msg.getReload())) {
			logger.error("Error: some field is null. Please check args.");
			return false;
		}

		return true;
	}

	private static boolean isNull(Object obj) {
		return obj == null ? true : false;
	}

	// ------------------ setter / getter
	/**
	 * @return the logger
	 */
	public static Logger getLogger() {
		return logger;
	}

	/**
	 * @param logger
	 *            the logger to set
	 */
	public static void setLogger(Logger logger) {
		MessageListenerImpl.logger = logger;
	}

	/**
	 * @return the jdbcTemplate
	 */
	public JdbcTemplate getJdbcTemplate() {
		return jdbcTemplate;
	}

	/**
	 * @param jdbcTemplate
	 *            the jdbcTemplate to set
	 */
	public void setJdbcTemplate(JdbcTemplate jdbcTemplate) {
		this.jdbcTemplate = jdbcTemplate;
	}

}
</pre>