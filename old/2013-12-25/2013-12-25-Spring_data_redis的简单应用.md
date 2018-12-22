#Spring data redis的简单应用
###发表时间：2013-12-25
###分类：Spring,redis,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1995424" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1995424</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>这里给出了一个简单封装的 RedisService 服务类。</p> 
 <pre name="code" class="java">package com.wanmei.redis.test.service;

import java.util.Collection;
import java.util.Set;

/**
 * &lt;pre&gt;
 * @author xuepeng&lt;br&gt;
 * @date 2013年12月25日&lt;br&gt;
 * @Copyright wanmei.com [2004-2013]&lt;br&gt;
 * @Description redis 的服务接口
 * &lt;/pre&gt;
 */
public interface RedisService {
	/**
	 * &lt;pre&gt;
	 * 通过key删除
	 * @param keys
	 * @return 被删除的记录数
	 * &lt;/pre&gt;
	 */
	public long delete(String... keys);

	/**
	 * &lt;pre&gt;
	 * 通过keys删除
	 * @param keys
	 * @return 被删除的记录数
	 * &lt;/pre&gt;
	 */
	public long delete(Collection&lt;String&gt; keys);

	/**
	 * &lt;pre&gt;
	 *  @param key
	 *  @param value
	 *  @param activeTime 秒
	 *  @return 添加key value 并且设置存活时间
	 * &lt;/pre&gt;
	 */
	public boolean set(byte[] key, byte[] value, long activeTime);

	/**
	 * &lt;pre&gt;
	 * @param key
	 * @param value
	 * @param activeTime 秒
	 * @return 添加key value 并且设置存活时间
	 * &lt;/pre&gt;
	 */
	public boolean set(String key, String value, long activeTime);

	/**
	 * &lt;pre&gt;
	 *  @param key
	 *  @param value
	 *  @return 添加key value
	 * &lt;/pre&gt;
	 */
	public boolean set(String key, String value);

	/**
	 * &lt;pre&gt;
	 *  @param key
	 *  @param value
	 *  @return 添加key value
	 * &lt;/pre&gt;
	 */
	public boolean set(byte[] key, byte[] value);

	/**
	 * &lt;pre&gt;
	 * @param key
	 * @return 获得value
	 * &lt;/pre&gt;
	 */
	public String get(String key);

	/**
	 * &lt;pre&gt;
	 * @param pattern
	 * @return 通过正则匹配keys
	 * &lt;/pre&gt;
	 */
	public Set&lt;String&gt; matchKeys(String pattern);

	/**
	 * &lt;pre&gt;
	 * @param key
	 * @return 检查key是否已经存在
	 * &lt;/pre&gt;
	 */
	public boolean exists(String key);

	/**
	 * &lt;pre&gt;
	 * @return 清空所有数据
	 * &lt;/pre&gt;
	 */
	public boolean flushDB();

}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">package com.wanmei.redis.test.service.impl;

import java.io.Serializable;
import java.io.UnsupportedEncodingException;
import java.util.ArrayList;
import java.util.Collection;
import java.util.Set;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.dao.DataAccessException;
import org.springframework.data.redis.connection.RedisConnection;
import org.springframework.data.redis.core.RedisCallback;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.stereotype.Service;

import com.wanmei.redis.test.service.RedisService;

/**
 * &lt;pre&gt;
 * @author xuepeng&lt;br&gt;
 * @date 2013年12月25日&lt;br&gt;
 * @Copyright wanmei.com [2004-2013]&lt;br&gt;
 * @Description Redis 服务实现类
 * &lt;/pre&gt;
 */
@Service(value = "redisService")
public class RedisServiceImpl implements RedisService {

	private static final String CHARSET = "UTF8";

	@Autowired
	private RedisTemplate&lt;String, Serializable&gt; redisTemplate;

	public void setRedisTemplate(
			RedisTemplate&lt;String, Serializable&gt; redisTemplate) {
		this.redisTemplate = redisTemplate;
	}

	@Override
	public boolean set(final byte[] key, final byte[] value,
			final long activeTime) {
		return redisTemplate.execute(new RedisCallback&lt;Boolean&gt;() {
			public Boolean doInRedis(RedisConnection connection)
					throws DataAccessException {
				boolean rs = true;
				connection.set(key, value);
				if (activeTime &gt; 0) {
					rs = connection.expire(key, activeTime);
				}
				return rs;
			}
		});
	}

