#XStream和JAXB的示例：java和xml的互相转换
###发表时间：2019-04-03
###分类：java,经验,XStream,XML,JAXB
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2439719" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2439719</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;"><span style="font-size: 16px;">XStream</span>：</p> 
 <p style="font-size: 14px;">官网： <a href="http://x-stream.github.io">http://x-stream.github.io</a></p> 
 <p style="font-size: 14px;">教程： <a href="http://www.studytrails.com/java/xml/xstream/xstream-introduction">http://www.studytrails.com/java/xml/xstream/xstream-introduction</a></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">示例代码结构：</p> 
 <div class="quote_div" style="font-size: 14px;">
  .
  <br>├── XStreamExample.java
  <br>├── bean
  <br>│&nbsp;&nbsp; ├── Address.java
  <br>│&nbsp;&nbsp; └── Person.java
  <br>└── convert
  <br>&nbsp; &nbsp; &nbsp; &nbsp;└── SingleValueDateConverter.java
 </div> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">package org.kanpiaoxue.learn.xstream;

import org.kanpiaoxue.learn.xstream.bean.Address;
import org.kanpiaoxue.learn.xstream.bean.Person;

import com.google.common.collect.Lists;
import com.thoughtworks.xstream.XStream;
import com.thoughtworks.xstream.io.xml.DomDriver;

import java.io.IOException;
import java.io.StringWriter;
import java.io.Writer;
import java.util.Date;
import java.util.List;

/**
 * @ClassName: XStreamExample
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2019/04/03 10:25:51
 * @Description: XStream示例类
 *               官网： http://x-stream.github.io
 *               教程：
 *               http://www.studytrails.com/java/xml/xstream/xstream-introduction/
 */
public class XStreamExample {
    public static void main(String[] args) throws IOException {
        /**
         * &lt;pre&gt;
         * 警告信息：Security framework of XStream not initialized, XStream is probably vulnerable.
         * 原因分析：防止被攻击引起安全问题
         * 参考资料： http://x-stream.github.io/security.html#example
         * 解决方案：设置安全策略和允许序列化和反序列的类型范围
         * XStream.setupDefaultSecurity(xstream);
         * xstream.allowTypes(new Class[] { Person.class, Address.class });
         * &lt;/pre&gt;
         */
        XStream xstream = new XStream(new DomDriver());
        XStream.setupDefaultSecurity(xstream);
        xstream.allowTypes(new Class[] { Person.class, Address.class });
        xstream.ignoreUnknownElements();
        xstream.processAnnotations(Person.class);

        String country = "中国";
        Address a1 = new Address(country, "北京市", "北京市", "海淀区", "中关村南大街1号");
        Address a2 = new Address(country, "江苏省", "南京市", "无名区", "总统府大街1号");
        List&lt;Address&gt; addresses = Lists.newArrayList(a1, a2);

        Person encodePerson = new Person(1, "薛", "仁", "贵", 70, addresses);
        encodePerson.setBirthday(new Date());
        encodePerson.setName("helloWorld");
        // 序列化
        String xml = toXML(xstream, encodePerson);
        System.out.println(xml);

        // 反序列化
        Person decodePerson = fromXML(xstream, xml);
        System.out.println(decodePerson);
    }

    private static Person fromXML(XStream xstream, String xml) throws IOException {
        /**
         * &lt;pre&gt;
         * 异常信息：Caused by: java.lang.AbstractMethodError: org.apache.xerces.jaxp.DocumentBuilderFactoryImpl.setFeature(Ljava/lang/String;Z)V
         * 异常原因：在系统中存在着多个解析器的时候，这时候程序无法选择解析器。需要人工指定解析器。
         * 解决方案：System.setProperty("javax.xml.parsers.DocumentBuilderFactory","com.sun.org.apache.xerces.internal.jaxp.DocumentBuilderFactoryImpl");
         * &lt;/pre&gt;
         */
        System.setProperty("javax.xml.parsers.DocumentBuilderFactory",
                "com.sun.org.apache.xerces.internal.jaxp.DocumentBuilderFactoryImpl");
        Person decodePerson = (Person) xstream.fromXML(xml);
        return decodePerson;
    }

