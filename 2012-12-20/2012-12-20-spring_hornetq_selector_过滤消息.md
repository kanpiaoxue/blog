#spring hornetq selector 过滤消息
###发表时间：2012-12-20
###分类：Spring,HornetQ
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1751436" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1751436</a>

---

<p>在接收 JMS消息的时候，我们经常要在消息队列里面过滤出自己需要的消息，摒弃我们不需要的消息。这个时候就需要用到 JMS的selector功能。这里结合spring3.1，给出一个例子。</p>
<p>&nbsp;</p>
<p>发送消息的配置：</p>
<p>&nbsp;</p>
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


	&lt;bean id="selectorQueue" class="org.hornetq.api.jms.HornetQJMSClient"
		factory-method="createQueue"&gt;
		&lt;constructor-arg value="org.spring.jms.selector.queue" /&gt;
	&lt;/bean&gt;
	
	
	&lt;bean id="transportConfiguration" class="org.hornetq.api.core.TransportConfiguration"&gt;
		&lt;constructor-arg
			value="org.hornetq.core.remoting.impl.netty.NettyConnectorFactory" /&gt;
		&lt;constructor-arg&gt;
			&lt;map key-type="java.lang.String" value-type="java.lang.Object"&gt;
				&lt;entry key="host" value="localhost"&gt;&lt;/entry&gt;
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
	&lt;/bean&gt;
	
	&lt;bean id="sender" class="com.wanmei.jms.spring.selector.config.sender.Sender"&gt;
		&lt;property name="jmsTemplate" ref="jmsTemplate" /&gt;
		&lt;property name="destination" ref="selectorQueue" /&gt;
	&lt;/bean&gt;
		
&lt;/beans&gt;</pre>
<p>&nbsp;</p>
<p>&nbsp;发送消息的Sender类</p>
<p>&nbsp;</p>
<pre name="code" class="java">/**
 * &lt;pre&gt;
 * &lt;/pre&gt;
 */
package com.wanmei.jms.spring.selector.config.sender;

import javax.jms.Destination;
import javax.jms.JMSException;
import javax.jms.Message;
import javax.jms.Session;
import javax.jms.TextMessage;

import org.apache.log4j.Logger;
import org.springframework.jms.core.JmsTemplate;
import org.springframework.jms.core.MessageCreator;

import com.wanmei.jms.spring.selector.java.State;

/**
 * &lt;pre&gt;
 * date 2012-12-20
 * &lt;/pre&gt;
 */
public class Sender implements State {
	private static final Logger LOGGER = Logger.getLogger(Sender.class);
	private JmsTemplate jmsTemplate;
	private Destination destination;
	

	public void send(final String message, final String fromNode,
			final String toNode) {
		try {
			LOGGER.info("start to send message to " + destination
					+ " [message:" + message + ",fromNode:" + fromNode
					+ ",toNode:" + toNode);
			jmsTemplate.send(destination, new MessageCreator() {

				@Override
				public Message createMessage(Session session)
						throws JMSException {
					LOGGER.info("session:"+session + "\nmessage : " + message);
					TextMessage msg = session.createTextMessage(message);
					msg.setStringProperty(FROM_NODE, fromNode);
					msg.setStringProperty(TO_NODE, toNode);
					
					LOGGER.info("--&gt;"+msg);
					LOGGER.info(TO_NODE+"--&gt;"+toNode);
					return msg;
				}
			});
			
			LOGGER.info("send message to " + destination + " successfully!");
		} catch (Throwable t) {
			LOGGER.error("Error:" + t.getMessage(), t);
		}
	}

	// ----------------- setter / getter
	public JmsTemplate getJmsTemplate() {
		return jmsTemplate;
	}

	public void setJmsTemplate(JmsTemplate jmsTemplate) {
		this.jmsTemplate = jmsTemplate;
	}

	public Destination getDestination() {
		return destination;
	}

	public void setDestination(Destination destination) {
		this.destination = destination;
	}

	public static Logger getLogger() {
		return LOGGER;
	}
}
</pre>
<p>&nbsp;</p>
<p>发送消息的main函数类</p>
<p>&nbsp;</p>
<pre name="code" class="java">/**
 * &lt;pre&gt;
 * &lt;/pre&gt;
 */
package com.wanmei.jms.spring.selector.config.sender;