	@Override
	public boolean set(String key, String value, long activeTime) {
		return this.set(key.getBytes(), value.getBytes(), activeTime);
	}

	@Override
	public boolean set(String key, String value) {
		return this.set(key, value, 0L);
	}

	@Override
	public boolean set(byte[] key, byte[] value) {
		return this.set(key, value, 0L);
	}

	@Override
	public String get(final String key) {
		return redisTemplate.execute(new RedisCallback&lt;String&gt;() {
			public String doInRedis(RedisConnection connection)
					throws DataAccessException {
				try {
					byte[] value = connection.get(key.getBytes());
					return value == null ? "" : new String(value, CHARSET);
				} catch (UnsupportedEncodingException e) {
					e.printStackTrace();
				}
				return "";
			}
		});
	}

	@Override
	public Set&lt;String&gt; matchKeys(String pattern) {
		return redisTemplate.keys(pattern);

	}

	@Override
	public boolean exists(final String key) {
		return redisTemplate.execute(new RedisCallback&lt;Boolean&gt;() {
			public Boolean doInRedis(RedisConnection connection)
					throws DataAccessException {
				return connection.exists(key.getBytes());
			}
		});
	}

	@Override
	public boolean flushDB() {
		return redisTemplate.execute(new RedisCallback&lt;Boolean&gt;() {
			public Boolean doInRedis(RedisConnection connection)
					throws DataAccessException {
				connection.flushDb();
				return true;
			}
		});
	}

	@Override
	public long delete(final Collection&lt;String&gt; keys) {
		return redisTemplate.execute(new RedisCallback&lt;Long&gt;() {
			public Long doInRedis(RedisConnection connection)
					throws DataAccessException {
				long result = 0;
				for (String key : keys) {
					result = connection.del(key.getBytes());
				}
				return result;
			}
		});
	}

	@Override
	public long delete(final String... keys) {
		Collection&lt;String&gt; cols = new ArrayList&lt;String&gt;();
		for (String key : keys) {
			cols.add(key);
		}
		return this.delete(cols);
	}

}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">package com.wanmei.redis;

import static org.junit.Assert.assertEquals;

import org.junit.Before;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import com.alibaba.fastjson.JSON;
import com.google.common.base.Strings;
import com.wanmei.redis.test.bean.User;
import com.wanmei.redis.test.service.RedisService;

/**
 * &lt;pre&gt;
 * @author xuepeng&lt;br&gt;
 * @date 2013年12月25日&lt;br&gt;
 * @Copyright wanmei.com [2004-2013]&lt;br&gt;
 * @Description 单元测试类
 * &lt;/pre&gt;
 */
public class UserServiceTest {
	private ApplicationContext app;
	private RedisService redisService;

	@Before
	public void before() throws Exception {
		app = new ClassPathXmlApplicationContext(
				"com/wanmei/redis/spring-ctx-application.xml");
		redisService = (RedisService) app.getBean("redisService");
	}

	@Test
	public void crud() {
		for (;;) {
			System.out.println(Strings.repeat("-", 50));
			// -------------- Create ---------------
			String address1 = Strings.repeat("上海", 50);
			User user = new User();
			user.setAddress(address1);
			user.setUid("u123456");

			String key = toJSONString(user);
			String value = key;

			long beforeSave = System.currentTimeMillis();
			redisService.set(key, value);
			System.out.println("save consumes : "
					+ (System.currentTimeMillis() - beforeSave));

			// ---------------Read ---------------
			long beforeRead = System.currentTimeMillis();
			String r1 = redisService.get(key);
			System.out.println("read consumes : "
					+ (System.currentTimeMillis() - beforeRead));
			user = parse(r1, User.class);
			System.out.println("address1=" + user.getAddress());
			assertEquals(address1, user.getAddress());

			// --------------Update ------------
			String address2 = "北京";
			user.setAddress(address2);
			final String key1 = toJSONString(user);
			String value1 = key1;
			redisService.set(key1, value1);
			String r2 = redisService.get(key1);
			user = parse(r2, User.class);
			System.out.println("address2Save=" + user.getAddress());
			assertEquals(address2, user.getAddress());

			// --------------Delete ------------
			long beforeDelete = System.currentTimeMillis();
			long rs = redisService.delete(key1);
			System.out.println("delete record's count : " + rs);

			System.out.println("delete consumes : "
					+ (System.currentTimeMillis() - beforeDelete));
			String r3 = redisService.get(key1);
			System.out.println("addressdel=" + r3);
			assertEquals("", r3);

			// -------------exist----------------
			user.setAddress("呵呵");
			user.setUid("哈哈哈");
			String lastKey = user.toString();
			redisService.set(lastKey, lastKey);
			boolean r4 = redisService.exists(lastKey);
			assertEquals(true, r4);

			// -------------flushDB----------------
			System.out.println("flushDB:" + redisService.flushDB());
			String r5 = redisService.get(lastKey);
			assertEquals("", r5);

		}
	}