    private static String toXML(XStream xstream, Person obj) throws IOException {
        try (Writer writer = new StringWriter()) {
            // 添加 xml 的 header
            writer.write("&lt;?xml version=\"1.0\" encoding=\"UTF-8\" ?&gt;\n");
            xstream.toXML(obj, writer);
            String xml = writer.toString();
            return xml;
        }
    }
}
</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">package org.kanpiaoxue.learn.xstream.bean;

import com.google.gson.GsonBuilder;
import com.thoughtworks.xstream.annotations.XStreamAlias;

/**
 * @ClassName: Address
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2019/04/03 10:26:35
 * @Description: 地址类
 */
// 如果不给类起别名，则对应的是类包名，例：org.kanpiaoxue.learn.xstream.bean.Address
@XStreamAlias("address")
public class Address {
    private String country;
    private String province;
    private String city;
    private String street;
    private String houseNumber;

    /**
     *
     */
    public Address() {
        super();
    }

    /**
     * @param country
     * @param province
     * @param city
     * @param street
     * @param houseNumber
     */
    public Address(String country, String province, String city, String street, String houseNumber) {
        super();
        this.country = country;
        this.province = province;
        this.city = city;
        this.street = street;
        this.houseNumber = houseNumber;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#equals(java.lang.Object)
     */
    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        }
        if (obj == null) {
            return false;
        }
        if (getClass() != obj.getClass()) {
            return false;
        }
        Address other = (Address) obj;
        if (city == null) {
            if (other.city != null) {
                return false;
            }
        } else if (!city.equals(other.city)) {
            return false;
        }
        if (country == null) {
            if (other.country != null) {
                return false;
            }
        } else if (!country.equals(other.country)) {
            return false;
        }
        if (houseNumber == null) {
            if (other.houseNumber != null) {
                return false;
            }
        } else if (!houseNumber.equals(other.houseNumber)) {
            return false;
        }
        if (province == null) {
            if (other.province != null) {
                return false;
            }
        } else if (!province.equals(other.province)) {
            return false;
        }
        if (street == null) {
            if (other.street != null) {
                return false;
            }
        } else if (!street.equals(other.street)) {
            return false;
        }
        return true;
    }

    /**
     * @return the city
     */
    public String getCity() {
        return city;
    }

    /**
     * @return the country
     */
    public String getCountry() {
        return country;
    }

    /**
     * @return the houseNumber
     */
    public String getHouseNumber() {
        return houseNumber;
    }

    /**
     * @return the province
     */
    public String getProvince() {
        return province;
    }

    /**
     * @return the street
     */
    public String getStreet() {
        return street;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#hashCode()
     */
    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((city == null) ? 0 : city.hashCode());
        result = prime * result + ((country == null) ? 0 : country.hashCode());
        result = prime * result + ((houseNumber == null) ? 0 : houseNumber.hashCode());
        result = prime * result + ((province == null) ? 0 : province.hashCode());
        result = prime * result + ((street == null) ? 0 : street.hashCode());
        return result;
    }

    /**
     * @param city
     *            the city to set
     */
    public void setCity(String city) {
        this.city = city;
    }

    /**
     * @param country
     *            the country to set
     */
    public void setCountry(String country) {
        this.country = country;
    }

    /**
     * @param houseNumber
     *            the houseNumber to set
     */
    public void setHouseNumber(String houseNumber) {
        this.houseNumber = houseNumber;
    }

    /**
     * @param province
     *            the province to set
     */
    public void setProvince(String province) {
        this.province = province;
    }

    /**
     * @param street
     *            the street to set
     */
    public void setStreet(String street) {
        this.street = street;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#toString()
     */
    @Override
    public String toString() {
        return new GsonBuilder().setPrettyPrinting().create().toJson(this);
    }

}
</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">package org.kanpiaoxue.learn.xstream.bean;

import org.kanpiaoxue.learn.xstream.convert.SingleValueDateConverter;