import org.apache.log4j.Logger;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

/**
 * &lt;pre&gt;
 * date 2012-12-20
 * &lt;/pre&gt;
 */
public class BootstrapSender {
	private static final Logger LOGGER = Logger
			.getLogger(BootstrapSender.class);

	/**
	 * &lt;pre&gt;
	 * @param args
	 * &lt;/pre&gt;
	 */
	public static void main(String[] args) {
		LOGGER.info("start to work and initialize spring frame.");
		String configLocation = "E:/workspace_java/hornetq/src/com/wanmei/jms/spring/selector/config/sender/applicationContext.xml";
		ApplicationContext applicationContext = new FileSystemXmlApplicationContext(
				configLocation);
		LOGGER.info("initialize spring frame successfully!");
		Sender sender = applicationContext.getBean("sender", Sender.class);
		for (int i = 0; i &lt; 10; i++) {
			Msg msg = createMessage(i);
			sender.send(msg.getMessage() + "-" + i, msg.getFromNode(), msg.getToNode());
		}
	}

	private static Msg createMessage(int i) {
		String base1 = "127.0.0.1";
		String base2 = "127.0.0.2";
		String message = message(base1);
		String fromNode = from(base1);
		String toNode = to(base2);
		if (i % 2 == 0) {
			message = message(base2);
			fromNode = from(base2);
			toNode = to(base1);
		}
		return new Msg(message, fromNode, toNode);
	}

	private static String message(String str) {
		return "send " + str;
	}

	private static String from(String str) {
		return "from " + str;
	}

	private static String to(String str) {
		return "to " + str;
	}

}

class Msg {
	private String message;
	private String fromNode;
	private String toNode;

	/**
	 * &lt;pre&gt;
	 * &lt;/pre&gt;
	 */
	public Msg() {
		super();
	}

	/**
	 * &lt;pre&gt;
	 * @param message
	 * @param fromNode
	 * @param toNode
	 * &lt;/pre&gt;
	 */
	public Msg(String message, String fromNode, String toNode) {
		super();
		this.message = message;
		this.fromNode = fromNode;
		this.toNode = toNode;
	}

	public String getMessage() {
		return message;
	}

	public void setMessage(String message) {
		this.message = message;
	}

	public String getFromNode() {
		return fromNode;
	}

	public void setFromNode(String fromNode) {
		this.fromNode = fromNode;
	}

	public String getToNode() {
		return toNode;
	}

	public void setToNode(String toNode) {
		this.toNode = toNode;
	}

}
</pre>
<p>&nbsp;</p>
<p>&nbsp;用到的一个接口类：</p>
<p>&nbsp;</p>
<pre name="code" class="java">/**
 * &lt;pre&gt;
 * &lt;/pre&gt;
 */
package com.wanmei.jms.spring.selector.java;

/**
 * &lt;pre&gt;
 * date 2012-12-20
 * &lt;/pre&gt;
 */
public interface State {
	public final static String FROM_NODE = "FROM_NODE";
	public final static String TO_NODE = "TO_NODE";
}</pre>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>------------------------------------------------------ 开始接收消息-------------------------------------</p>
<p>接收的spring的配置文件：</p>
<p>&nbsp;</p>
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

	&lt;bean id="selectorQueue" class="org.hornetq.api.jms.HornetQJMSClient"
		factory-method="createQueue"&gt;
		&lt;constructor-arg value="org.spring.jms.selector.queue" /&gt;
	&lt;/bean&gt;
	
	&lt;bean id="transportConfiguration" class="org.hornetq.api.core.TransportConfiguration"&gt;
		&lt;constructor-arg
			value="org.hornetq.core.remoting.impl.netty.NettyConnectorFactory" /&gt;
		&lt;constructor-arg&gt;
			&lt;map key-type="java.lang.String" value-type="java.lang.Object"&gt;
				&lt;entry key="host" value="localhost"&gt;&lt;/entry&gt;
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
	
	&lt;bean id="receiveListener" class="com.wanmei.jms.spring.selector.java.ReceiveListener"/&gt;
	
