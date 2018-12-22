#guava计算md5、sha1和murmurhash
###发表时间：2017-05-04
###分类：guava,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2372640" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2372640</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>下面是我用来计算MD5和sha1的一段使用guava的代码。</p> 
 <pre name="code" class="java">    public static void test002() throws Exception {
        String msg = StringUtils.repeat('-', 200);
        int testCount = 100000;
        long sha1Time = 0L;
        long md5Time = 0L;
        long murmur3Time = 0L;
        double sha1Average = 0D;
        double md5Average = 0D;
        double murmur3Average = 0D;

        long one = System.currentTimeMillis();
        HashFunction sha1 = Hashing.sha1();
        for (int i = 0; i &lt; testCount; i++) {
            Stopwatch w = Stopwatch.createStarted();
            HashCode hashCode = sha1.hashString(msg + i, Charsets.UTF_8);
            String str = hashCode.toString();
            System.out.println(String.format("sh1's hashCode:%s,length:%s,it consumes:%s", str, str.length(),
                    w));
        }
        long two = System.currentTimeMillis();
        sha1Time = two - one;
        HashFunction md5 = Hashing.md5();
        for (int i = 0; i &lt; testCount; i++) {
            Stopwatch w = Stopwatch.createStarted();
            HashCode md5HashCode = md5.hashString(msg + i, Charsets.UTF_8);
            String md5HashCodeStr = md5HashCode.toString();
            System.out.println(String.format("md5's hashCode:%s,length:%s,it consumes:%s", md5HashCodeStr,
                    md5HashCodeStr.length(), w));
        }
        long three = System.currentTimeMillis();
        md5Time = three - two;

        HashFunction murmur3 = Hashing.murmur3_32();
        Set&lt;String&gt; set = Sets.newHashSet();
        for (int i = 0; i &lt; testCount; i++) {
            Stopwatch w = Stopwatch.createStarted();
            HashCode murmur3HashCode = murmur3.hashString(msg + i, Charsets.UTF_8);
            String murmur3HashCodeStr = murmur3HashCode.toString();
            System.out.println(String.format("murmur3's hashCode:%s,length:%s,it consumes:%s",
                    murmur3HashCodeStr, murmur3HashCodeStr.length(), w));
            set.add(murmur3HashCodeStr);
        }
        long four = System.currentTimeMillis();
        murmur3Time = four - three;

        sha1Average = sha1Time / testCount;
        md5Average = md5Time / testCount;
        murmur3Average = murmur3Time / testCount;

        System.out.println("set size : " + set.size());
        System.out
                .println(String
                        .format("sha1 sum time:%s seconds,average time:%s ms\nmd5 sum time:%s seconds,average time:%s ms\nmurmur3 sum time:%s seconds,average time:%s ms",
                                changeToSecond(sha1Time), sha1Average, changeToSecond(md5Time), md5Average,
                                changeToSecond(murmur3Time), murmur3Average));

    }</pre> 
 <p>&nbsp;</p> 
</div>