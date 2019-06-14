#Properties读取配置文件
###发表时间：2012-11-17
###分类：java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1728414" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1728414</a>

---

<p>Properties 是java自带的读取配置文件的工具类。</p>
<p>&nbsp;</p>
<p>/com/test/properties/test.properties 是一个准备好的properties文件，内容如下：</p>
<p> </p>
<pre name="code" class="java">hello_1=world1
hello_2=world2
hello_3=world3
hello_4=world4
hello_5=world5
hello_6=world6
hello_7=world7
hello_8=world8
hello_9=world9
hello_0=world0</pre>
<p>&nbsp;</p>
<p>java的源码如下：</p>
<p> </p>
<pre name="code" class="java">public class PropertiesTest {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		PropertiesTest test = new PropertiesTest();
		test.setProperty();

	}

	private void setProperty() {
		String fileName = "/com/test/properties/test.properties";
		InputStream in = PropertiesTest.class.getResourceAsStream(fileName);
		Properties properties = new Properties();
		try {
			properties.load(in);

			// 读取出所有properties的内容，并设置为系统变量
			// Register the properties as system properties
			Enumeration&lt;?&gt; enumeration = properties.propertyNames();
			while (enumeration.hasMoreElements()) {
				String name = (String) enumeration.nextElement();
				String value = properties.getProperty(name);
				if (value != null) {
					System.out.println(name + "=" + value);
					System.setProperty(name, value);
				}
			}

		} catch (IOException e) {
			e.printStackTrace();
		}
	}

}</pre>