import com.google.gson.GsonBuilder;
import com.thoughtworks.xstream.annotations.XStreamAlias;
import com.thoughtworks.xstream.annotations.XStreamAsAttribute;
import com.thoughtworks.xstream.annotations.XStreamConverter;
import com.thoughtworks.xstream.annotations.XStreamOmitField;

import java.util.Date;
import java.util.List;

/**
 * @ClassName: Person
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2019/04/03 10:26:25
 * @Description: 人员类
 */
// 如果不给类起别名，则对应的是类包名，例：org.kanpiaoxue.learn.xstream.bean.Person
@XStreamAlias("person")
public class Person {
    private Integer id;
    @XStreamAlias("first_name")
    private String firstName;

    @XStreamAlias("middle_name")
    private String middleName;

    @XStreamAlias("last_name")
    private String lastName;

    @XStreamAsAttribute
    private Integer age;

    private List&lt;Address&gt; addresses;
    @XStreamConverter(SingleValueDateConverter.class)
    private Date birthday;

    @XStreamOmitField
    private String name;

    /**
     *
     */
    public Person() {
        super();
    }

    /**
     * @param id
     * @param firstName
     * @param middleName
     * @param lastName
     * @param age
     * @param addresses
     */
    public Person(Integer id, String firstName, String middleName, String lastName, Integer age,
            List&lt;Address&gt; addresses) {
        super();
        this.id = id;
        this.firstName = firstName;
        this.middleName = middleName;
        this.lastName = lastName;
        this.age = age;
        this.addresses = addresses;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#equals(java.lang.Object)
     */
    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        }
        if (obj == null) {
            return false;
        }
        if (getClass() != obj.getClass()) {
            return false;
        }
        Person other = (Person) obj;
        if (addresses == null) {
            if (other.addresses != null) {
                return false;
            }
        } else if (!addresses.equals(other.addresses)) {
            return false;
        }
        if (age == null) {
            if (other.age != null) {
                return false;
            }
        } else if (!age.equals(other.age)) {
            return false;
        }
        if (firstName == null) {
            if (other.firstName != null) {
                return false;
            }
        } else if (!firstName.equals(other.firstName)) {
            return false;
        }
        if (id == null) {
            if (other.id != null) {
                return false;
            }
        } else if (!id.equals(other.id)) {
            return false;
        }
        if (lastName == null) {
            if (other.lastName != null) {
                return false;
            }
        } else if (!lastName.equals(other.lastName)) {
            return false;
        }
        if (middleName == null) {
            if (other.middleName != null) {
                return false;
            }
        } else if (!middleName.equals(other.middleName)) {
            return false;
        }
        return true;
    }

    /**
     * @return the addresses
     */
    public List&lt;Address&gt; getAddresses() {
        return addresses;
    }

    /**
     * @return the age
     */
    public Integer getAge() {
        return age;
    }

    /**
     * @return the birthday
     */
    public Date getBirthday() {
        return birthday;
    }

    /**
     * @return the firstName
     */
    public String getFirstName() {
        return firstName;
    }

    /**
     * @return the id
     */
    public Integer getId() {
        return id;
    }

    /**
     * @return the lastName
     */
    public String getLastName() {
        return lastName;
    }

    /**
     * @return the middleName
     */
    public String getMiddleName() {
        return middleName;
    }

    /**
     * @return the name
     */
    public String getName() {
        return name;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#hashCode()
     */
    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((addresses == null) ? 0 : addresses.hashCode());
        result = prime * result + ((age == null) ? 0 : age.hashCode());
        result = prime * result + ((firstName == null) ? 0 : firstName.hashCode());
        result = prime * result + ((id == null) ? 0 : id.hashCode());
        result = prime * result + ((lastName == null) ? 0 : lastName.hashCode());
        result = prime * result + ((middleName == null) ? 0 : middleName.hashCode());
        return result;
    }

    /**
     * @param addresses
     *            the addresses to set
     */
    public void setAddresses(List&lt;Address&gt; addresses) {
        this.addresses = addresses;
    }

    /**
     * @param age
     *            the age to set
     */
    public void setAge(Integer age) {
        this.age = age;
    }

    /**
     * @param birthday
     *            the birthday to set
     */
    public void setBirthday(Date birthday) {
        this.birthday = birthday;
    }

    /**
     * @param firstName
     *            the firstName to set
     */
    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    /**
     * @param id
     *            the id to set
     */
    public void setId(Integer id) {
        this.id = id;
    }

    /**
     * @param lastName
     *            the lastName to set
     */
    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    /**
     * @param middleName
     *            the middleName to set
     */
    public void setMiddleName(String middleName) {
        this.middleName = middleName;
    }

    /**
     * @param name
     *            the name to set
     */
    public void setName(String name) {
        this.name = name;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#toString()
     */
    @Override
    public String toString() {
        return new GsonBuilder().setPrettyPrinting().create().toJson(this);
    }

}
</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">package org.kanpiaoxue.learn.xstream.convert;

