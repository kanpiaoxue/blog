#spring  用JavaBean 配置List、Map、Set等java容器
###发表时间：2011-11-02
###分类：Spring
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1231120" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1231120</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>用数值配置spring装配的JavaBean内部的List类型很容易，下面介绍如何用javabean装配JavaBean中的List</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public class Element implements Serializable{
	/**
	 *
	 */
	private static final long serialVersionUID = -6956332143541075576L;
	private Integer id;
	private String name;
	private String url;
	public Integer getId() {
		return id;
	}
	public void setId(Integer id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getUrl() {
		return url;
	}
	public void setUrl(String url) {
		this.url = url;
	}
	
}</pre> 
 <p>&nbsp;public class Test {</p> 
 <pre name="code" class="java">	private List&lt;Element&gt; elementList;
	
	
	public List&lt;Element&gt; getElementList() {
		return elementList;
	}


	public void setElementList(List&lt;Element&gt; elementList) {
		this.elementList = elementList;
	}


	/**
	 * @param args
	 */
	public static void main(String[] args) {
		String[] configLocations = {"E:\\test.xml"};
		ApplicationContext applicationContext = new FileSystemXmlApplicationContext(configLocations);
		Test test = (Test)applicationContext.getBean("test");
		List&lt;Element&gt; elList = test.getElementList();
		for(Element el : elList){
			System.out.println(el.getId() + " , " + el.getName() + " , " + el.getUrl());
		}
	}

}</pre> 
 <p>&nbsp;&lt;?xml version="1.0" encoding="UTF-8"?&gt;</p> 
 <pre name="code" class="xml">&lt;beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:tx="http://www.springframework.org/schema/tx"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-2.5.xsd
                      http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-2.5.xsd
                      http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-2.5.xsd"&gt;

	&lt;bean id="element0" class="com.beantest.Element"&gt;
		&lt;property name="id" value="1001"/&gt;
		&lt;property name="name" value="hello"/&gt;
		&lt;property name="url" value="http://www.baidu.com/"/&gt;
	&lt;/bean&gt;
	&lt;bean id="element1" class="com.beantest.Element"&gt;
		&lt;property name="id" value="1002"/&gt;
		&lt;property name="name" value="world"/&gt;
		&lt;property name="url" value="http://www.google.com/"/&gt;
	&lt;/bean&gt;
	&lt;bean id="test" class="com.beantest.Test"&gt;
		&lt;property name="elementList"&gt;
			&lt;list&gt;
				&lt;ref bean="element0" /&gt;
				&lt;ref bean="element1" /&gt;
			&lt;/list&gt;
		&lt;/property&gt;
	&lt;/bean&gt;
&lt;/beans&gt;</pre> 
 <p>&nbsp;这样，两个bean element0和element1就被装配到了bean test里面。</p> 
 <pre name="code" class="xml">&lt;bean id="moreComplexObject" class="example.ComplexObject"&gt;
    &lt;!-- results in a setAdminEmails(java.util.Properties) call --&gt;
    &lt;property name="adminEmails"&gt;
        &lt;props&gt;
            &lt;prop key="administrator"&gt;administrator@example.org&lt;/prop&gt;
            &lt;prop key="support"&gt;support@example.org&lt;/prop&gt;
            &lt;prop key="development"&gt;development@example.org&lt;/prop&gt;
        &lt;/props&gt;
    &lt;/property&gt;
    &lt;!-- results in a setSomeList(java.util.List) call --&gt;
    &lt;property name="someList"&gt;
        &lt;list&gt;
            &lt;value&gt;a list element followed by a reference&lt;/value&gt;
            &lt;ref bean="myDataSource" /&gt;
        &lt;/list&gt;
    &lt;/property&gt;
    &lt;!-- results in a setSomeMap(java.util.Map) call --&gt;
    &lt;property name="someMap"&gt;
        &lt;map&gt;
            &lt;entry key="an entry" value="just some string"/&gt;
            &lt;entry key ="a ref" value-ref="myDataSource"/&gt;
        &lt;/map&gt;
    &lt;/property&gt;
    &lt;!-- results in a setSomeSet(java.util.Set) call --&gt;
    &lt;property name="someSet"&gt;
        &lt;set&gt;
            &lt;value&gt;just some string&lt;/value&gt;
            &lt;ref bean="myDataSource" /&gt;
        &lt;/set&gt;
    &lt;/property&gt;
&lt;/bean&gt;</pre> 
 <p>&nbsp;</p> 
 <p>spring直接在xml里面声明List，如下：</p> 
 <pre name="code" class="xml">	&lt;bean id="dmapScheduleframeworkCallbackUrls" class="java.util.ArrayList"&gt;
		&lt;constructor-arg index="1"&gt;
			&lt;list&gt;
				&lt;value&gt;localhost:8080&lt;/value&gt;
				&lt;value&gt;localhost:8081&lt;/value&gt;
				&lt;value&gt;localhost:8082&lt;/value&gt;
			&lt;/list&gt;
		&lt;/constructor-arg&gt;
	&lt;/bean&gt;</pre> 
 <p>&nbsp;</p> 
</div>