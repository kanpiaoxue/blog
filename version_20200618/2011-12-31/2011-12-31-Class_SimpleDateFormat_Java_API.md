#Class SimpleDateFormat Java API
###发表时间：2011-12-31
###分类：java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1331323" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1331323</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <h2> <span>java.text</span>&nbsp;<br>Class SimpleDateFormat</h2> 
 <pre><a title="class in java.lang" href="http://docs.oracle.com/javase/6/docs/api/java/lang/Object.html">java.lang.Object</a>
  </pre> 
 <p><img src="http://docs.oracle.com/javase/6/docs/api/resources/inherit.gif" alt="extended by "></p> 
 <pre><a title="class in java.text" href="http://docs.oracle.com/javase/6/docs/api/java/text/Format.html">java.text.Format</a>
      </pre> 
 <p><img src="http://docs.oracle.com/javase/6/docs/api/resources/inherit.gif" alt="extended by "></p> 
 <pre><a title="class in java.text" href="http://docs.oracle.com/javase/6/docs/api/java/text/DateFormat.html">java.text.DateFormat</a>
          </pre> 
 <p><img src="http://docs.oracle.com/javase/6/docs/api/resources/inherit.gif" alt="extended by "></p> 
 <pre><strong>java.text.SimpleDateFormat</strong>