import org.joda.time.DateTime;
import org.joda.time.format.DateTimeFormat;
import org.joda.time.format.DateTimeFormatter;

import com.thoughtworks.xstream.converters.Converter;
import com.thoughtworks.xstream.converters.MarshallingContext;
import com.thoughtworks.xstream.converters.UnmarshallingContext;
import com.thoughtworks.xstream.io.HierarchicalStreamReader;
import com.thoughtworks.xstream.io.HierarchicalStreamWriter;

import java.util.Date;

/**
 * @ClassName: SingleValueDateConverter
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2019/04/03 11:14:03
 * @Description: date的转换器
 */
public class SingleValueDateConverter implements Converter {
    private static final DateTimeFormatter format = DateTimeFormat.forPattern("yyyy-MM-dd HH:mm:ss");

    /*
     * (non-Javadoc)
     * @see
     * com.thoughtworks.xstream.converters.ConverterMatcher#canConvert(java.lang
     * .Class)
     */
    @Override
    public boolean canConvert(@SuppressWarnings("rawtypes") Class type) {
        return type.equals(Date.class);
    }

    /*
     * (non-Javadoc)
     * @see
     * com.thoughtworks.xstream.converters.Converter#marshal(java.lang.Object,
     * com.thoughtworks.xstream.io.HierarchicalStreamWriter,
     * com.thoughtworks.xstream.converters.MarshallingContext)
     */
    @Override
    public void marshal(Object source, HierarchicalStreamWriter writer, MarshallingContext context) {
        Date date = (Date) source;
        DateTime d = new DateTime(date);
        writer.setValue(d.toString(format));
    }

    /*
     * (non-Javadoc)
     * @see
     * com.thoughtworks.xstream.converters.Converter#unmarshal(com.thoughtworks.
     * xstream.io.HierarchicalStreamReader,
     * com.thoughtworks.xstream.converters.UnmarshallingContext)
     */
    @Override
    public Object unmarshal(HierarchicalStreamReader reader, UnmarshallingContext context) {
        String str = reader.getValue();
        DateTime d = format.parseDateTime(str);
        return d.toDate();
    }

}
</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;输出内容：</p> 
 <p style="font-size: 14px;">xml：</p> 
 <pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8" ?&gt;
&lt;person age="70"&gt;
  &lt;id&gt;1&lt;/id&gt;
  &lt;first__name&gt;薛&lt;/first__name&gt;
  &lt;middle__name&gt;仁&lt;/middle__name&gt;
  &lt;last__name&gt;贵&lt;/last__name&gt;
  &lt;addresses&gt;
    &lt;address&gt;
      &lt;country&gt;中国&lt;/country&gt;
      &lt;province&gt;北京市&lt;/province&gt;
      &lt;city&gt;北京市&lt;/city&gt;
      &lt;street&gt;海淀区&lt;/street&gt;
      &lt;houseNumber&gt;中关村南大街1号&lt;/houseNumber&gt;
    &lt;/address&gt;
    &lt;address&gt;
      &lt;country&gt;中国&lt;/country&gt;
      &lt;province&gt;江苏省&lt;/province&gt;
      &lt;city&gt;南京市&lt;/city&gt;
      &lt;street&gt;无名区&lt;/street&gt;
      &lt;houseNumber&gt;总统府大街1号&lt;/houseNumber&gt;
    &lt;/address&gt;
  &lt;/addresses&gt;
  &lt;birthday&gt;2019-04-03 11:42:56&lt;/birthday&gt;
