#Stream类的collect方法
###发表时间：2018-02-28
###分类：java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2411853" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2411853</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>Stream类的collect方法</p> 
 <p>参考：&nbsp;<a href="https://www.jianshu.com/p/ccbb42ad9551">https://www.jianshu.com/p/ccbb42ad9551</a></p> 
 <p>&nbsp;</p> 
 <div> 
  <div> 
   <ul> 
    <li>Collectors.toSet()：转换成set集合。</li> 
    <li>Collectors.toCollection(TreeSet::new)：转换成特定的set集合。<br> TreeSet&lt;Integer&gt; collect2 = Stream.of(1, 3, 4).collect(Collectors.toCollection(TreeSet::new));</li> 
    <li>Collectors.toMap(x -&gt; x, x -&gt; x + 1)：转换成map。<br> Map&lt;Integer, Integer&gt; collect1 = Stream.of(1, 3, 4).collect(Collectors.toMap(x -&gt; x, x -&gt; x + 1));</li> 
    <li>Collectors.minBy(Integer::compare)：求最小值，相对应的当然也有maxBy方法。</li> 
    <li>Collectors.averagingInt(x-&gt;x)：求平均值，同时也有averagingDouble、averagingLong方法。<br> System.out.println(Stream.of(1, 2, 3).collect(Collectors.averagingInt(x-&gt;x)));</li> 
    <li>Collectors.summingInt(x -&gt; x))：求和。</li> 
    <li>Collectors.summarizingDouble(x -&gt; x)：可以获取最大值、最小值、平均值、总和值、总数。<br> DoubleSummaryStatistics summaryStatistics = Stream.of(1, 3, 4).collect(Collectors.summarizingDouble(x -&gt; x));<br> summaryStatistics.getAverage()；//平均值</li> 
    <li>Collectors.groupingBy(x -&gt; x)有三种方法，查看源码可以知道前两个方法最终调用第三个方法，第二个参数默认HashMap::new 第三个参数默认Collectors.toList()，参考SQL的groupBy。<br> Map&lt;Integer, List&lt;Integer&gt;&gt; map = Stream.of(1, 3, 3, 4).collect(Collectors.groupingBy(x -&gt; x));<br> Map&lt;Integer, Long&gt; map = Stream.of(1, 3, 3, 4).collect(Collectors.groupingBy(x -&gt; x, Collectors.counting()));<br> HashMap&lt;Integer, Long&gt; hashMap = Stream.of(1, 3, 3, 4).collect(Collectors.groupingBy(x -&gt; x, HashMap::new, Collectors.counting()));</li> 
    <li>Collectors.partitioningBy(x -&gt; x &gt; 2)，把数据分成两部分，key为ture/false。第一个方法也是调用第二个方法，第二个参数默认为Collectors.toList()。<br> Map&lt;Boolean, List&lt;Integer&gt;&gt; collect5 = Stream.of(1, 3, 4).collect(Collectors.partitioningBy(x -&gt; x &gt; 2));<br> Map&lt;Boolean, Long&gt; collect4 = Stream.of(1, 3, 4).collect(Collectors.partitioningBy(x -&gt; x &gt; 2, Collectors.counting()));</li> 
    <li>Collectors.joining(",")：拼接字符串。<br> System.out.println(Stream.of("a", "b", "c").collect(Collectors.joining(",")));</li> 
    <li>Collectors.reducing(0, x -&gt; x + 1, (x, y) -&gt; x + y))：在求累计值的时候，还可以对参数值进行改变，这里是都+1后再求和。跟reduce方法有点类似，但reduce方法没有第二个参数。<br> System.out.println(Stream.of(1, 3, 4).collect(Collectors.reducing(0, x -&gt; x + 1, (x, y) -&gt; x + y)));</li> 
    <li>Collectors.collectingAndThen(Collectors.joining(","), x -&gt; x + "d")：先执行collect操作后再执行第二个参数的表达式。这里是先拼接字符串，再在最后+ "d"。<br> String str= Stream.of("a", "b", "c").collect(Collectors.collectingAndThen(Collectors.joining(","), x -&gt; x + "d"));</li> 
    <li>Collectors.mapping(...)：跟map操作类似，只是参数有点区别。<br> System.out.println(Stream.of("a", "b", "c").collect(Collectors.mapping(x -&gt; x.toUpperCase(), Collectors.joining(","))));</li> 
   </ul> 
  </div> 作者：抹茶菌
  <br>链接：https://www.jianshu.com/p/ccbb42ad9551
  <br>來源：简书
  <br>著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
 </div> 
 <div>
  &nbsp;
 </div> 
 <div>
  ===================
 </div> 
 <div> 
  <pre name="code" class="java">    public static void test003() throws Exception {
        TreeSet&lt;Integer&gt; collect2 = Stream.of(1, 3, 4, 2).collect(Collectors.toCollection(TreeSet::new));
        System.out.println(collect2);// [1, 2, 3, 4]

        List&lt;KeyValue&lt;Integer, String&gt;&gt; kvs = Lists.newArrayList();
        for (int i = 0; i &lt; 3; i++) {
            kvs.add(new KeyValue&lt;&gt;(i, "hello-" + i));
        }
        Map&lt;Integer, String&gt; map = kvs.stream().collect(Collectors.toMap(KeyValue::getKey, kv -&gt; {
            return kv.getValue() + "&amp;&amp;" + kv.getKey();
        }));
        System.out.println(map);// {0=hello-0&amp;&amp;0, 1=hello-1&amp;&amp;1, 2=hello-2&amp;&amp;2}

        String joinResult = Stream.of("a", "b", "c")
                .collect(Collectors.mapping(x -&gt; x.toUpperCase(), Collectors.joining(",")));
        System.out.println(joinResult);// A,B,C

        Map&lt;Integer, Integer&gt; collect1 = Stream.of(1, 3, 4).collect(Collectors.toMap(x -&gt; x, x -&gt; x + 1));
        System.out.println(collect1);// {1=2, 3=4, 4=5}

        // Collectors.joining(",")：拼接字符串。
        System.out.println(Stream.of("a", "b", "c").collect(Collectors.joining(",")));// a,b,c

        System.out.println(Stream.of("a", "b", "c")
                .collect(Collectors.collectingAndThen(Collectors.joining(","), x -&gt; x + "d")));// a,b,cd

    }</pre> &nbsp;&nbsp;
 </div> 
</div>