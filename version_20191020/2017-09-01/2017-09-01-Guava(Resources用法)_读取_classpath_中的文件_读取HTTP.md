#Guava（Resources用法） 读取 classpath 中的文件、读取HTTP
###发表时间：2017-09-01
###分类：guava,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2391851" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2391851</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>假设 classpath 中有个文件是： hello.txt</p> 
 <p>guava 读取其中的文件内容：</p> 
 <pre name="code" class="java">URL url = Resources.getResource("hello.txt");
List&lt;String&gt; lines = Resources.asCharSource(url, Charsets.UTF_8).readLines();</pre> 
 <p>&nbsp;读取&nbsp;http://www.iteye.com/ 的内容：</p> 
 <pre name="code" class="java">URL url = new URL("http://www.iteye.com/");
List&lt;String&gt; lines = Resources.asCharSource(url, Charsets.UTF_8).readLines();</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>下面是 Guava 中<span style="background-color: #fafafa; font-family: monospace;">Resources的官网 API。</span></p> 
 <p>==============</p> 
 <p>&nbsp;</p> 
 <div class="header" style="clear: both; margin: 0px 20px; padding: 5px 0px 0px; color: #353833; font-family: 'DejaVu Sans', Arial, Helvetica, sans-serif;"> 
  <div class="subTitle" style="margin: 5px 0px 0px;">
   com.google.common.io
  </div> 
  <h2 class="title" style="font-size: 18px; color: #2c4557; margin-top: 10px; margin-bottom: 10px;" title="Class Resources">Class Resources</h2> 
 </div> 
 <div class="contentContainer" style="clear: both; padding: 10px 20px; color: #353833; font-family: 'DejaVu Sans', Arial, Helvetica, sans-serif;"> 
  <ul class="inheritance" style="margin-bottom: 0px;"> 
   <li style="display: inline;"><a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true">java.lang.Object</a></li> 
   <li style="display: inline;"> 
    <ul class="inheritance" style="margin-bottom: 0px; margin-left: 15px; padding-top: 1px; padding-left: 15px;"> 
     <li style="display: inline;">com.google.common.io.Resources</li> 
    </ul> </li> 
  </ul> 
  <div class="description"> 
   <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
    <li class="blockList" style="margin-bottom: 15px; line-height: 1.4;"> 
     <hr> <br><pre><a style="color: #4a6782;" title="annotation in com.google.common.annotations" href="/com/google/common/annotations/Beta.html">@Beta</a>
 <a style="color: #4a6782;" title="annotation in com.google.common.annotations" href="/com/google/common/annotations/GwtIncompatible.html">@GwtIncompatible</a>
