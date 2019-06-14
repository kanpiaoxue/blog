#log4j PatternLayout的格式
###发表时间：2015-08-04
###分类：log4j,log
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2232624" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2232624</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>引自官网：&nbsp;<a href="https://logging.apache.org/log4j/1.2/apidocs/org/apache/log4j/PatternLayout.html">https://logging.apache.org/log4j/1.2/apidocs/org/apache/log4j/PatternLayout.html</a></p> 
 <br>
 <h2>org.apache.log4j <br> Class PatternLayout</h2> 
 <pre><strong>org.apache.log4j.PatternLayout</strong>
</pre> 
 <dl>
  <dt>
   <strong>&nbsp;</strong>
  </dt>
 </dl> 
 <hr> 
 <pre>public class <strong>PatternLayout</strong>extends <a title="class in org.apache.log4j" href="/org/apache/log4j/Layout.html">Layout</a></pre> 
 <p>A flexible layout configurable with pattern string. This code is known to have synchronization and other issues which are not present in org.apache.log4j.EnhancedPatternLayout. EnhancedPatternLayout should be used in preference to PatternLayout. EnhancedPatternLayout is distributed in the log4j extras companion.</p> 
 <p>The goal of this class is to <a href="/org/apache/log4j/PatternLayout.html#format(org.apache.log4j.spi.LoggingEvent)"><code>format</code></a> a <a title="class in org.apache.log4j.spi" href="/org/apache/log4j/spi/LoggingEvent.html"><code>LoggingEvent</code></a> and return the results as a String. The results depend on the <em>conversion pattern</em>.</p> 
 <p>The conversion pattern is closely related to the conversion pattern of the printf function in C. A conversion pattern is composed of literal text and format control expressions called <em>conversion specifiers</em>.</p> 
 <p><em>You are free to insert any literal text within the conversion pattern.</em></p> 
 <p>Each conversion specifier starts with a percent sign (%) and is followed by optional <em>format modifiers</em> and a <em>conversion character</em>. The conversion character specifies the type of data, e.g. category, priority, date, thread name. The format modifiers control such things as field width, padding, left and right justification. The following is a simple example.</p> 
 <p>Let the conversion pattern be <strong>"%-5p [%t]: %m%n"</strong> and assume that the log4j environment was set to use a PatternLayout. Then the statements</p> 
 <pre>   Category root = Category.getRoot();
   root.debug("Message 1");
   root.warn("Message 2");
   </pre> 
 <p>would yield the output</p> 
 <pre>   DEBUG [main]: Message 1
   WARN  [main]: Message 2
   </pre> 
 <p>Note that there is no explicit separator between text and conversion specifiers. The pattern parser knows when it has reached the end of a conversion specifier when it reads a conversion character. In the example above the conversion specifier <strong>%-5p</strong> means the priority of the logging event should be left justified to a width of five characters. The recognized conversion characters are</p> 
 <p>&nbsp;</p> 
 <table border="1" cellpadding="8">
  <tbody> 
   <tr> 
    <th>Conversion Character</th> 
    <th>Effect</th> 
   </tr> 
   <tr> 
    <td align="center"><strong>c</strong></td> 
    <td>Used to output the category of the logging event. The category conversion specifier can be optionally followed by <em>precision specifier</em>, that is a decimal constant in brackets. <p>If a precision specifier is given, then only the corresponding number of right most components of the category name will be printed. By default the category name is printed in full.</p> <p>For example, for the category name "a.b.c" the pattern <strong>%c{2}</strong> will output "b.c".</p> </td> 
   </tr> 
   <tr> 
    <td align="center"><strong>C</strong></td> 
    <td>Used to output the fully qualified class name of the caller issuing the logging request. This conversion specifier can be optionally followed by <em>precision specifier</em>, that is a decimal constant in brackets. <p>If a precision specifier is given, then only the corresponding number of right most components of the class name will be printed. By default the class name is output in fully qualified form.</p> <p>For example, for the class name "org.apache.xyz.SomeClass", the pattern <strong>%C{1}</strong> will output "SomeClass".</p> <p><strong>WARNING</strong> Generating the caller class information is slow. Thus, use should be avoided unless execution speed is not an issue.</p> </td> 
   </tr> 
   <tr> 
    <td align="center"><strong>d</strong></td> 
    <td>Used to output the date of the logging event. The date conversion specifier may be followed by a <em>date format specifier</em> enclosed between braces. For example, <strong>%d{HH:mm:ss,SSS}</strong> or <strong>%d{dd&nbsp;MMM&nbsp;yyyy&nbsp;HH:mm:ss,SSS}</strong>. If no date format specifier is given then ISO8601 format is assumed. <p>The date format specifier admits the same syntax as the time pattern string of the <a title="class or interface in java.text" href="http://java.sun.com/j2se/1.4.2/docs/api/java/text/SimpleDateFormat.html?is-external=true"><code>SimpleDateFormat</code></a>. Although part of the standard JDK, the performance of <code>SimpleDateFormat</code> is quite poor.</p> <p>For better results it is recommended to use the log4j date formatters. These can be specified using one of the strings "ABSOLUTE", "DATE" and "ISO8601" for specifying <a title="class in org.apache.log4j.helpers" href="/org/apache/log4j/helpers/AbsoluteTimeDateFormat.html"><code>AbsoluteTimeDateFormat</code></a>, <a title="class in org.apache.log4j.helpers" href="/org/apache/log4j/helpers/DateTimeDateFormat.html"><code>DateTimeDateFormat</code></a> and respectively <a title="class in org.apache.log4j.helpers" href="/org/apache/log4j/helpers/ISO8601DateFormat.html"><code>ISO8601DateFormat</code></a>. For example, <strong>%d{ISO8601}</strong> or <strong>%d{ABSOLUTE}</strong>.</p> <p>These dedicated date formatters perform significantly better than <a title="class or interface in java.text" href="http://java.sun.com/j2se/1.4.2/docs/api/java/text/SimpleDateFormat.html?is-external=true"><code>SimpleDateFormat</code></a>.</p> </td> 
   </tr> 
   <tr> 
    <td align="center"><strong>F</strong></td> 
    <td>Used to output the file name where the logging request was issued. <p><strong>WARNING</strong> Generating caller location information is extremely slow and should be avoided unless execution speed is not an issue.</p> </td> 
   </tr> 
   <tr> 
    <td align="center"><strong>l</strong></td> 
    <td>Used to output location information of the caller which generated the logging event. <p>The location information depends on the JVM implementation but usually consists of the fully qualified name of the calling method followed by the callers source the file name and line number between parentheses.</p> <p>The location information can be very useful. However, its generation is <em>extremely</em> slow and should be avoided unless execution speed is not an issue.</p> </td> 
   </tr> 
   <tr> 
    <td align="center"><strong>L</strong></td> 
    <td>Used to output the line number from where the logging request was issued. <p><strong>WARNING</strong> Generating caller location information is extremely slow and should be avoided unless execution speed is not an issue.</p> </td> 
   </tr> 
   <tr> 
    <td align="center"><strong>m</strong></td> 
    <td>Used to output the application supplied message associated with the logging event.</td> 
   </tr> 
   <tr> 
    <td align="center"><strong>M</strong></td> 
    <td>Used to output the method name where the logging request was issued. <p><strong>WARNING</strong> Generating caller location information is extremely slow and should be avoided unless execution speed is not an issue.</p> </td> 
   </tr> 
   <tr> 
    <td align="center"><strong>n</strong></td> 
    <td>Outputs the platform dependent line separator character or characters. <p>This conversion character offers practically the same performance as using non-portable line separator strings such as "\n", or "\r\n". Thus, it is the preferred way of specifying a line separator.</p> </td> 
   </tr> 
   <tr> 
    <td align="center"><strong>p</strong></td> 
    <td>Used to output the priority of the logging event.</td> 
   </tr> 
   <tr> 
    <td align="center"><strong>r</strong></td> 
    <td>Used to output the number of milliseconds elapsed from the construction of the layout until the creation of the logging event.</td> 
   </tr> 
   <tr> 
    <td align="center"><strong>t</strong></td> 
    <td>Used to output the name of the thread that generated the logging event.</td> 
   </tr> 
   <tr> 
    <td align="center"><strong>x</strong></td> 
    <td>Used to output the NDC (nested diagnostic context) associated with the thread that generated the logging event.</td> 
   </tr> 
   <tr> 
    <td align="center"><strong>X</strong></td> 
    <td> <p>Used to output the MDC (mapped diagnostic context) associated with the thread that generated the logging event. The <strong>X</strong> conversion character <em>must</em> be followed by the key for the map placed between braces, as in <strong>%X{clientNumber}</strong> where <code>clientNumber</code> is the key. The value in the MDC corresponding to the key will be output.</p> <p>See <a title="class in org.apache.log4j" href="/org/apache/log4j/MDC.html"><code>MDC</code></a> class for more details.</p> </td> 
   </tr> 
   <tr> 
    <td align="center"><strong>%</strong></td> 
    <td>The sequence %% outputs a single percent sign.</td> 
   </tr> 
  </tbody>
 </table> 
 <p>By default the relevant information is output as is. However, with the aid of format modifiers it is possible to change the minimum field width, the maximum field width and justification.</p> 
 <p>The optional format modifier is placed between the percent sign and the conversion character.</p> 
 <p>The first optional format modifier is the <em>left justification flag</em> which is just the minus (-) character. Then comes the optional <em>minimum field width</em> modifier. This is a decimal constant that represents the minimum number of characters to output. If the data item requires fewer characters, it is padded on either the left or the right until the minimum width is reached. The default is to pad on the left (right justify) but you can specify right padding with the left justification flag. The padding character is space. If the data item is larger than the minimum field width, the field is expanded to accommodate the data. The value is never truncated.</p> 
 <p>This behavior can be changed using the <em>maximum field width</em> modifier which is designated by a period followed by a decimal constant. If the data item is longer than the maximum field, then the extra characters are removed from the <em>beginning</em> of the data item and not from the end. For example, it the maximum field width is eight and the data item is ten characters long, then the first two characters of the data item are dropped. This behavior deviates from the printf function in C where truncation is done from the end.</p> 
 <p>Below are various format modifier examples for the category conversion specifier.</p> 
 <p>&nbsp;</p> 
 <table border="1" cellpadding="8">
  <tbody> 
   <tr> 
    <th>Format modifier</th> 
    <th>left justify</th> 
    <th>minimum width</th> 
    <th>maximum width</th> 
    <th>comment</th> 
   </tr> 
   <tr> 
    <td align="center">%20c</td> 
    <td align="center">false</td> 
    <td align="center">20</td> 
    <td align="center">none</td> 
    <td>Left pad with spaces if the category name is less than 20 characters long.</td> 
   </tr> 
   <tr> 
    <td align="center">%-20c</td> 
    <td align="center">true</td> 
    <td align="center">20</td> 
    <td align="center">none</td> 
    <td>Right pad with spaces if the category name is less than 20 characters long.</td> 
   </tr> 
   <tr> 
    <td align="center">%.30c</td> 
    <td align="center">NA</td> 
    <td align="center">none</td> 
    <td align="center">30</td> 
    <td>Truncate from the beginning if the category name is longer than 30 characters.</td> 
   </tr> 
   <tr> 
    <td align="center">%20.30c</td> 
    <td align="center">false</td> 
    <td align="center">20</td> 
    <td align="center">30</td> 
    <td>Left pad with spaces if the category name is shorter than 20 characters. However, if category name is longer than 30 characters, then truncate from the beginning.</td> 
   </tr> 
   <tr> 
    <td align="center">%-20.30c</td> 
    <td align="center">true</td> 
    <td align="center">20</td> 
    <td align="center">30</td> 
    <td>Right pad with spaces if the category name is shorter than 20 characters. However, if category name is longer than 30 characters, then truncate from the beginning.</td> 
   </tr> 
  </tbody>
 </table> 
 <p>Below are some examples of conversion patterns.</p> 
 <p>&nbsp;</p> 
 <dl>
  <dt>
   <strong>%r [%t] %-5p %c %x - %m%n</strong>
  </dt>
 </dl> 
 <p>&nbsp;</p> 
 <dl> 
  <dt></dt> 
  <dd>
   This is essentially the TTCC layout. 
   <p>&nbsp;</p> 
  </dd> 
  <dt>
   <strong>%-6r [%15.15t] %-5p %30.30c %x - %m%n</strong>
  </dt> 
 </dl> 
 <p>&nbsp;</p> 
 <dl> 
  <dt></dt> 
  <dd>
   Similar to the TTCC layout except that the relative time is right padded if less than 6 digits, thread name is right padded if less than 15 characters and truncated if longer and the category name is left padded if shorter than 30 characters and truncated if longer.
  </dd> 
 </dl> 
 <p>The above text is largely inspired from Peter A. Darnell and Philip E. Margolis' highly recommended book "C -- a Software Engineering Approach", ISBN 0-387-97389-3.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <dl> 
  <dt>
   <strong>Since:</strong>
  </dt> 
  <dd>
   0.8.2
  </dd> 
  <dt>
   <strong>Author:</strong>
  </dt> 
  <dd> 
   <a href="mailto:cakalijp@Maritz.com">James P. Cakalic</a>, Ceki Gülcü
  </dd> 
 </dl> 
</div>