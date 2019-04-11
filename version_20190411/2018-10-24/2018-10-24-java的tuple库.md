#java的tuple库
###发表时间：2018-10-24
###分类：java,tuple
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2432656" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2432656</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p style="line-height: 1.3em; font-size: 13px; font-family: Verdana, Helvetica, Arial, sans-serif;">avatuples is one of the simplest java libraries ever made. Its aim is to provide a set of java classes that allow you to work with&nbsp;<em>tuple</em>s.</p> 
 <p style="line-height: 1.3em; font-size: 13px; font-family: Verdana, Helvetica, Arial, sans-serif;"><strong>Tuples? What are tuples?</strong></p> 
 <p style="line-height: 1.3em; font-size: 13px; font-family: Verdana, Helvetica, Arial, sans-serif;">A tuple is just a sequence of objects that do not necessarily relate to each other in any way. For example:&nbsp;<tt>[23, "Saturn", java.sql.Connection@li734s]</tt>&nbsp;can be considered a tuple of three elements (a&nbsp;<em>triplet</em>) containing an Integer, a String, and a JDBC Connection object. As simple as that.</p> 
 <p style="line-height: 1.3em; font-size: 13px; font-family: Verdana, Helvetica, Arial, sans-serif;">&nbsp;</p> 
 <p>地址：&nbsp;<a href="https://www.javatuples.org/">https://www.javatuples.org/</a></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">&lt;!-- <a href="https://mvnrepository.com/artifact/org.javatuples/javatuples">https://mvnrepository.com/artifact/org.javatuples/javatuples</a> --&gt;
&lt;dependency&gt;
    &lt;groupId&gt;org.javatuples&lt;/groupId&gt;
    &lt;artifactId&gt;javatuples&lt;/artifactId&gt;
    &lt;version&gt;1.2&lt;/version&gt;
&lt;/dependency&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p style="line-height: 1.3em; font-size: 13px; font-family: Verdana, Helvetica, Arial, sans-serif;"><strong>javatuples</strong>&nbsp;offers you tuple classes from one to ten elements:</p> 
 <ul style="font-family: Verdana, Helvetica, Arial, sans-serif; font-size: 13px;"> 
  <li> <tt>Unit&lt;A</tt>&gt; (1 element)</li> 
  <li> <tt>Pair&lt;A,B</tt>&gt; (2 elements)</li> 
  <li> <tt>Triplet&lt;A,B,C</tt>&gt; (3 elements)</li> 
  <li> <tt>Quartet&lt;A,B,C,D</tt>&gt; (4 elements)</li> 
  <li> <tt>Quintet&lt;A,B,C,D,E</tt>&gt; (5 elements)</li> 
  <li> <tt>Sextet&lt;A,B,C,D,E,F</tt>&gt; (6 elements)</li> 
  <li> <tt>Septet&lt;A,B,C,D,E,F,G</tt>&gt; (7 elements)</li> 
  <li> <tt>Octet&lt;A,B,C,D,E,F,G,H</tt>&gt; (8 elements)</li> 
  <li> <tt>Ennead&lt;A,B,C,D,E,F,G,H,I</tt>&gt; (9 elements)</li> 
  <li> <tt>Decade&lt;A,B,C,D,E,F,G,H,I,J</tt>&gt; (10 elements)</li> 
 </ul> 
 <p style="line-height: 1.3em; font-size: 13px; font-family: Verdana, Helvetica, Arial, sans-serif;">Plus a couple of very common 2-element tuple classes equivalent to&nbsp;<tt>Pair</tt>, just for the sake of code semantics:</p> 
 <ul style="font-family: Verdana, Helvetica, Arial, sans-serif; font-size: 13px;"> 
  <li> <tt>KeyValue&lt;A,B</tt>&gt;</li> 
  <li> <tt>LabelValue&lt;A,B</tt>&gt;</li> 
 </ul> 
 <p style="line-height: 1.3em; font-size: 13px; font-family: Verdana, Helvetica, Arial, sans-serif;">All tuple classes are:</p> 
 <ul style="font-family: Verdana, Helvetica, Arial, sans-serif; font-size: 13px;"> 
  <li>Typesafe</li> 
  <li>Immutable</li> 
  <li>Iterable</li> 
  <li>Serializable</li> 
  <li>Comparable (implements&nbsp;<tt>Comparable&lt;Tuple</tt>&gt;)</li> 
  <li>Implementing&nbsp;<tt>equals(...)</tt>&nbsp;and&nbsp;<tt>hashCode()</tt> </li> 
  <li>Implementing&nbsp;<tt>toString()</tt> </li> 
 </ul> 
 <div class="section" style="padding: 4px; font-family: Verdana, Helvetica, Arial, sans-serif; font-size: 13px;">
  &nbsp;
 </div> 
</div>