	private static String toJSONString(Object t) {
		return JSON.toJSONString(t);
	}

	private static &lt;T&gt; T parse(String text, Class&lt;T&gt; clazz) {
		return JSON.parseObject(text, clazz);
	}
}</pre> 
 <p>下面是Spring的XML配置：</p> 
 <p>&nbsp; &nbsp;spring-ctx-application.xml</p> 
 <pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:jdbc="http://www.springframework.org/schema/jdbc" xmlns:jee="http://www.springframework.org/schema/jee"
	xmlns:jms="http://www.springframework.org/schema/jms" xmlns:lang="http://www.springframework.org/schema/lang"
	xmlns:mvc="http://www.springframework.org/schema/mvc" xmlns:oxm="http://www.springframework.org/schema/oxm"
	xmlns:p="http://www.springframework.org/schema/p" xmlns:sec="http://www.springframework.org/schema/security"
	xmlns:task="http://www.springframework.org/schema/task" xmlns:tx="http://www.springframework.org/schema/tx"
	xmlns:util="http://www.springframework.org/schema/util" xmlns:cache="http://www.springframework.org/schema/cache"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.0.xsd
		http://www.springframework.org/schema/jdbc http://www.springframework.org/schema/jdbc/spring-jdbc-3.0.xsd
		http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-3.0.xsd
		http://www.springframework.org/schema/jms http://www.springframework.org/schema/jms/spring-jms-3.0.xsd
		http://www.springframework.org/schema/lang http://www.springframework.org/schema/lang/spring-lang-3.0.xsd
		http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd
		http://www.springframework.org/schema/oxm http://www.springframework.org/schema/oxm/spring-oxm-3.0.xsd
		http://www.springframework.org/schema/security http://www.springframework.org/schema/security/spring-security-3.0.xsd
		http://www.springframework.org/schema/task http://www.springframework.org/schema/task/spring-task-3.0.xsd
		http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.0.xsd
		http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util-3.0.xsd
		http://www.springframework.org/schema/cache http://www.springframework.org/schema/cache/spring-cache.xsd"&gt;

	&lt;context:annotation-config /&gt;
	&lt;context:component-scan base-package="com.wanmei.redis"&gt;&lt;/context:component-scan&gt;
	&lt;context:property-placeholder
		location="classpath:com/wanmei/redis/test/config/redis.properties" /&gt;
	&lt;!-- 对象池配置： --&gt;
	&lt;bean id="jedisPoolConfig" class="redis.clients.jedis.JedisPoolConfig"&gt;
		&lt;property name="maxActive" value="${redis.pool.maxActive}" /&gt;
		&lt;property name="maxIdle" value="${redis.pool.maxIdle}" /&gt;
		&lt;property name="maxWait" value="${redis.pool.maxWait}" /&gt;
	&lt;/bean&gt;
	&lt;!-- 工厂实现： --&gt;
	&lt;bean id="jedisConnectionFactory"
		class="org.springframework.data.redis.connection.jedis.JedisConnectionFactory"&gt;
		&lt;property name="hostName" value="${redis.ip}" /&gt;
		&lt;property name="port" value="${redis.port}" /&gt;
		&lt;property name="poolConfig" ref="jedisPoolConfig" /&gt;
	&lt;/bean&gt;

	&lt;!--模板类： --&gt;
	&lt;bean id="redisTemplate" class="org.springframework.data.redis.core.RedisTemplate"
		p:connection-factory-ref="jedisConnectionFactory" /&gt;


&lt;/beans&gt;
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp; &nbsp; &nbsp;redis.properties</p> 
 <pre name="code" class="java">redis.pool.maxActive=1000
redis.pool.maxIdle=100
redis.pool.maxWait=500

redis.ip=test-server
redis.port=6379</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>