&lt;/person&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">json：</p> 
 <pre name="code" class="js">{
  "id": 1,
  "firstName": "薛",
  "middleName": "仁",
  "lastName": "贵",
  "age": 70,
  "addresses": [
    {
      "country": "中国",
      "province": "北京市",
      "city": "北京市",
      "street": "海淀区",
      "houseNumber": "中关村南大街1号"
    },
    {
      "country": "中国",
      "province": "江苏省",
      "city": "南京市",
      "street": "无名区",
      "houseNumber": "总统府大街1号"
    }
  ],
  "birthday": "Apr 3, 2019 11:42:56 AM"
}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;"><span style="font-family: 'Courier New'; font-size: 16px;"><span style="font-family: SimHei, 黑体, tahoma, arial, helvetica, sans-serif;">JAXB</span>：</span>除了XStream之外，jdk也提供了类似的功能<span style="font-family: 'Courier New'; font-size: 16px;">JAXB（</span><span class="s1" style="font-family: 'Courier New'; font-size: 16px;">Java</span><span style="font-family: 'Courier New'; font-size: 16px;"> Architecture </span><span class="s2" style="font-family: 'Courier New'; font-size: 16px;"><strong>for</strong></span><span class="s1" style="font-family: 'Courier New'; font-size: 16px;">XML</span><span class="s1" style="font-family: 'Courier New'; font-size: 16px;">Binding</span><span class="s1" style="font-family: 'Courier New'; font-size: 16px;">(JAXB)）</span>。</p> 
 <p>官网： Java Architecture for XML Binding，<a href="https://docs.oracle.com/javase/8/docs/technotes/guides/xml/jaxb/index.html">https://docs.oracle.com/javase/8/docs/technotes/guides/xml/jaxb/index.html</a></p> 
 <p>oracle提供的官网教程： <a href="https://docs.oracle.com/javase/tutorial/jaxb/intro/index.html">https://docs.oracle.com/javase/tutorial/jaxb/intro/index.html</a></p> 
 <p>参考教程： <a href="https://www.baeldung.com/jaxb">https://www.baeldung.com/jaxb</a></p> 
 <p>&nbsp;</p> 
 <p style="font-size: 14px;">举例如下：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">public static void main(String[] args) throws IOException {
    String country = "中国=====";
    Address a1 = new Address(country, "北京市", "北京市", "海淀区", "中关村南大街1号");
    Address a2 = new Address(country, "江苏省", "南京市", "无名区", "总统府大街1号");
    List&lt;Address&gt; addresses = Lists.newArrayList(a1, a2);

    Person encodePerson = new Person(1, "薛", "仁", "贵", 70, addresses);
    encodePerson.setBirthday(new Date());
    encodePerson.setName("helloWorld");

    File file = new File(
            "hello.xml");
    System.out.println(file);
    // 序列化 to file
    JAXB.marshal(encodePerson, file);
    Files.readAllLines(Paths.get(file.getAbsolutePath())).forEach(System.out::println);

    System.setProperty("org.xml.sax.driver", "com.sun.org.apache.xerces.internal.parsers.SAXParser");
    System.setProperty("javax.xml.parsers.DocumentBuilderFactory",
            "com.sun.org.apache.xerces.internal.jaxp.DocumentBuilderFactoryImpl");
    System.setProperty("javax.xml.parsers.SAXParserFactory",
            "com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl");

    // 反序列化 from file
    Person newPerson = JAXB.unmarshal(file, Person.class);
    System.out.println(newPerson);

    // 序列化 to String
    String xml = null;
    try (StringWriter writer = new StringWriter()) {
        JAXB.marshal(encodePerson, writer);
        xml = writer.toString();
        System.out.println(xml);
    }
    // 反序列化 from String
    try (StringReader reader = new StringReader(xml)) {
        Person newPerson1 = JAXB.unmarshal(reader, Person.class);
        System.out.println(newPerson1);
    }

}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>