public final class <a style="color: #4a6782;" href="/src-html/com/google/common/io/Resources.html#line.47">Resources</a>
extends <a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true">Object</a></pre> 
     <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif;">
      Provides utility methods for working with resources in the classpath. Note that even though these methods use&nbsp;
      <a style="color: #4a6782;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">URL</code></a>&nbsp;parameters, they are usually not appropriate for HTTP or other non-classpath resources. 
      <p>All method parameters must be non-null unless documented otherwise.</p> 
     </div> 
     <dl> 
      <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
       <span class="simpleTagLabel">Since:</span>
      </dt> 
      <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;">
       1.0
      </dd> 
      <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
       <span class="simpleTagLabel">Author:</span>
      </dt> 
      <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;">
       Chris Nokleberg, Ben Yu, Colin Decker
      </dd> 
     </dl> </li> 
   </ul> 
  </div> 
  <div class="summary"> 
   <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
    <li class="blockList" style="margin-bottom: 15px; line-height: 1.4;"> 
     <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
      <li class="blockList" style="margin-bottom: 15px; line-height: 1.4; padding-right: 20px; padding-bottom: 5px; padding-left: 10px; border: 1px solid #ededed; background-color: #f8f8f8;"> <a style="color: #353833;" name="method.summary"></a> <h3 style="font-size: 16px; font-style: italic; margin-top: 15px; margin-bottom: 15px;">Method Summary</h3> 
       <table class="memberSummary" style="width: 1537px; border-left: 1px solid #eeeeee; border-right: 1px solid #eeeeee; border-bottom: 1px solid #eeeeee; padding: 0px; height: 572px;" summary="Method Summary table, listing methods, and an explanation" border="0" cellspacing="0" cellpadding="3"> 
        <caption style="text-align: left; color: #253441; font-weight: bold; clear: none; overflow: hidden; padding: 10px 0px 0px 1px; margin: 0px; white-space: pre;"> 
         <span id="t0" class="activeTableTab" style="white-space: nowrap; padding: 0px 0px 7px; display: inline; float: none; background-color: #f8981d; border: none; height: 16px; background-image: none;"><span style="padding: 5px 12px 7px; display: inline-block; float: left; border: none; height: 16px; margin-right: 3px;">All Methods</span></span>
         <span id="t1" class="tableTab" style="white-space: nowrap; padding: 0px 0px 7px; display: inline; float: none; background-color: #f8981d; border: none; height: 16px; background-image: none;"><span style="padding: 5px 12px 7px; display: inline-block; float: left; background-color: #4d7a97; border: none; height: 16px; margin-right: 3px;"><a style="color: #ffffff;">Static Methods</a></span></span>
         <span id="t4" class="tableTab" style="white-space: nowrap; padding: 0px 0px 7px; display: inline; float: none; background-color: #f8981d; border: none; height: 16px; background-image: none;"><span style="padding: 5px 12px 7px; display: inline-block; float: left; background-color: #4d7a97; border: none; height: 16px; margin-right: 3px;"><a style="color: #ffffff;">Concrete Methods</a></span></span> 
        </caption> 
        <tbody> 
         <tr> 
          <th class="colFirst" style="vertical-align: top; padding: 8px 3px 3px 7px; background: #dee3e9; white-space: nowrap; font-size: 13px; width: 350px;" scope="col">Modifier and Type</th> 
          <th class="colLast" style="vertical-align: top; padding: 8px 3px 3px 7px; background: #dee3e9; font-size: 13px;" scope="col">Method and Description</th> 
         </tr> 
         <tr id="i0" class="altColor" style="background-color: #ffffff;"> 
          <td class="colFirst" style="padding: 8px 0px 3px 10px; vertical-align: top; white-space: nowrap; font-size: 13px; width: 350px;"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">static&nbsp;<a style="color: #4a6782; font-weight: bold;" title="class in com.google.common.io" href="/com/google/common/io/ByteSource.html">ByteSource</a></code></td> 
          <td class="colLast" style="padding: 8px 0px 3px 10px; vertical-align: top; font-size: 13px;"> <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><span class="memberNameLink" style="font-weight: bold;"><a style="color: #4a6782; padding-bottom: 3px;" href="/com/google/common/io/Resources.html#asByteSource-java.net.URL-">asByteSource</a></span>(<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;url)</code> 
           <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-size: 14px; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif; padding-top: 0px;">
            Returns a&nbsp;
            <a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class in com.google.common.io" href="/com/google/common/io/ByteSource.html"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">ByteSource</code></a>&nbsp;that reads from the given URL.
           </div> </td> 
         </tr> 
         <tr id="i1" class="rowColor" style="background-color: #eeeeef;"> 
          <td class="colFirst" style="padding: 8px 0px 3px 10px; vertical-align: top; white-space: nowrap; font-size: 13px; width: 350px;"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">static&nbsp;<a style="color: #4a6782; font-weight: bold;" title="class in com.google.common.io" href="/com/google/common/io/CharSource.html">CharSource</a></code></td> 
          <td class="colLast" style="padding: 8px 0px 3px 10px; vertical-align: top; font-size: 13px;"> <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><span class="memberNameLink" style="font-weight: bold;"><a style="color: #4a6782; padding-bottom: 3px;" href="/com/google/common/io/Resources.html#asCharSource-java.net.URL-java.nio.charset.Charset-">asCharSource</a></span>(<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;url,&nbsp;<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.nio.charset" href="http://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html?is-external=true">Charset</a>&nbsp;charset)</code> 
           <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-size: 14px; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif; padding-top: 0px;">
            Returns a&nbsp;
            <a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class in com.google.common.io" href="/com/google/common/io/CharSource.html"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">CharSource</code></a>&nbsp;that reads from the given URL using the given character set.
           </div> </td> 
         </tr> 
         <tr id="i2" class="altColor" style="background-color: #ffffff;"> 
          <td class="colFirst" style="padding: 8px 0px 3px 10px; vertical-align: top; white-space: nowrap; font-size: 13px; width: 350px;"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">static void</code></td> 
          <td class="colLast" style="padding: 8px 0px 3px 10px; vertical-align: top; font-size: 13px;"> <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><span class="memberNameLink" style="font-weight: bold;"><a style="color: #4a6782; padding-bottom: 3px;" href="/com/google/common/io/Resources.html#copy-java.net.URL-java.io.OutputStream-">copy</a></span>(<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;from,&nbsp;<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.io" href="http://docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html?is-external=true">OutputStream</a>&nbsp;to)</code> 
           <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-size: 14px; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif; padding-top: 0px;">
            Copies all bytes from a URL to an output stream.
           </div> </td> 
         </tr> 
         <tr id="i3" class="rowColor" style="background-color: #eeeeef;"> 
          <td class="colFirst" style="padding: 8px 0px 3px 10px; vertical-align: top; white-space: nowrap; font-size: 13px; width: 350px;"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">static&nbsp;<a style="color: #4a6782; font-weight: bold;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a></code></td> 
          <td class="colLast" style="padding: 8px 0px 3px 10px; vertical-align: top; font-size: 13px;"> <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><span class="memberNameLink" style="font-weight: bold;"><a style="color: #4a6782; padding-bottom: 3px;" href="/com/google/common/io/Resources.html#getResource-java.lang.Class-java.lang.String-">getResource</a></span>(<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Class.html?is-external=true">Class</a>&lt;?&gt;&nbsp;contextClass,&nbsp;<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/String.html?is-external=true">String</a>&nbsp;resourceName)</code> 
           <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-size: 14px; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif; padding-top: 0px;">
            Given a&nbsp;
            <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">resourceName</code>&nbsp;that is relative to&nbsp;
            <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">contextClass</code>, returns a&nbsp;
            <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">URL</code>&nbsp;pointing to the named resource.
           </div> </td> 
         </tr> 
         <tr id="i4" class="altColor" style="background-color: #ffffff;"> 
          <td class="colFirst" style="padding: 8px 0px 3px 10px; vertical-align: top; white-space: nowrap; font-size: 13px; width: 350px;"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">static&nbsp;<a style="color: #4a6782; font-weight: bold;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a></code></td> 
          <td class="colLast" style="padding: 8px 0px 3px 10px; vertical-align: top; font-size: 13px;"> <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><span class="memberNameLink" style="font-weight: bold;"><a style="color: #4a6782; padding-bottom: 3px;" href="/com/google/common/io/Resources.html#getResource-java.lang.String-">getResource</a></span>(<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/String.html?is-external=true">String</a>&nbsp;resourceName)</code> 
           <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-size: 14px; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif; padding-top: 0px;">
            Returns a&nbsp;
            <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">URL</code>&nbsp;pointing to&nbsp;
            <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">resourceName</code>&nbsp;if the resource is found using the&nbsp;
            <a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html?is-external=true#getContextClassLoader--">context class loader</a>.
           </div> </td> 
         </tr> 
         <tr id="i5" class="rowColor" style="background-color: #eeeeef;"> 
          <td class="colFirst" style="padding: 8px 0px 3px 10px; vertical-align: top; white-space: nowrap; font-size: 13px; width: 350px;"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">static&nbsp;<a style="color: #4a6782; font-weight: bold;" title="class or interface in java.util" href="http://docs.oracle.com/javase/8/docs/api/java/util/List.html?is-external=true">List</a>&lt;<a style="color: #4a6782; font-weight: bold;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/String.html?is-external=true">String</a>&gt;</code></td> 
          <td class="colLast" style="padding: 8px 0px 3px 10px; vertical-align: top; font-size: 13px;"> <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><span class="memberNameLink" style="font-weight: bold;"><a style="color: #4a6782; padding-bottom: 3px;" href="/com/google/common/io/Resources.html#readLines-java.net.URL-java.nio.charset.Charset-">readLines</a></span>(<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;url,&nbsp;<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.nio.charset" href="http://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html?is-external=true">Charset</a>&nbsp;charset)</code> 
           <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-size: 14px; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif; padding-top: 0px;">
            Reads all of the lines from a URL.
           </div> </td> 
         </tr> 
         <tr id="i6" class="altColor" style="background-color: #ffffff;"> 
          <td class="colFirst" style="padding: 8px 0px 3px 10px; vertical-align: top; white-space: nowrap; font-size: 13px; width: 350px;"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">static &lt;T&gt;&nbsp;T</code></td> 
          <td class="colLast" style="padding: 8px 0px 3px 10px; vertical-align: top; font-size: 13px;"> <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><span class="memberNameLink" style="font-weight: bold;"><a style="color: #4a6782; padding-bottom: 3px;" href="/com/google/common/io/Resources.html#readLines-java.net.URL-java.nio.charset.Charset-com.google.common.io.LineProcessor-">readLines</a></span>(<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;url,&nbsp;<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.nio.charset" href="http://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html?is-external=true">Charset</a>&nbsp;charset,&nbsp;<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="interface in com.google.common.io" href="/com/google/common/io/LineProcessor.html">LineProcessor</a>&lt;T&gt;&nbsp;callback)</code> 
           <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-size: 14px; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif; padding-top: 0px;">
            Streams lines from a URL, stopping when our callback returns false, or we have read all of the lines.
           </div> </td> 
         </tr> 
         <tr id="i7" class="rowColor" style="background-color: #eeeeef;"> 
          <td class="colFirst" style="padding: 8px 0px 3px 10px; vertical-align: top; white-space: nowrap; font-size: 13px; width: 350px;"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">static byte[]</code></td> 
          <td class="colLast" style="padding: 8px 0px 3px 10px; vertical-align: top; font-size: 13px;"> <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><span class="memberNameLink" style="font-weight: bold;"><a style="color: #4a6782; padding-bottom: 3px;" href="/com/google/common/io/Resources.html#toByteArray-java.net.URL-">toByteArray</a></span>(<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;url)</code> 
           <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-size: 14px; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif; padding-top: 0px;">
            Reads all bytes from a URL into a byte array.
           </div> </td> 
         </tr> 
         <tr id="i8" class="altColor" style="background-color: #ffffff;"> 
          <td class="colFirst" style="padding: 8px 0px 3px 10px; vertical-align: top; white-space: nowrap; font-size: 13px; width: 350px;"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">static&nbsp;<a style="color: #4a6782; font-weight: bold;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/String.html?is-external=true">String</a></code></td> 
          <td class="colLast" style="padding: 8px 0px 3px 10px; vertical-align: top; font-size: 13px;"> <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><span class="memberNameLink" style="font-weight: bold;"><a style="color: #4a6782; padding-bottom: 3px;" href="/com/google/common/io/Resources.html#toString-java.net.URL-java.nio.charset.Charset-">toString</a></span>(<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;url,&nbsp;<a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.nio.charset" href="http://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html?is-external=true">Charset</a>&nbsp;charset)</code> 
           <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-size: 14px; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif; padding-top: 0px;">
            Reads all characters from a URL into a&nbsp;
            <a style="color: #4a6782; padding-bottom: 3px; font-weight: bold;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/String.html?is-external=true"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">String</code></a>, using the given character set.
           </div> </td> 
         </tr> 
        </tbody> 
       </table> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 15px; line-height: 1.4; padding-bottom: 5px; padding-left: 8px; border: none; background-color: #ffffff;"> <a style="color: #353833;" name="methods.inherited.from.class.java.lang.Object"></a> <h3>Methods inherited from class&nbsp;java.lang.<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true">Object</a> </h3> <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true#clone--">clone</a>,&nbsp;<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true#equals-java.lang.Object-">equals</a>,&nbsp;<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true#finalize--">finalize</a>,&nbsp;<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true#getClass--">getClass</a>,&nbsp;<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true#hashCode--">hashCode</a>,&nbsp;<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true#notify--">notify</a>,&nbsp;<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true#notifyAll--">notifyAll</a>,&nbsp;<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true#toString--">toString</a>,&nbsp;<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true#wait--">wait</a>,&nbsp;<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true#wait-long-">wait</a>,&nbsp;<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html?is-external=true#wait-long-int-">wait</a></code> </li> 
       </ul> </li> 
     </ul> </li> 
   </ul> 
  </div> 
  <div class="details"> 
   <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
    <li class="blockList" style="margin-bottom: 15px; line-height: 1.4;"> 
     <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
      <li class="blockList" style="margin-bottom: 15px; line-height: 1.4; padding-right: 20px; padding-bottom: 5px; padding-left: 10px; border: 1px solid #ededed; background-color: #f8f8f8;"> <a style="color: #353833;" name="method.detail"></a> <h3 style="font-size: 16px; font-style: italic; margin-top: 15px; margin-bottom: 15px;">Method Detail</h3> <a style="color: #353833;" name="asByteSource-java.net.URL-"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 15px; line-height: 1.4; padding-bottom: 5px; padding-left: 8px; border: none; background-color: #ffffff;"> <h4>asByteSource</h4> <pre>public static&nbsp;<a style="color: #4a6782;" title="class in com.google.common.io" href="/com/google/common/io/ByteSource.html">ByteSource</a>&nbsp;<a style="color: #4a6782;" href="/src-html/com/google/common/io/Resources.html#line.55">asByteSource</a>(<a style="color: #4a6782;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;url)</pre> 
         <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif;">
          Returns a&nbsp;
          <a style="color: #4a6782;" title="class in com.google.common.io" href="/com/google/common/io/ByteSource.html"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">ByteSource</code></a>&nbsp;that reads from the given URL.
         </div> 
         <dl> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="simpleTagLabel">Since:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;">
           14.0
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="asCharSource-java.net.URL-java.nio.charset.Charset-"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 15px; line-height: 1.4; padding-bottom: 5px; padding-left: 8px; border: none; background-color: #ffffff;"> <h4>asCharSource</h4> <pre>public static&nbsp;<a style="color: #4a6782;" title="class in com.google.common.io" href="/com/google/common/io/CharSource.html">CharSource</a>&nbsp;<a style="color: #4a6782;" href="/src-html/com/google/common/io/Resources.html#line.86">asCharSource</a>(<a style="color: #4a6782;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;url,
                                      <a style="color: #4a6782;" title="class or interface in java.nio.charset" href="http://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html?is-external=true">Charset</a>&nbsp;charset)</pre> 
         <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif;">
          Returns a&nbsp;
          <a style="color: #4a6782;" title="class in com.google.common.io" href="/com/google/common/io/CharSource.html"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">CharSource</code></a>&nbsp;that reads from the given URL using the given character set.
         </div> 
         <dl> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="simpleTagLabel">Since:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;">
           14.0
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="toByteArray-java.net.URL-"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 15px; line-height: 1.4; padding-bottom: 5px; padding-left: 8px; border: none; background-color: #ffffff;"> <h4>toByteArray</h4> <pre>public static&nbsp;byte[]&nbsp;<a style="color: #4a6782;" href="/src-html/com/google/common/io/Resources.html#line.97">toByteArray</a>(<a style="color: #4a6782;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;url)
                          throws <a style="color: #4a6782;" title="class or interface in java.io" href="http://docs.oracle.com/javase/8/docs/api/java/io/IOException.html?is-external=true">IOException</a></pre> 
         <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif;">
          Reads all bytes from a URL into a byte array.
         </div> 
         <dl> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="paramLabel">Parameters:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">url</code>&nbsp;- the URL to read from
          </dd> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="returnLabel">Returns:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;">
           a byte array containing all the bytes from the URL
          </dd> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="throwsLabel">Throws:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><a style="color: #4a6782;" title="class or interface in java.io" href="http://docs.oracle.com/javase/8/docs/api/java/io/IOException.html?is-external=true">IOException</a></code>&nbsp;- if an I/O error occurs
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="toString-java.net.URL-java.nio.charset.Charset-"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 15px; line-height: 1.4; padding-bottom: 5px; padding-left: 8px; border: none; background-color: #ffffff;"> <h4>toString</h4> <pre>public static&nbsp;<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/String.html?is-external=true">String</a>&nbsp;<a style="color: #4a6782;" href="/src-html/com/google/common/io/Resources.html#line.110">toString</a>(<a style="color: #4a6782;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;url,
                              <a style="color: #4a6782;" title="class or interface in java.nio.charset" href="http://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html?is-external=true">Charset</a>&nbsp;charset)
                       throws <a style="color: #4a6782;" title="class or interface in java.io" href="http://docs.oracle.com/javase/8/docs/api/java/io/IOException.html?is-external=true">IOException</a></pre> 
         <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif;">
          Reads all characters from a URL into a&nbsp;
          <a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/String.html?is-external=true"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">String</code></a>, using the given character set.
         </div> 
         <dl> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="paramLabel">Parameters:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">url</code>&nbsp;- the URL to read from
          </dd> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">charset</code>&nbsp;- the charset used to decode the input stream; see&nbsp;
           <a style="color: #4a6782;" title="class in com.google.common.base" href="/com/google/common/base/Charsets.html"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">Charsets</code></a>&nbsp;for helpful predefined constants
          </dd> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="returnLabel">Returns:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;">
           a string containing all the characters from the URL
          </dd> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="throwsLabel">Throws:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><a style="color: #4a6782;" title="class or interface in java.io" href="http://docs.oracle.com/javase/8/docs/api/java/io/IOException.html?is-external=true">IOException</a></code>&nbsp;- if an I/O error occurs.
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="readLines-java.net.URL-java.nio.charset.Charset-com.google.common.io.LineProcessor-"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 15px; line-height: 1.4; padding-bottom: 5px; padding-left: 8px; border: none; background-color: #ffffff;"> <h4>readLines</h4> <pre>public static&nbsp;&lt;T&gt;&nbsp;T&nbsp;<a style="color: #4a6782;" href="/src-html/com/google/common/io/Resources.html#line.126">readLines</a>(<a style="color: #4a6782;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;url,
                              <a style="color: #4a6782;" title="class or interface in java.nio.charset" href="http://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html?is-external=true">Charset</a>&nbsp;charset,
                              <a style="color: #4a6782;" title="interface in com.google.common.io" href="/com/google/common/io/LineProcessor.html">LineProcessor</a>&lt;T&gt;&nbsp;callback)
                       throws <a style="color: #4a6782;" title="class or interface in java.io" href="http://docs.oracle.com/javase/8/docs/api/java/io/IOException.html?is-external=true">IOException</a></pre> 
         <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif;">
          Streams lines from a URL, stopping when our callback returns false, or we have read all of the lines.
         </div> 
         <dl> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="paramLabel">Parameters:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">url</code>&nbsp;- the URL to read from
          </dd> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">charset</code>&nbsp;- the charset used to decode the input stream; see&nbsp;
           <a style="color: #4a6782;" title="class in com.google.common.base" href="/com/google/common/base/Charsets.html"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">Charsets</code></a>&nbsp;for helpful predefined constants
          </dd> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">callback</code>&nbsp;- the LineProcessor to use to handle the lines
          </dd> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="returnLabel">Returns:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;">
           the output of processing the lines
          </dd> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="throwsLabel">Throws:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><a style="color: #4a6782;" title="class or interface in java.io" href="http://docs.oracle.com/javase/8/docs/api/java/io/IOException.html?is-external=true">IOException</a></code>&nbsp;- if an I/O error occurs
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="readLines-java.net.URL-java.nio.charset.Charset-"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 15px; line-height: 1.4; padding-bottom: 5px; padding-left: 8px; border: none; background-color: #ffffff;"> <h4>readLines</h4> <pre>public static&nbsp;<a style="color: #4a6782;" title="class or interface in java.util" href="http://docs.oracle.com/javase/8/docs/api/java/util/List.html?is-external=true">List</a>&lt;<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/String.html?is-external=true">String</a>&gt;&nbsp;<a style="color: #4a6782;" href="/src-html/com/google/common/io/Resources.html#line.144">readLines</a>(<a style="color: #4a6782;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;url,
                                     <a style="color: #4a6782;" title="class or interface in java.nio.charset" href="http://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html?is-external=true">Charset</a>&nbsp;charset)
                              throws <a style="color: #4a6782;" title="class or interface in java.io" href="http://docs.oracle.com/javase/8/docs/api/java/io/IOException.html?is-external=true">IOException</a></pre> 
         <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif;">
          Reads all of the lines from a URL. The lines do not include line-termination characters, but do include other leading and trailing whitespace. 
          <p>This method returns a mutable&nbsp;<code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">List</code>. For an&nbsp;<code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">ImmutableList</code>, use&nbsp;<code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">Resources.asCharSource(url, charset).readLines()</code>.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="paramLabel">Parameters:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">url</code>&nbsp;- the URL to read from
          </dd> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">charset</code>&nbsp;- the charset used to decode the input stream; see&nbsp;
           <a style="color: #4a6782;" title="class in com.google.common.base" href="/com/google/common/base/Charsets.html"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">Charsets</code></a>&nbsp;for helpful predefined constants
          </dd> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="returnLabel">Returns:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;">
           a mutable&nbsp;
           <a style="color: #4a6782;" title="class or interface in java.util" href="http://docs.oracle.com/javase/8/docs/api/java/util/List.html?is-external=true"><code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">List</code></a>&nbsp;containing all the lines
          </dd> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="throwsLabel">Throws:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><a style="color: #4a6782;" title="class or interface in java.io" href="http://docs.oracle.com/javase/8/docs/api/java/io/IOException.html?is-external=true">IOException</a></code>&nbsp;- if an I/O error occurs
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="copy-java.net.URL-java.io.OutputStream-"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 15px; line-height: 1.4; padding-bottom: 5px; padding-left: 8px; border: none; background-color: #ffffff;"> <h4>copy</h4> <pre>public static&nbsp;void&nbsp;<a style="color: #4a6782;" href="/src-html/com/google/common/io/Resources.html#line.173">copy</a>(<a style="color: #4a6782;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;from,
                        <a style="color: #4a6782;" title="class or interface in java.io" href="http://docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html?is-external=true">OutputStream</a>&nbsp;to)
                 throws <a style="color: #4a6782;" title="class or interface in java.io" href="http://docs.oracle.com/javase/8/docs/api/java/io/IOException.html?is-external=true">IOException</a></pre> 
         <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif;">
          Copies all bytes from a URL to an output stream.
         </div> 
         <dl> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="paramLabel">Parameters:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">from</code>&nbsp;- the URL to read from
          </dd> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">to</code>&nbsp;- the output stream
          </dd> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="throwsLabel">Throws:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><a style="color: #4a6782;" title="class or interface in java.io" href="http://docs.oracle.com/javase/8/docs/api/java/io/IOException.html?is-external=true">IOException</a></code>&nbsp;- if an I/O error occurs
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="getResource-java.lang.String-"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 15px; line-height: 1.4; padding-bottom: 5px; padding-left: 8px; border: none; background-color: #ffffff;"> <h4>getResource</h4> <pre>public static&nbsp;<a style="color: #4a6782;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;<a style="color: #4a6782;" href="/src-html/com/google/common/io/Resources.html#line.192">getResource</a>(<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/String.html?is-external=true">String</a>&nbsp;resourceName)</pre> 
         <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif;">
          Returns a&nbsp;
          <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">URL</code>&nbsp;pointing to&nbsp;
          <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">resourceName</code>&nbsp;if the resource is found using the&nbsp;
          <a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html?is-external=true#getContextClassLoader--">context class loader</a>. In simple environments, the context class loader will find resources from the class path. In environments where different threads can have different class loaders, for example app servers, the context class loader will typically have been set to an appropriate loader for the current thread. 
          <p>In the unusual case where the context class loader is null, the class loader that loaded this class (<code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">Resources</code>) will be used instead.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="throwsLabel">Throws:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/IllegalArgumentException.html?is-external=true">IllegalArgumentException</a></code>&nbsp;- if the resource is not found
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="getResource-java.lang.Class-java.lang.String-"></a> 
       <ul class="blockListLast" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 15px; line-height: 1.4; padding-bottom: 5px; padding-left: 8px; border: none; background-color: #ffffff;"> <h4>getResource</h4> <pre>public static&nbsp;<a style="color: #4a6782;" title="class or interface in java.net" href="http://docs.oracle.com/javase/8/docs/api/java/net/URL.html?is-external=true">URL</a>&nbsp;<a style="color: #4a6782;" href="/src-html/com/google/common/io/Resources.html#line.207">getResource</a>(<a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/Class.html?is-external=true">Class</a>&lt;?&gt;&nbsp;contextClass,
                              <a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/String.html?is-external=true">String</a>&nbsp;resourceName)</pre> 
         <div class="block" style="margin: 3px 10px 2px 0px; color: #474747; font-family: 'DejaVu Serif', Georgia, 'Times New Roman', Times, serif;">
          Given a&nbsp;
          <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">resourceName</code>&nbsp;that is relative to&nbsp;
          <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">contextClass</code>, returns a&nbsp;
          <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;">URL</code>&nbsp;pointing to the named resource.
         </div> 
         <dl> 
          <dt style="font-size: 12px; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="throwsLabel">Throws:</span>
          </dt> 
          <dd style="margin-top: 5px; margin-bottom: 10px; margin-left: 0px; font-family: 'DejaVu Sans Mono', monospace;"> 
           <code style="font-family: 'DejaVu Sans Mono', monospace; font-size: 14px; padding-top: 4px; margin-top: 8px; line-height: 1.4em;"><a style="color: #4a6782;" title="class or interface in java.lang" href="http://docs.oracle.com/javase/8/docs/api/java/lang/IllegalArgumentException.html?is-external=true">IllegalArgumentException</a></code>&nbsp;- if the resource is not found
          </dd> 
         </dl> </li> 
       </ul> </li> 
     </ul> </li> 
   </ul> 
  </div> 
 </div> 
</div>