</pre> 
 <dl> 
  <dt>
   <strong>All Implemented Interfaces:</strong>
  </dt> 
  <dd> 
   <a title="interface in java.io" href="http://docs.oracle.com/javase/6/docs/api/java/io/Serializable.html">Serializable</a>,&nbsp;
   <a title="interface in java.lang" href="http://docs.oracle.com/javase/6/docs/api/java/lang/Cloneable.html">Cloneable</a> 
  </dd> 
 </dl> 
 <hr> 
 <pre>public class <strong>SimpleDateFormat</strong></pre> 
 <dl> 
  <dt></dt> 
  <dt>
   extends 
   <a title="class in java.text" href="http://docs.oracle.com/javase/6/docs/api/java/text/DateFormat.html">DateFormat</a> 
  </dt> 
 </dl> 
 <p><code>SimpleDateFormat</code>&nbsp;is a concrete class for formatting and parsing dates in a locale-sensitive manner. It allows for formatting (date -&gt; text), parsing (text -&gt; date), and normalization.</p> 
 <p><code>SimpleDateFormat</code>&nbsp;allows you to start by choosing any user-defined patterns for date-time formatting. However, you are encouraged to create a date-time formatter with either&nbsp;<code>getTimeInstance</code>,&nbsp;<code>getDateInstance</code>, or&nbsp;<code>getDateTimeInstance</code>&nbsp;in&nbsp;<code>DateFormat</code>. Each of these class methods can return a date/time formatter initialized with a default format pattern. You may modify the format pattern using the&nbsp;<code>applyPattern</code>&nbsp;methods as desired. For more information on using these methods, see&nbsp;<a title="class in java.text" href="http://docs.oracle.com/javase/6/docs/api/java/text/DateFormat.html"><code>DateFormat</code></a>.</p> 
 <h4>Date and Time Patterns</h4> 
 <p>Date and time formats are specified by&nbsp;<em>date and time pattern</em>&nbsp;strings. Within date and time pattern strings, unquoted letters from&nbsp;<code>'A'</code>&nbsp;to&nbsp;<code>'Z'</code>&nbsp;and from&nbsp;<code>'a'</code>&nbsp;to<code>'z'</code>&nbsp;are interpreted as pattern letters representing the components of a date or time string. Text can be quoted using single quotes (<code>'</code>) to avoid interpretation.&nbsp;<code>"''"</code>&nbsp;represents a single quote. All other characters are not interpreted; they're simply copied into the output string during formatting or matched against the input string during parsing.</p> 
 <p>The following pattern letters are defined (all other characters from&nbsp;<code>'A'</code>&nbsp;to&nbsp;<code>'Z'</code>&nbsp;and from&nbsp;<code>'a'</code>&nbsp;to&nbsp;<code>'z'</code>&nbsp;are reserved):</p> 
 <blockquote> 
  <table summary="Chart shows pattern letters, date/time component, presentation, and examples." border="0" cellspacing="3" cellpadding="0">
   <tbody> 
    <tr> 
     <th align="left">Letter</th> 
     <th align="left">Date or Time Component</th> 
     <th align="left">Presentation</th> 
     <th align="left">Examples</th> 
    </tr> 
    <tr> 
     <td><code>G</code></td> 
     <td>Era designator</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#text">Text</a></td> 
     <td><code>AD</code></td> 
    </tr> 
    <tr> 
     <td><code>y</code></td> 
     <td>Year</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#year">Year</a></td> 
     <td> <code>1996</code>;&nbsp;<code>96</code> </td> 
    </tr> 
    <tr> 
     <td><code>M</code></td> 
     <td>Month in year</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#month">Month</a></td> 
     <td> <code>July</code>;&nbsp;<code>Jul</code>;&nbsp;<code>07</code> </td> 
    </tr> 
    <tr> 
     <td><code>w</code></td> 
     <td>Week in year</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">Number</a></td> 
     <td><code>27</code></td> 
    </tr> 
    <tr> 
     <td><code>W</code></td> 
     <td>Week in month</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">Number</a></td> 
     <td><code>2</code></td> 
    </tr> 
    <tr> 
     <td><code>D</code></td> 
     <td>Day in year</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">Number</a></td> 
     <td><code>189</code></td> 
    </tr> 
    <tr> 
     <td><code>d</code></td> 
     <td>Day in month</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">Number</a></td> 
     <td><code>10</code></td> 
    </tr> 
    <tr> 
     <td><code>F</code></td> 
     <td>Day of week in month</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">Number</a></td> 
     <td><code>2</code></td> 
    </tr> 
    <tr> 
     <td><code>E</code></td> 
     <td>Day in week</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#text">Text</a></td> 
     <td> <code>Tuesday</code>;&nbsp;<code>Tue</code> </td> 
    </tr> 
    <tr> 
     <td><code>a</code></td> 
     <td>Am/pm marker</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#text">Text</a></td> 
     <td><code>PM</code></td> 
    </tr> 
    <tr> 
     <td><code>H</code></td> 
     <td>Hour in day (0-23)</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">Number</a></td> 
     <td><code>0</code></td> 
    </tr> 
    <tr> 
     <td><code>k</code></td> 
     <td>Hour in day (1-24)</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">Number</a></td> 
     <td><code>24</code></td> 
    </tr> 
    <tr> 
     <td><code>K</code></td> 
     <td>Hour in am/pm (0-11)</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">Number</a></td> 
     <td><code>0</code></td> 
    </tr> 
    <tr> 
     <td><code>h</code></td> 
     <td>Hour in am/pm (1-12)</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">Number</a></td> 
     <td><code>12</code></td> 
    </tr> 
    <tr> 
     <td><code>m</code></td> 
     <td>Minute in hour</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">Number</a></td> 
     <td><code>30</code></td> 
    </tr> 
    <tr> 
     <td><code>s</code></td> 
     <td>Second in minute</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">Number</a></td> 
     <td><code>55</code></td> 
    </tr> 
    <tr> 
     <td><code>S</code></td> 
     <td>Millisecond</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">Number</a></td> 
     <td><code>978</code></td> 
    </tr> 
    <tr> 
     <td><code>z</code></td> 
     <td>Time zone</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#timezone">General time zone</a></td> 
     <td> <code>Pacific Standard Time</code>;&nbsp;<code>PST</code>;&nbsp;<code>GMT-08:00</code> </td> 
    </tr> 
    <tr> 
     <td><code>Z</code></td> 
     <td>Time zone</td> 
     <td><a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#rfc822timezone">RFC 822 time zone</a></td> 
     <td><code>-0800</code></td> 
    </tr> 
   </tbody>
  </table> 
 </blockquote> 
 <p>Pattern letters are usually repeated, as their number determines the exact presentation:</p> 
 <ul> 
  <li> <strong><a name="text"></a>Text:</strong>&nbsp;For formatting, if the number of pattern letters is 4 or more, the full form is used; otherwise a short or abbreviated form is used if available. For parsing, both forms are accepted, independent of the number of pattern letters.</li> 
  <li> <strong><a name="number"></a>Number:</strong>&nbsp;For formatting, the number of pattern letters is the minimum number of digits, and shorter numbers are zero-padded to this amount. For parsing, the number of pattern letters is ignored unless it's needed to separate two adjacent fields.</li> 
  <li> <strong><a name="year"></a>Year:</strong>&nbsp;If the formatter's&nbsp;<a href="http://docs.oracle.com/javase/6/docs/api/java/text/DateFormat.html#getCalendar()"><code>Calendar</code></a>&nbsp;is the Gregorian calendar, the following rules are applied.<br>
   <ul> 
    <li>For formatting, if the number of pattern letters is 2, the year is truncated to 2 digits; otherwise it is interpreted as a&nbsp;<a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">number</a>.</li> 
    <li>For parsing, if the number of pattern letters is more than 2, the year is interpreted literally, regardless of the number of digits. So using the pattern "MM/dd/yyyy", "01/11/12" parses to Jan 11, 12 A.D.</li> 
    <li>For parsing with the abbreviated year pattern ("y" or "yy"),&nbsp;<code>SimpleDateFormat</code>&nbsp;must interpret the abbreviated year relative to some century. It does this by adjusting dates to be within 80 years before and 20 years after the time the&nbsp;<code>SimpleDateFormat</code>&nbsp;instance is created. For example, using a pattern of "MM/dd/yy" and a&nbsp;<code>SimpleDateFormat</code>&nbsp;instance created on Jan 1, 1997, the string "01/11/12" would be interpreted as Jan 11, 2012 while the string "05/04/64" would be interpreted as May 4, 1964. During parsing, only strings consisting of exactly two digits, as defined by<a href="http://docs.oracle.com/javase/6/docs/api/java/lang/Character.html#isDigit(char)"><code>Character.isDigit(char)</code></a>, will be parsed into the default century. Any other numeric string, such as a one digit string, a three or more digit string, or a two digit string that isn't all digits (for example, "-1"), is interpreted literally. So "01/02/3" or "01/02/003" are parsed, using the same pattern, as Jan 2, 3 AD. Likewise, "01/02/-3" is parsed as Jan 2, 4 BC.</li> 
   </ul> Otherwise, calendar system specific forms are applied. For both formatting and parsing, if the number of pattern letters is 4 or more, a calendar specific&nbsp;<a href="http://docs.oracle.com/javase/6/docs/api/java/util/Calendar.html#LONG">long form</a>&nbsp;is used. Otherwise, a calendar specific&nbsp;<a href="http://docs.oracle.com/javase/6/docs/api/java/util/Calendar.html#SHORT">short or abbreviated form</a>&nbsp;is used.</li> 
  <li> <strong><a name="month"></a>Month:</strong>&nbsp;If the number of pattern letters is 3 or more, the month is interpreted as&nbsp;<a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#text">text</a>; otherwise, it is interpreted as a&nbsp;<a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#number">number</a>.</li> 
  <li> <strong><a name="timezone"></a>General time zone:</strong>&nbsp;Time zones are interpreted as&nbsp;<a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#text">text</a>&nbsp;if they have names. For time zones representing a GMT offset value, the following syntax is used: <pre>     <a name="GMTOffsetTimeZone"></a><em>GMTOffsetTimeZone:</em>
             <code>GMT</code> <em>Sign</em> <em>Hours</em> <code>:</code> <em>Minutes</em>
     <em>Sign:</em> one of
             <code>+ -</code>
     <em>Hours:</em>
             <em>Digit</em>
             <em>Digit</em> <em>Digit</em>
     <em>Minutes:</em>
             <em>Digit</em> <em>Digit</em>
     <em>Digit:</em> one of
             <code>0 1 2 3 4 5 6 7 8 9</code></pre> <em>Hours</em>&nbsp;must be between 0 and 23, and&nbsp;<em>Minutes</em>&nbsp;must be between 00 and 59. The format is locale independent and digits must be taken from the Basic Latin block of the Unicode standard. <p>For parsing,&nbsp;<a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#rfc822timezone">RFC 822 time zones</a>&nbsp;are also accepted.</p> </li> 
  <li> <strong><a name="rfc822timezone"></a>RFC 822 time zone:</strong>&nbsp;For formatting, the RFC 822 4-digit time zone format is used: <pre>     <em>RFC822TimeZone:</em>
             <em>Sign</em> <em>TwoDigitHours</em> <em>Minutes</em>
     <em>TwoDigitHours:</em>
             <em>Digit Digit</em></pre> <em>TwoDigitHours</em>&nbsp;must be between 00 and 23. Other definitions are as for&nbsp;<a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#timezone">general time zones</a>. <p>For parsing,&nbsp;<a href="http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html#timezone">general time zones</a>&nbsp;are also accepted.</p> </li> 
 </ul> 
 <p><code>SimpleDateFormat</code>&nbsp;also supports&nbsp;<em>localized date and time pattern</em>&nbsp;strings. In these strings, the pattern letters described above may be replaced with other, locale dependent, pattern letters.&nbsp;<code>SimpleDateFormat</code>&nbsp;does not deal with the localization of text other than the pattern letters; that's up to the client of the class.</p> 
 <p>&nbsp;</p> 
 <h4>Examples</h4> 
 <p>The following examples show how date and time patterns are interpreted in the U.S. locale. The given date and time are 2001-07-04 12:08:56 local time in the U.S. Pacific Time time zone.</p> 
 <blockquote> 
  <table summary="Examples of date and time patterns interpreted in the U.S. locale" border="0" cellspacing="3" cellpadding="0">
   <tbody> 
    <tr> 
     <th align="left">Date and Time Pattern</th> 
     <th align="left">Result</th> 
    </tr> 
    <tr> 
     <td><code>"yyyy.MM.dd G 'at' HH:mm:ss z"</code></td> 
     <td><code>2001.07.04 AD at 12:08:56 PDT</code></td> 
    </tr> 
    <tr> 
     <td><code>"EEE, MMM d, ''yy"</code></td> 
     <td><code>Wed, Jul 4, '01</code></td> 
    </tr> 
    <tr> 
     <td><code>"h:mm a"</code></td> 
     <td><code>12:08 PM</code></td> 
    </tr> 
    <tr> 
     <td><code>"hh 'o''clock' a, zzzz"</code></td> 
     <td><code>12 o'clock PM, Pacific Daylight Time</code></td> 
    </tr> 
    <tr> 
     <td><code>"K:mm a, z"</code></td> 
     <td><code>0:08 PM, PDT</code></td> 
    </tr> 
    <tr> 
     <td><code>"yyyyy.MMMMM.dd GGG hh:mm aaa"</code></td> 
     <td><code>02001.July.04 AD 12:08 PM</code></td> 
    </tr> 
    <tr> 
     <td><code>"EEE, d MMM yyyy HH:mm:ss Z"</code></td> 
     <td><code>Wed, 4 Jul 2001 12:08:56 -0700</code></td> 
    </tr> 
    <tr> 
     <td><code>"yyMMddHHmmssZ"</code></td> 
     <td><code>010704120856-0700</code></td> 
    </tr> 
    <tr> 
     <td><code>"yyyy-MM-dd'T'HH:mm:ss.SSSZ"</code></td> 
     <td><code>2001-07-04T12:08:56.235-0700</code></td> 
    </tr> 
   </tbody>
  </table> 
 </blockquote> 
 <h4> <a name="synchronization"></a>Synchronization</h4> 
 <p>Date formats are not synchronized. It is recommended to create separate format instances for each thread. If multiple threads access a format concurrently, it must be synchronized externally.</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">字母  日期或时间元素  表示  示例
G  Era 标志符  Text  AD
y  年  Year  1996; 96
M  年中的月份  Month  July; Jul; 07
w  年中的周数  Number  27
W  月份中的周数  Number  2
D  年中的天数  Number  189
d  月份中的天数  Number  10
F  月份中的星期  Number  2
E  星期中的天数  Text  Tuesday; Tue
a  Am/pm 标记  Text  PM
H  一天中的小时数（0-23）  Number  0
k  一天中的小时数（1-24）  Number  24
K  am/pm 中的小时数（0-11）  Number  0
h  am/pm 中的小时数（1-12）  Number  12
m  小时中的分钟数  Number  30
s  分钟中的秒数  Number  55
S  毫秒数  Number  978
z  时区  General time zone  Pacific Standard Time; PST; GMT-08:00
Z  时区  RFC 822 time zone  -0800</pre> 
 <p>&nbsp;</p> 
</div>