&lt;bean id="jmsContainer" class="org.springframework.jms.listener.DefaultMessageListenerContainer"&gt;
	    &lt;property name="connectionFactory" ref="connectionFactory"/&gt;
	    &lt;property name="destination" ref="selectorQueue"/&gt;
	    &lt;property name="messageListener" ref="receiveListener"/&gt;
	    &lt;property name="messageSelector" value="TO_NODE='to 127.0.0.1'"/&gt;
	&lt;/bean&gt;
&lt;/beans&gt;</pre>
<p>&nbsp;</p>
<p>&nbsp;实现了MessageListener接口的类：</p>
<p>&nbsp;</p>
<pre name="code" class="java">/**
 * &lt;pre&gt;
 * &lt;/pre&gt;
 */
package com.wanmei.jms.spring.selector.java;

import javax.jms.JMSException;
import javax.jms.Message;
import javax.jms.MessageListener;
import javax.jms.TextMessage;

import org.apache.log4j.Logger;

/**
 * &lt;pre&gt;
 * date 2012-12-20
 * &lt;/pre&gt;
 */
public class ReceiveListener implements MessageListener, State {
	private static final Logger LOGGER = Logger
			.getLogger(ReceiveListener.class);

	/*
	 * (non-Javadoc)
	 * 
	 * @see javax.jms.MessageListener#onMessage(javax.jms.Message)
	 */
	@Override
	public void onMessage(Message msg) {
		try {
			// LOGGER.info("start to receive from " + msg.getJMSDestination());
			TextMessage message = (TextMessage) msg;
			String fromNode = message.getStringProperty(FROM_NODE);
			String toNode = message.getStringProperty(TO_NODE);
			LOGGER.info("receive message from " + message.getJMSDestination()
					+ ", msg : " + message.getText() + ", fromNode : " + fromNode
					+ ", toNode : " + toNode);
		} catch (JMSException e) {
			LOGGER.error("Error" + e.getMessage(), e);
		}
	}

}
</pre>
<p>&nbsp;</p>
<p>&nbsp;含有main函数的引导类：</p>
<p>&nbsp;</p>
<pre name="code" class="java">/**
 * &lt;pre&gt;
 * &lt;/pre&gt;
 */
package com.wanmei.jms.spring.selector;

import org.apache.log4j.Logger;
import org.springframework.context.support.FileSystemXmlApplicationContext;

/**
 * &lt;pre&gt;
 * date 2012-12-20
 * &lt;/pre&gt;
 */
public class Bootstrap {
	private static final Logger LOGGER = Logger
			.getLogger(Bootstrap.class);
	/**
	 *&lt;pre&gt;
	 * @param args
	 *&lt;/pre&gt;
	 */
	public static void main(String[] args) {
		LOGGER.info("start to work and initialize spring frame.");
		String configLocation = "E:/workspace_tmp_copy/hornetq/src/com/wanmei/jms/spring/selector/config/receiver/c1/applicationContext.xml";
		new FileSystemXmlApplicationContext(configLocation);
		LOGGER.info("initialize spring frame successfully!");
		LOGGER.info("spring : " + configLocation);
	}

}
</pre>
<p>&nbsp;</p>
<p>------------ 备注：</p>
<p>上面接收的spring的配置文件还可以采取另一种 JMS Namespace Support 来进行配置，注意<span style="white-space: pre;"> </span>destination="org.spring.jms.selector.queue" 这里是queue的名称，不是引用</p>
<p>配置文件如下：</p>
<p>&nbsp;</p>
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

	
	&lt;bean id="transportConfiguration" class="org.hornetq.api.core.TransportConfiguration"&gt;
		&lt;constructor-arg
			value="org.hornetq.core.remoting.impl.netty.NettyConnectorFactory" /&gt;
		&lt;constructor-arg&gt;
			&lt;map key-type="java.lang.String" value-type="java.lang.Object"&gt;
				&lt;entry key="host" value="localhost"&gt;&lt;/entry&gt;
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

	
	&lt;bean id="receiveListener" class="com.wanmei.jms.spring.selector.java.ReceiveListener"/&gt;

	&lt;jms:listener-container connection-factory="connectionFactory"
                        concurrency="10"&gt;
	    &lt;jms:listener destination="org.spring.jms.selector.queue" ref="receiveListener" selector="TO_NODE='to 127.0.0.1'"/&gt;
	&lt;/jms:listener-container&gt;
	
&lt;/beans&gt;</pre>
<p> &nbsp;具体内容请参考spring.3.1的reference的文档</p>