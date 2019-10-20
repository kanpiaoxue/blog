#JDK中Java String format
###发表时间：2014-09-03
###分类：jdk,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2113068" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2113068</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <div class="header" style="clear: both; margin: 0px 20px; padding: 5px 0px 0px;"> 
  <div class="subTitle" style="margin: 5px 0px 0px;">
   java.util
  </div> 
  <h2 class="title" style="color: #2c4557; margin-top: 10px; margin-bottom: 10px;" title="Class Formatter">Class Formatter</h2> 
 </div> 
 <div class="contentContainer" style="clear: both; padding: 10px 20px;"> 
  <ul class="inheritance" style="margin-bottom: 0px;"> 
   <li style="display: inline;"><a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html">java.lang.Object</a></li> 
   <li style="display: inline;"> 
    <ul class="inheritance" style="margin-bottom: 0px; margin-left: 15px; padding-top: 1px; padding-left: 15px;"> 
     <li style="display: inline;">java.util.Formatter</li> 
    </ul> </li> 
  </ul> 
  <div class="description"> 
   <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
    <li class="blockList" style="margin-bottom: 25px;"> 
     <dl> 
      <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
       All Implemented Interfaces:
      </dt> 
      <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
       <a style="color: #4c6b87;" title="interface in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/Closeable.html">Closeable</a>,&nbsp;
       <a style="color: #4c6b87;" title="interface in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/Flushable.html">Flushable</a>,&nbsp;
       <a style="color: #4c6b87;" title="interface in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/AutoCloseable.html">AutoCloseable</a> 
      </dd> 
     </dl> 
     <hr> <br><pre>public final class <span class="strong" style="font-weight: bold;">Formatter</span>
extends <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html">Object</a>
implements <a style="color: #4c6b87;" title="interface in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/Closeable.html">Closeable</a>, <a style="color: #4c6b87;" title="interface in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/Flushable.html">Flushable</a></pre> 
     <div class="block" style="margin: 3px 0px 0px;">
      An interpreter for printf-style format strings. This class provides support for layout justification and alignment, common formats for numeric, string, and date/time data, and locale-specific output. Common Java types such as&nbsp;
      <code style="font-size: 1.2em;">byte</code>,&nbsp;
      <a style="color: #4c6b87;" title="class in java.math" href="http://docs.oracle.com/javase/7/docs/api/java/math/BigDecimal.html"><code style="font-size: 1.2em;">BigDecimal</code></a>, and&nbsp;
      <a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Calendar.html"><code style="font-size: 1.2em;">Calendar</code></a>&nbsp;are supported. Limited formatting customization for arbitrary user types is provided through the&nbsp;
      <a style="color: #4c6b87;" title="interface in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formattable.html"><code style="font-size: 1.2em;">Formattable</code></a>&nbsp;interface. 
      <p><span style="color: #ff0000;">Formatters are not necessarily safe for multithreaded access.</span> Thread safety is optional and is the responsibility of users of methods in this class.</p> 
      <p>Formatted printing for the Java language is heavily inspired by C's&nbsp;<code style="font-size: 1.2em;">printf</code>. Although the format strings are similar to C, some customizations have been made to accommodate the Java language and exploit some of its features. Also, Java formatting is more strict than C's; for example, if a conversion is incompatible with a flag, an exception will be thrown. In C inapplicable flags are silently ignored. The format strings are thus intended to be recognizable to C programmers but not necessarily completely compatible with those in C.</p> 
      <p>Examples of expected usage:</p> 
      <blockquote> 
       <pre>   StringBuilder sb = new StringBuilder();
   // Send all output to the Appendable object sb
   Formatter formatter = new Formatter(sb, Locale.US);

   // Explicit argument indices may be used to re-order output.
   formatter.format("%4$2s %3$2s %2$2s %1$2s", "a", "b", "c", "d")
   // -&gt; " d  c  b  a"

   // Optional locale as the first argument can be used to get
   // locale-specific formatting of numbers.  The precision and width can be
   // given to round and align the value.
   formatter.format(Locale.FRANCE, "e = %+10.4f", Math.E);
   // -&gt; "e =    +2,7183"

   // The '(' numeric flag may be used to format negative numbers with
   // parentheses rather than a minus sign.  Group separators are
   // automatically inserted.
   formatter.format("Amount gained or lost since last statement: $ %(,.2f",
                    balanceDelta);
   // -&gt; "Amount gained or lost since last statement: $ (6,217.58)"
 </pre> 
      </blockquote> 
      <p>Convenience methods for common formatting requests exist as illustrated by the following invocations:</p> 
      <blockquote> 
       <pre>   // Writes a formatted string to System.out.
   System.out.format("Local time: %tT", Calendar.getInstance());
   // -&gt; "Local time: 13:34:18"

   // Writes formatted output to System.err.
   System.err.printf("Unable to open file '%1$s': %2$s",
                     fileName, exception.getMessage());
   // -&gt; "Unable to open file 'food': No such file or directory"
 </pre> 
      </blockquote> 
      <p>Like C's&nbsp;<code style="font-size: 1.2em;">sprintf(3)</code>, Strings may be formatted using the static method&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#format(java.lang.String,%20java.lang.Object...)"><code style="font-size: 1.2em;">String.format</code></a>:</p> 
      <blockquote> 
       <pre>   // Format a string containing a date.
   import java.util.Calendar;
   import java.util.GregorianCalendar;
   import static java.util.Calendar.*;

   Calendar c = new GregorianCalendar(1995, MAY, 23);
   String s = String.format("Duke's Birthday: %1$tm %1$te,%1$tY", c);
   // -&gt; s == "Duke's Birthday: May 23, 1995"
 </pre> 
      </blockquote> 
      <h3 style="font-size: 1.4em;"> <a style="color: #353833;" name="org"></a>Organization</h3> 
      <p>This specification is divided into two sections. The first section,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#summary">Summary</a>, covers the basic formatting concepts. This section is intended for users who want to get started quickly and are familiar with formatted printing in other programming languages. The second section,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#detail">Details</a>, covers the specific implementation details. It is intended for users who want more precise specification of formatting behavior.</p> 
      <h3 style="font-size: 1.4em;"> <a style="color: #353833;" name="summary"></a>Summary</h3> 
      <p>This section is intended to provide a brief overview of formatting concepts. For precise behavioral details, refer to the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#detail">Details</a>&nbsp;section.</p> 
      <h4 style="font-size: 1.3em;"> <a style="color: #353833;" name="syntax"></a>Format String Syntax</h4> 
      <p>Every method which produces formatted output requires a&nbsp;<em>format string</em>&nbsp;and an&nbsp;<em>argument list</em>. The format string is a&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html"><code style="font-size: 1.2em;">String</code></a>&nbsp;which may contain fixed text and one or more embedded&nbsp;<em>format specifiers</em>. Consider the following example:</p> 
      <blockquote> 
       <pre>   Calendar c = ...;
   String s = String.format("Duke's Birthday: %1$tm %1$te,%1$tY", c);
 </pre> 
      </blockquote> This format string is the first argument to the&nbsp;
      <code style="font-size: 1.2em;">format</code>&nbsp;method. It contains three format specifiers "
      <code style="font-size: 1.2em;">%1$tm</code>", "
      <code style="font-size: 1.2em;">%1$te</code>", and "
      <code style="font-size: 1.2em;">%1$tY</code>" which indicate how the arguments should be processed and where they should be inserted in the text. The remaining portions of the format string are fixed text including&nbsp;
      <code style="font-size: 1.2em;">"Dukes Birthday: "</code>&nbsp;and any other spaces or punctuation. The argument list consists of all arguments passed to the method after the format string. In the above example, the argument list is of size one and consists of the&nbsp;
      <a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Calendar.html"><code style="font-size: 1.2em;">Calendar</code></a>&nbsp;object&nbsp;
      <code style="font-size: 1.2em;">c</code>. 
      <ul> 
       <li>The format specifiers for general, character, and numeric types have the following syntax: 
        <blockquote> 
         <pre>   %[argument_index$][flags][width][.precision]conversion
 </pre> 
        </blockquote> <p>The optional&nbsp;<em>argument_index</em>&nbsp;is a decimal integer indicating the position of the argument in the argument list. The first argument is referenced by "<code style="font-size: 1.2em;">1$</code>", the second by "<code style="font-size: 1.2em;">2$</code>", etc.</p> <p>The optional&nbsp;<em>flags</em>&nbsp;is a set of characters that modify the output format. The set of valid flags depends on the conversion.</p> <p>The optional&nbsp;<em>width</em>&nbsp;is a non-negative decimal integer indicating the minimum number of characters to be written to the output.</p> <p>The optional&nbsp;<em>precision</em>&nbsp;is a non-negative decimal integer usually used to restrict the number of characters. The specific behavior depends on the conversion.</p> <p>The required&nbsp;<em>conversion</em>&nbsp;is a character indicating how the argument should be formatted. The set of valid conversions for a given argument depends on the argument's data type.</p> </li> 
       <li>The format specifiers for types which are used to represents dates and times have the following syntax: 
        <blockquote> 
         <pre>   %[argument_index$][flags][width]conversion
 </pre> 
        </blockquote> <p>The optional&nbsp;<em>argument_index</em>,&nbsp;<em>flags</em>&nbsp;and&nbsp;<em>width</em>&nbsp;are defined as above.</p> <p>The required&nbsp;<em>conversion</em>&nbsp;is a two character sequence. The first character is&nbsp;<code style="font-size: 1.2em;">'t'</code>&nbsp;or&nbsp;<code style="font-size: 1.2em;">'T'</code>. The second character indicates the format to be used. These characters are similar to but not completely identical to those defined by GNU&nbsp;<code style="font-size: 1.2em;">date</code>&nbsp;and POSIX&nbsp;<code style="font-size: 1.2em;">strftime(3c)</code>.</p> </li> 
       <li>The format specifiers which do not correspond to arguments have the following syntax: 
        <blockquote> 
         <pre>   %[flags][width]conversion
 </pre> 
        </blockquote> <p>The optional&nbsp;<em>flags</em>&nbsp;and&nbsp;<em>width</em>&nbsp;is defined as above.</p> <p>The required&nbsp;<em>conversion</em>&nbsp;is a character indicating content to be inserted in the output.</p> </li> 
      </ul> 
      <h4 style="font-size: 1.3em;">Conversions</h4> 
      <p>Conversions are divided into the following categories:</p> 
      <ol> 
       <li> <strong>General</strong>&nbsp;- may be applied to any argument type</li> 
       <li> <strong>Character</strong>&nbsp;- may be applied to basic types which represent Unicode characters:&nbsp;<code style="font-size: 1.2em;">char</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Character.html"><code style="font-size: 1.2em;">Character</code></a>,&nbsp;<code style="font-size: 1.2em;">byte</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Byte.html"><code style="font-size: 1.2em;">Byte</code></a>,&nbsp;<code style="font-size: 1.2em;">short</code>, and&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Short.html"><code style="font-size: 1.2em;">Short</code></a>. This conversion may also be applied to the types&nbsp;<code style="font-size: 1.2em;">int</code>&nbsp;and&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Integer.html"><code style="font-size: 1.2em;">Integer</code></a>&nbsp;when&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Character.html#isValidCodePoint(int)"><code style="font-size: 1.2em;">Character.isValidCodePoint(int)</code></a>&nbsp;returns&nbsp;<code style="font-size: 1.2em;">true</code> </li> 
       <li> <strong>Numeric</strong>
        <ol> 
         <li> <strong>Integral</strong>&nbsp;- may be applied to Java integral types:&nbsp;<code style="font-size: 1.2em;">byte</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Byte.html"><code style="font-size: 1.2em;">Byte</code></a>,&nbsp;<code style="font-size: 1.2em;">short</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Short.html"><code style="font-size: 1.2em;">Short</code></a>,&nbsp;<code style="font-size: 1.2em;">int</code>&nbsp;and&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Integer.html"><code style="font-size: 1.2em;">Integer</code></a>,&nbsp;<code style="font-size: 1.2em;">long</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Long.html"><code style="font-size: 1.2em;">Long</code></a>, and&nbsp;<a style="color: #4c6b87;" title="class in java.math" href="http://docs.oracle.com/javase/7/docs/api/java/math/BigInteger.html"><code style="font-size: 1.2em;">BigInteger</code></a> </li> 
         <li> <strong>Floating Point</strong>&nbsp;- may be applied to Java floating-point types:&nbsp;<code style="font-size: 1.2em;">float</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Float.html"><code style="font-size: 1.2em;">Float</code></a>,&nbsp;<code style="font-size: 1.2em;">double</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Double.html"><code style="font-size: 1.2em;">Double</code></a>, and&nbsp;<a style="color: #4c6b87;" title="class in java.math" href="http://docs.oracle.com/javase/7/docs/api/java/math/BigDecimal.html"><code style="font-size: 1.2em;">BigDecimal</code></a> </li> 
        </ol> </li> 
       <li> <strong>Date/Time</strong>&nbsp;- may be applied to Java types which are capable of encoding a date or time:&nbsp;<code style="font-size: 1.2em;">long</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Long.html"><code style="font-size: 1.2em;">Long</code></a>,&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Calendar.html"><code style="font-size: 1.2em;">Calendar</code></a>, and&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Date.html"><code style="font-size: 1.2em;">Date</code></a>.</li> 
       <li> <strong>Percent</strong>&nbsp;- produces a literal&nbsp;<code style="font-size: 1.2em;">'%'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0025'</tt>)</li> 
       <li> <strong>Line Separator</strong>&nbsp;- produces the platform-specific line separator</li> 
      </ol> 
      <p>The following table summarizes the supported conversions. Conversions denoted by an upper-case character (i.e.&nbsp;<code style="font-size: 1.2em;">'B'</code>,&nbsp;<code style="font-size: 1.2em;">'H'</code>,&nbsp;<code style="font-size: 1.2em;">'S'</code>,&nbsp;<code style="font-size: 1.2em;">'C'</code>,&nbsp;<code style="font-size: 1.2em;">'X'</code>,&nbsp;<code style="font-size: 1.2em;">'E'</code>,&nbsp;<code style="font-size: 1.2em;">'G'</code>,&nbsp;<code style="font-size: 1.2em;">'A'</code>, and&nbsp;<code style="font-size: 1.2em;">'T'</code>) are the same as those for the corresponding lower-case conversion characters except that the result is converted to upper case according to the rules of the prevailing&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html"><code style="font-size: 1.2em;">Locale</code></a>. The result is equivalent to the following invocation of&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#toUpperCase()"><code style="font-size: 1.2em;">String.toUpperCase()</code></a></p> 
      <pre>    out.toUpperCase() </pre> 
      <table style="border-bottom-style: none; width: 1863px;" summary="genConv" cellpadding="5">
       <tbody> 
        <tr> 
         <th valign="bottom">Conversion</th> 
         <th valign="bottom">Argument Category</th> 
         <th valign="bottom">Description</th> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"> <code style="font-size: 1.2em;">'b'</code>,&nbsp;<code style="font-size: 1.2em;">'B'</code> </td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">general</td> 
         <td style="padding: 3px 3px 3px 7px;">If the argument&nbsp;<em>arg</em>&nbsp;is&nbsp;<code style="font-size: 1.2em;">null</code>, then the result is "<code style="font-size: 1.2em;">false</code>". If&nbsp;<em>arg</em>&nbsp;is a&nbsp;<code style="font-size: 1.2em;">boolean</code>&nbsp;or&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Boolean.html"><code style="font-size: 1.2em;">Boolean</code></a>, then the result is the string returned by&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#valueOf(boolean)"><code style="font-size: 1.2em;">String.valueOf(arg)</code></a>. Otherwise, the result is "true".</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"> <code style="font-size: 1.2em;">'h'</code>,&nbsp;<code style="font-size: 1.2em;">'H'</code> </td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">general</td> 
         <td style="padding: 3px 3px 3px 7px;">If the argument&nbsp;<em>arg</em>&nbsp;is&nbsp;<code style="font-size: 1.2em;">null</code>, then the result is "<code style="font-size: 1.2em;">null</code>". Otherwise, the result is obtained by invoking&nbsp;<code style="font-size: 1.2em;">Integer.toHexString(arg.hashCode())</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"> <code style="font-size: 1.2em;">'s'</code>,&nbsp;<code style="font-size: 1.2em;">'S'</code> </td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">general</td> 
         <td style="padding: 3px 3px 3px 7px;">If the argument&nbsp;<em>arg</em>&nbsp;is&nbsp;<code style="font-size: 1.2em;">null</code>, then the result is "<code style="font-size: 1.2em;">null</code>". If&nbsp;<em>arg</em>&nbsp;implements&nbsp;<a style="color: #4c6b87;" title="interface in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formattable.html"><code style="font-size: 1.2em;">Formattable</code></a>, then&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formattable.html#formatTo(java.util.Formatter,%20int,%20int,%20int)"><code style="font-size: 1.2em;">arg.formatTo</code></a>&nbsp;is invoked. Otherwise, the result is obtained by invoking&nbsp;<code style="font-size: 1.2em;">arg.toString()</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"> <code style="font-size: 1.2em;">'c'</code>,&nbsp;<code style="font-size: 1.2em;">'C'</code> </td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">character</td> 
         <td style="padding: 3px 3px 3px 7px;">The result is a Unicode character</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'d'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">integral</td> 
         <td style="padding: 3px 3px 3px 7px;">The result is formatted as a decimal integer</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'o'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">integral</td> 
         <td style="padding: 3px 3px 3px 7px;">The result is formatted as an octal integer</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"> <code style="font-size: 1.2em;">'x'</code>,&nbsp;<code style="font-size: 1.2em;">'X'</code> </td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">integral</td> 
         <td style="padding: 3px 3px 3px 7px;">The result is formatted as a hexadecimal integer</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"> <code style="font-size: 1.2em;">'e'</code>,&nbsp;<code style="font-size: 1.2em;">'E'</code> </td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">floating point</td> 
         <td style="padding: 3px 3px 3px 7px;">The result is formatted as a decimal number in computerized scientific notation</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'f'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">floating point</td> 
         <td style="padding: 3px 3px 3px 7px;">The result is formatted as a decimal number</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"> <code style="font-size: 1.2em;">'g'</code>,&nbsp;<code style="font-size: 1.2em;">'G'</code> </td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">floating point</td> 
         <td style="padding: 3px 3px 3px 7px;">The result is formatted using computerized scientific notation or decimal format, depending on the precision and the value after rounding.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"> <code style="font-size: 1.2em;">'a'</code>,&nbsp;<code style="font-size: 1.2em;">'A'</code> </td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">floating point</td> 
         <td style="padding: 3px 3px 3px 7px;">The result is formatted as a hexadecimal floating-point number with a significand and an exponent</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"> <code style="font-size: 1.2em;">'t'</code>,&nbsp;<code style="font-size: 1.2em;">'T'</code> </td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">date/time</td> 
         <td style="padding: 3px 3px 3px 7px;">Prefix for date and time conversion characters. See&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#dt">Date/Time Conversions</a>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'%'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">percent</td> 
         <td style="padding: 3px 3px 3px 7px;">The result is a literal&nbsp;<code style="font-size: 1.2em;">'%'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0025'</tt>)</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'n'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top">line separator</td> 
         <td style="padding: 3px 3px 3px 7px;">The result is the platform-specific line separator</td> 
        </tr> 
       </tbody>
      </table> 
      <p>Any characters not explicitly defined as conversions are illegal and are reserved for future extensions.</p> 
      <h4 style="font-size: 1.3em;"> <a style="color: #353833;" name="dt"></a>Date/Time Conversions</h4> 
      <p>The following date and time conversion suffix characters are defined for the&nbsp;<code style="font-size: 1.2em;">'t'</code>&nbsp;and&nbsp;<code style="font-size: 1.2em;">'T'</code>&nbsp;conversions. The types are similar to but not completely identical to those defined by GNU&nbsp;<code style="font-size: 1.2em;">date</code>&nbsp;and POSIX&nbsp;<code style="font-size: 1.2em;">strftime(3c)</code>. Additional conversion types are provided to access Java-specific functionality (e.g.&nbsp;<code style="font-size: 1.2em;">'L'</code>&nbsp;for milliseconds within the second).</p> 
      <p>The following conversion characters are used for formatting times:</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="time" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'H'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Hour of the day for the 24-hour clock, formatted as two digits with a leading zero as necessary i.e.&nbsp;<code style="font-size: 1.2em;">00 - 23</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'I'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Hour for the 12-hour clock, formatted as two digits with a leading zero as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">01 - 12</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'k'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Hour of the day for the 24-hour clock, i.e.&nbsp;<code style="font-size: 1.2em;">0 - 23</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'l'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Hour for the 12-hour clock, i.e.&nbsp;<code style="font-size: 1.2em;">1 - 12</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'M'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Minute within the hour formatted as two digits with a leading zero as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">00 - 59</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'S'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Seconds within the minute, formatted as two digits with a leading zero as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">00 - 60</code>&nbsp;("<code style="font-size: 1.2em;">60</code>" is a special value required to support leap seconds).</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'L'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Millisecond within the second formatted as three digits with leading zeros as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">000 - 999</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'N'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Nanosecond within the second, formatted as nine digits with leading zeros as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">000000000 - 999999999</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'p'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Locale-specific&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DateFormatSymbols.html#getAmPmStrings()">morning or afternoon</a>&nbsp;marker in lower case, e.g."<code style="font-size: 1.2em;">am</code>" or "<code style="font-size: 1.2em;">pm</code>". Use of the conversion prefix&nbsp;<code style="font-size: 1.2em;">'T'</code>&nbsp;forces this output to upper case.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'z'</code></td> 
         <td style="padding: 3px 3px 3px 7px;"> <a style="color: #4c6b87;" href="http://www.ietf.org/rfc/rfc0822.txt">RFC&nbsp;822</a>&nbsp;style numeric time zone offset from GMT, e.g.&nbsp;<code style="font-size: 1.2em;">-0800</code>. This value will be adjusted as necessary for Daylight Saving Time. For&nbsp;<code style="font-size: 1.2em;">long</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Long.html"><code style="font-size: 1.2em;">Long</code></a>, and&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Date.html"><code style="font-size: 1.2em;">Date</code></a>&nbsp;the time zone used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/TimeZone.html#getDefault()">default time zone</a>&nbsp;for this instance of the Java virtual machine.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'Z'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">A string representing the abbreviation for the time zone. This value will be adjusted as necessary for Daylight Saving Time. For&nbsp;<code style="font-size: 1.2em;">long</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Long.html"><code style="font-size: 1.2em;">Long</code></a>, and&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Date.html"><code style="font-size: 1.2em;">Date</code></a>&nbsp;the time zone used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/TimeZone.html#getDefault()">default time zone</a>&nbsp;for this instance of the Java virtual machine. The Formatter's locale will supersede the locale of the argument (if any).</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'s'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Seconds since the beginning of the epoch starting at 1 January 1970&nbsp;<code style="font-size: 1.2em;">00:00:00</code>&nbsp;UTC, i.e.&nbsp;<code style="font-size: 1.2em;">Long.MIN_VALUE/1000</code>&nbsp;to&nbsp;<code style="font-size: 1.2em;">Long.MAX_VALUE/1000</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'Q'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Milliseconds since the beginning of the epoch starting at 1 January 1970&nbsp;<code style="font-size: 1.2em;">00:00:00</code>&nbsp;UTC, i.e.&nbsp;<code style="font-size: 1.2em;">Long.MIN_VALUE</code>&nbsp;to&nbsp;<code style="font-size: 1.2em;">Long.MAX_VALUE</code>.</td> 
        </tr> 
       </tbody>
      </table> 
      <p>The following conversion characters are used for formatting dates:</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="date" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'B'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Locale-specific&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DateFormatSymbols.html#getMonths()">full month name</a>, e.g.&nbsp;<code style="font-size: 1.2em;">"January"</code>,&nbsp;<code style="font-size: 1.2em;">"February"</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'b'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Locale-specific&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DateFormatSymbols.html#getShortMonths()">abbreviated month name</a>, e.g.&nbsp;<code style="font-size: 1.2em;">"Jan"</code>,&nbsp;<code style="font-size: 1.2em;">"Feb"</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'h'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Same as&nbsp;<code style="font-size: 1.2em;">'b'</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'A'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Locale-specific full name of the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DateFormatSymbols.html#getWeekdays()">day of the week</a>, e.g.&nbsp;<code style="font-size: 1.2em;">"Sunday"</code>,&nbsp;<code style="font-size: 1.2em;">"Monday"</code> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'a'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Locale-specific short name of the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DateFormatSymbols.html#getShortWeekdays()">day of the week</a>, e.g.&nbsp;<code style="font-size: 1.2em;">"Sun"</code>,&nbsp;<code style="font-size: 1.2em;">"Mon"</code> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'C'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Four-digit year divided by&nbsp;<code style="font-size: 1.2em;">100</code>, formatted as two digits with leading zero as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">00 - 99</code> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'Y'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Year, formatted as at least four digits with leading zeros as necessary, e.g.&nbsp;<code style="font-size: 1.2em;">0092</code>&nbsp;equals&nbsp;<code style="font-size: 1.2em;">92</code>&nbsp;CE for the Gregorian calendar.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'y'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Last two digits of the year, formatted with leading zeros as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">00 - 99</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'j'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Day of year, formatted as three digits with leading zeros as necessary, e.g.&nbsp;<code style="font-size: 1.2em;">001 - 366</code>&nbsp;for the Gregorian calendar.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'m'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Month, formatted as two digits with leading zeros as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">01 - 13</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'d'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Day of month, formatted as two digits with leading zeros as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">01 - 31</code> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'e'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Day of month, formatted as two digits, i.e.&nbsp;<code style="font-size: 1.2em;">1 - 31</code>.</td> 
        </tr> 
       </tbody>
      </table> 
      <p>The following conversion characters are used for formatting common date/time compositions.</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="composites" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'R'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Time formatted for the 24-hour clock as&nbsp;<code style="font-size: 1.2em;">"%tH:%tM"</code> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'T'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Time formatted for the 24-hour clock as&nbsp;<code style="font-size: 1.2em;">"%tH:%tM:%tS"</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'r'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Time formatted for the 12-hour clock as&nbsp;<code style="font-size: 1.2em;">"%tI:%tM:%tS %Tp"</code>. The location of the morning or afternoon marker (<code style="font-size: 1.2em;">'%Tp'</code>) may be locale-dependent.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'D'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Date formatted as&nbsp;<code style="font-size: 1.2em;">"%tm/%td/%ty"</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'F'</code></td> 
         <td style="padding: 3px 3px 3px 7px;"> <a style="color: #4c6b87;" href="http://www.w3.org/TR/NOTE-datetime">ISO&nbsp;8601</a>&nbsp;complete date formatted as&nbsp;<code style="font-size: 1.2em;">"%tY-%tm-%td"</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'c'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">Date and time formatted as&nbsp;<code style="font-size: 1.2em;">"%ta %tb %td %tT %tZ %tY"</code>, e.g.&nbsp;<code style="font-size: 1.2em;">"Sun Jul 20 16:17:00 EDT 1969"</code>.</td> 
        </tr> 
       </tbody>
      </table> 
      <p>Any characters not explicitly defined as date/time conversion suffixes are illegal and are reserved for future extensions.</p> 
      <h4 style="font-size: 1.3em;">Flags</h4> 
      <p>The following table summarizes the supported flags.&nbsp;<em>y</em>&nbsp;means the flag is supported for the indicated argument types.</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="genConv" cellpadding="5">
       <tbody> 
        <tr> 
         <th valign="bottom">Flag</th> 
         <th valign="bottom">General</th> 
         <th valign="bottom">Character</th> 
         <th valign="bottom">Integral</th> 
         <th valign="bottom">Floating Point</th> 
         <th valign="bottom">Date/Time</th> 
         <th valign="bottom">Description</th> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;">'-'</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y</td> 
         <td style="padding: 3px 3px 3px 7px;">The result will be left-justified.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;">'#'</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y<sup style="font-size: 0.6em;">1</sup> </td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y<sup style="font-size: 0.6em;">3</sup> </td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;">The result should use a conversion-dependent alternate form</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;">'+'</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y<sup style="font-size: 0.6em;">4</sup> </td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;">The result will always include a sign</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;">'&nbsp;&nbsp;'</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y<sup style="font-size: 0.6em;">4</sup> </td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;">The result will include a leading space for positive values</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;">'0'</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;">The result will be zero-padded</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;">','</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y<sup style="font-size: 0.6em;">2</sup> </td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y<sup style="font-size: 0.6em;">5</sup> </td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;">The result will include locale-specific&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DecimalFormatSymbols.html#getGroupingSeparator()">grouping separators</a> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;">'('</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">-</td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y<sup style="font-size: 0.6em;">4</sup> </td> 
         <td style="padding: 3px 3px 3px 7px;" align="center" valign="top">y<sup style="font-size: 0.6em;">5</sup> </td> 
         <td style="padding: 3px 3px 3px 7px;" align="center">-</td> 
         <td style="padding: 3px 3px 3px 7px;">The result will enclose negative numbers in parentheses</td> 
        </tr> 
       </tbody>
      </table> 
      <p><sup style="font-size: 0.6em;">1</sup>&nbsp;Depends on the definition of&nbsp;<a style="color: #4c6b87;" title="interface in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formattable.html"><code style="font-size: 1.2em;">Formattable</code></a>.</p> 
      <p><sup style="font-size: 0.6em;">2</sup>&nbsp;For&nbsp;<code style="font-size: 1.2em;">'d'</code>&nbsp;conversion only.</p> 
      <p><sup style="font-size: 0.6em;">3</sup>&nbsp;For&nbsp;<code style="font-size: 1.2em;">'o'</code>,&nbsp;<code style="font-size: 1.2em;">'x'</code>, and&nbsp;<code style="font-size: 1.2em;">'X'</code>&nbsp;conversions only.</p> 
      <p><sup style="font-size: 0.6em;">4</sup>&nbsp;For&nbsp;<code style="font-size: 1.2em;">'d'</code>,&nbsp;<code style="font-size: 1.2em;">'o'</code>,&nbsp;<code style="font-size: 1.2em;">'x'</code>, and&nbsp;<code style="font-size: 1.2em;">'X'</code>&nbsp;conversions applied to&nbsp;<a style="color: #4c6b87;" title="class in java.math" href="http://docs.oracle.com/javase/7/docs/api/java/math/BigInteger.html"><code style="font-size: 1.2em;">BigInteger</code></a>&nbsp;or&nbsp;<code style="font-size: 1.2em;">'d'</code>&nbsp;applied to&nbsp;<code style="font-size: 1.2em;">byte</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Byte.html"><code style="font-size: 1.2em;">Byte</code></a>,&nbsp;<code style="font-size: 1.2em;">short</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Short.html"><code style="font-size: 1.2em;">Short</code></a>,&nbsp;<code style="font-size: 1.2em;">int</code>&nbsp;and&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Integer.html"><code style="font-size: 1.2em;">Integer</code></a>,&nbsp;<code style="font-size: 1.2em;">long</code>, and&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Long.html"><code style="font-size: 1.2em;">Long</code></a>.</p> 
      <p><sup style="font-size: 0.6em;">5</sup>&nbsp;For&nbsp;<code style="font-size: 1.2em;">'e'</code>,&nbsp;<code style="font-size: 1.2em;">'E'</code>,&nbsp;<code style="font-size: 1.2em;">'f'</code>,&nbsp;<code style="font-size: 1.2em;">'g'</code>, and&nbsp;<code style="font-size: 1.2em;">'G'</code>&nbsp;conversions only.</p> 
      <p>Any characters not explicitly defined as flags are illegal and are reserved for future extensions.</p> 
      <h4 style="font-size: 1.3em;">Width</h4> 
      <p>The width is the minimum number of characters to be written to the output. For the line separator conversion, width is not applicable; if it is provided, an exception will be thrown.</p> 
      <h4 style="font-size: 1.3em;">Precision</h4> 
      <p>For general argument types, the precision is the maximum number of characters to be written to the output.</p> 
      <p>For the floating-point conversions&nbsp;<code style="font-size: 1.2em;">'e'</code>,&nbsp;<code style="font-size: 1.2em;">'E'</code>, and&nbsp;<code style="font-size: 1.2em;">'f'</code>&nbsp;the precision is the number of digits after the decimal separator. If the conversion is&nbsp;<code style="font-size: 1.2em;">'g'</code>&nbsp;or&nbsp;<code style="font-size: 1.2em;">'G'</code>, then the precision is the total number of digits in the resulting magnitude after rounding. If the conversion is&nbsp;<code style="font-size: 1.2em;">'a'</code>&nbsp;or&nbsp;<code style="font-size: 1.2em;">'A'</code>, then the precision must not be specified.</p> 
      <p>For character, integral, and date/time argument types and the percent and line separator conversions, the precision is not applicable; if a precision is provided, an exception will be thrown.</p> 
      <h4 style="font-size: 1.3em;">Argument Index</h4> 
      <p>The argument index is a decimal integer indicating the position of the argument in the argument list. The first argument is referenced by "<code style="font-size: 1.2em;">1$</code>", the second by "<code style="font-size: 1.2em;">2$</code>", etc.</p> 
      <p>Another way to reference arguments by position is to use the&nbsp;<code style="font-size: 1.2em;">'&lt;'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u003c'</tt>) flag, which causes the argument for the previous format specifier to be re-used. For example, the following two statements would produce identical strings:</p> 
      <blockquote> 
       <pre>   Calendar c = ...;
   String s1 = String.format("Duke's Birthday: %1$tm %1$te,%1$tY", c);

   String s2 = String.format("Duke's Birthday: %1$tm %&lt;te,%&lt;tY", c);
 </pre> 
      </blockquote> 
      <hr> 
      <h3 style="font-size: 1.4em;"> <a style="color: #353833;" name="detail"></a>Details</h3> 
      <p>This section is intended to provide behavioral details for formatting, including conditions and exceptions, supported data types, localization, and interactions between flags, conversions, and data types. For an overview of formatting concepts, refer to the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#summary">Summary</a></p> 
      <p>Any characters not explicitly defined as conversions, date/time conversion suffixes, or flags are illegal and are reserved for future extensions. Use of such a character in a format string will cause an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/UnknownFormatConversionException.html"><code style="font-size: 1.2em;">UnknownFormatConversionException</code></a>&nbsp;or&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/UnknownFormatFlagsException.html"><code style="font-size: 1.2em;">UnknownFormatFlagsException</code></a>&nbsp;to be thrown.</p> 
      <p>If the format specifier contains a width or precision with an invalid value or which is otherwise unsupported, then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatWidthException.html"><code style="font-size: 1.2em;">IllegalFormatWidthException</code></a>&nbsp;or&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatPrecisionException.html"><code style="font-size: 1.2em;">IllegalFormatPrecisionException</code></a>&nbsp;respectively will be thrown.</p> 
      <p>If a format specifier contains a conversion character that is not applicable to the corresponding argument, then an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatConversionException.html"><code style="font-size: 1.2em;">IllegalFormatConversionException</code></a>&nbsp;will be thrown.</p> 
      <p>All specified exceptions may be thrown by any of the&nbsp;<code style="font-size: 1.2em;">format</code>&nbsp;methods of&nbsp;<code style="font-size: 1.2em;">Formatter</code>&nbsp;as well as by any&nbsp;<code style="font-size: 1.2em;">format</code>&nbsp;convenience methods such as&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#format(java.lang.String,%20java.lang.Object...)"><code style="font-size: 1.2em;">String.format</code></a>&nbsp;and&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/io/PrintStream.html#printf(java.lang.String,%20java.lang.Object...)"><code style="font-size: 1.2em;">PrintStream.printf</code></a>.</p> 
      <p>Conversions denoted by an upper-case character (i.e.&nbsp;<code style="font-size: 1.2em;">'B'</code>,&nbsp;<code style="font-size: 1.2em;">'H'</code>,&nbsp;<code style="font-size: 1.2em;">'S'</code>,&nbsp;<code style="font-size: 1.2em;">'C'</code>,&nbsp;<code style="font-size: 1.2em;">'X'</code>,&nbsp;<code style="font-size: 1.2em;">'E'</code>,&nbsp;<code style="font-size: 1.2em;">'G'</code>,&nbsp;<code style="font-size: 1.2em;">'A'</code>, and&nbsp;<code style="font-size: 1.2em;">'T'</code>) are the same as those for the corresponding lower-case conversion characters except that the result is converted to upper case according to the rules of the prevailing&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html"><code style="font-size: 1.2em;">Locale</code></a>. The result is equivalent to the following invocation of<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#toUpperCase()"><code style="font-size: 1.2em;">String.toUpperCase()</code></a></p> 
      <pre>    out.toUpperCase() </pre> 
      <h4 style="font-size: 1.3em;"> <a style="color: #353833;" name="dgen"></a>General</h4> 
      <p>The following general conversions may be applied to any argument type:</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="dgConv" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'b'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0062'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Produces either "<code style="font-size: 1.2em;">true</code>" or "<code style="font-size: 1.2em;">false</code>" as returned by&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Boolean.html#toString(boolean)"><code style="font-size: 1.2em;">Boolean.toString(boolean)</code></a>. <p>If the argument is&nbsp;<code style="font-size: 1.2em;">null</code>, then the result is "<code style="font-size: 1.2em;">false</code>". If the argument is a&nbsp;<code style="font-size: 1.2em;">boolean</code>&nbsp;or&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Boolean.html"><code style="font-size: 1.2em;">Boolean</code></a>, then the result is the string returned by&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#valueOf(boolean)"><code style="font-size: 1.2em;">String.valueOf()</code></a>. Otherwise, the result is "<code style="font-size: 1.2em;">true</code>".</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given, then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'B'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0042'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">The upper-case variant of&nbsp;<code style="font-size: 1.2em;">'b'</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'h'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0068'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Produces a string representing the hash code value of the object. <p>If the argument,&nbsp;<em>arg</em>&nbsp;is&nbsp;<code style="font-size: 1.2em;">null</code>, then the result is "<code style="font-size: 1.2em;">null</code>". Otherwise, the result is obtained by invoking&nbsp;<code style="font-size: 1.2em;">Integer.toHexString(arg.hashCode())</code>.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given, then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'H'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0048'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">The upper-case variant of&nbsp;<code style="font-size: 1.2em;">'h'</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'s'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0073'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Produces a string. <p>If the argument is&nbsp;<code style="font-size: 1.2em;">null</code>, then the result is "<code style="font-size: 1.2em;">null</code>". If the argument implements&nbsp;<a style="color: #4c6b87;" title="interface in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formattable.html"><code style="font-size: 1.2em;">Formattable</code></a>, then its&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formattable.html#formatTo(java.util.Formatter,%20int,%20int,%20int)"><code style="font-size: 1.2em;">formatTo</code></a>&nbsp;method is invoked. Otherwise, the result is obtained by invoking the argument's&nbsp;<code style="font-size: 1.2em;">toString()</code>&nbsp;method.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given and the argument is not a&nbsp;<a style="color: #4c6b87;" title="interface in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formattable.html"><code style="font-size: 1.2em;">Formattable</code></a>&nbsp;, then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'S'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0053'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">The upper-case variant of&nbsp;<code style="font-size: 1.2em;">'s'</code>.</td> 
        </tr> 
       </tbody>
      </table> 
      <p>The following&nbsp;<a style="color: #353833;" name="dFlags"></a>flags&nbsp;apply to general conversions:</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="dFlags" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'-'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u002d'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Left justifies the output. Spaces (<tt style="font-size: 1.2em;">'\u0020'</tt>) will be added at the end of the converted value as required to fill the minimum width of the field. If the width is not provided, then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/MissingFormatWidthException.html"><code style="font-size: 1.2em;">MissingFormatWidthException</code></a>&nbsp;will be thrown. If this flag is not given then the output will be right-justified.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'#'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0023'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output use an alternate form. The definition of the form is specified by the conversion.</td> 
        </tr> 
       </tbody>
      </table> 
      <p>The&nbsp;<a style="color: #353833;" name="genWidth"></a>width&nbsp;is the minimum number of characters to be written to the output. If the length of the converted value is less than the width then the output will be padded by&nbsp;<tt style="font-size: 1.2em;">'&nbsp;&nbsp;'</tt>&nbsp;(<tt style="font-size: 1.2em;">'\u0020'</tt>) until the total number of characters equals the width. The padding is on the left by default. If the&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;flag is given, then the padding will be on the right. If the width is not specified then there is no minimum.</p> 
      <p>The precision is the maximum number of characters to be written to the output. The precision is applied before the width, thus the output will be truncated to&nbsp;<code style="font-size: 1.2em;">precision</code>&nbsp;characters even if the width is greater than the precision. If the precision is not specified then there is no explicit limit on the number of characters.</p> 
      <h4 style="font-size: 1.3em;"> <a style="color: #353833;" name="dchar"></a>Character</h4> This conversion may be applied to&nbsp;
      <code style="font-size: 1.2em;">char</code>&nbsp;and&nbsp;
      <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Character.html"><code style="font-size: 1.2em;">Character</code></a>. It may also be applied to the types&nbsp;
      <code style="font-size: 1.2em;">byte</code>,&nbsp;
      <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Byte.html"><code style="font-size: 1.2em;">Byte</code></a>,&nbsp;
      <code style="font-size: 1.2em;">short</code>, and&nbsp;
      <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Short.html"><code style="font-size: 1.2em;">Short</code></a>,&nbsp;
      <code style="font-size: 1.2em;">int</code>&nbsp;and&nbsp;
      <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Integer.html"><code style="font-size: 1.2em;">Integer</code></a>&nbsp;when&nbsp;
      <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Character.html#isValidCodePoint(int)"><code style="font-size: 1.2em;">Character.isValidCodePoint(int)</code></a>&nbsp;returns&nbsp;
      <code style="font-size: 1.2em;">true</code>. If it returns&nbsp;
      <code style="font-size: 1.2em;">false</code>&nbsp;then an&nbsp;
      <a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatCodePointException.html"><code style="font-size: 1.2em;">IllegalFormatCodePointException</code></a>&nbsp;will be thrown. 
      <table style="border-bottom-style: none; width: 1863px;" summary="charConv" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'c'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0063'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Formats the argument as a Unicode character as described in&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Character.html#unicode">Unicode Character Representation</a>. This may be more than one 16-bit&nbsp;<code style="font-size: 1.2em;">char</code>&nbsp;in the case where the argument represents a supplementary character. <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given, then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'C'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0043'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">The upper-case variant of&nbsp;<code style="font-size: 1.2em;">'c'</code>.</td> 
        </tr> 
       </tbody>
      </table> 
      <p>The&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;flag defined for&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#dFlags">General conversions</a>&nbsp;applies. If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given, then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> 
      <p>The width is defined as for&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#genWidth">General conversions</a>.</p> 
      <p>The precision is not applicable. If the precision is specified then an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatPrecisionException.html"><code style="font-size: 1.2em;">IllegalFormatPrecisionException</code></a>&nbsp;will be thrown.</p> 
      <h4 style="font-size: 1.3em;"> <a style="color: #353833;" name="dnum"></a>Numeric</h4> 
      <p>Numeric conversions are divided into the following categories:</p> 
      <ol> 
       <li><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#dnint"><strong>Byte, Short, Integer, and Long</strong></a></li> 
       <li><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#dnbint"><strong>BigInteger</strong></a></li> 
       <li><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#dndec"><strong>Float and Double</strong></a></li> 
       <li><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#dnbdec"><strong>BigDecimal</strong></a></li> 
      </ol> 
      <p>Numeric types will be formatted according to the following algorithm:</p> 
      <p><strong><a style="color: #353833;" name="l10n%20algorithm"></a>Number Localization Algorithm</strong></p> 
      <p>After digits are obtained for the integer part, fractional part, and exponent (as appropriate for the data type), the following transformation is applied:</p> 
      <ol> 
       <li>Each digit character&nbsp;<em>d</em>&nbsp;in the string is replaced by a locale-specific digit computed relative to the current locale's&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DecimalFormatSymbols.html#getZeroDigit()">zero digit</a>&nbsp;<em>z</em>; that is&nbsp;<em>d&nbsp;-&nbsp;</em>&nbsp;<code style="font-size: 1.2em;">'0'</code>&nbsp;<em>&nbsp;+&nbsp;z</em>.</li> 
       <li>If a decimal separator is present, a locale-specific&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DecimalFormatSymbols.html#getDecimalSeparator()">decimal separator</a>&nbsp;is substituted.</li> 
       <li>If the&nbsp;<code style="font-size: 1.2em;">','</code>&nbsp;(<tt style="font-size: 1.2em;">'\u002c'</tt>)&nbsp;<a style="color: #353833;" name="l10n%20group"></a>flag&nbsp;is given, then the locale-specific&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DecimalFormatSymbols.html#getGroupingSeparator()">grouping separator</a>&nbsp;is inserted by scanning the integer part of the string from least significant to most significant digits and inserting a separator at intervals defined by the locale's&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DecimalFormat.html#getGroupingSize()">grouping size</a>.</li> 
       <li>If the&nbsp;<code style="font-size: 1.2em;">'0'</code>&nbsp;flag is given, then the locale-specific&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DecimalFormatSymbols.html#getZeroDigit()">zero digits</a>&nbsp;are inserted after the sign character, if any, and before the first non-zero digit, until the length of the string is equal to the requested field width.</li> 
       <li>If the value is negative and the&nbsp;<code style="font-size: 1.2em;">'('</code>&nbsp;flag is given, then a&nbsp;<code style="font-size: 1.2em;">'('</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0028'</tt>) is prepended and a&nbsp;<code style="font-size: 1.2em;">')'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0029'</tt>) is appended.</li> 
       <li>If the value is negative (or floating-point negative zero) and&nbsp;<code style="font-size: 1.2em;">'('</code>&nbsp;flag is not given, then a&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u002d'</tt>) is prepended.</li> 
       <li>If the&nbsp;<code style="font-size: 1.2em;">'+'</code>&nbsp;flag is given and the value is positive or zero (or floating-point positive zero), then a&nbsp;<code style="font-size: 1.2em;">'+'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u002b'</tt>) will be prepended.</li> 
      </ol> 
      <p>If the value is NaN or positive infinity the literal strings "NaN" or "Infinity" respectively, will be output. If the value is negative infinity, then the output will be "(Infinity)" if the&nbsp;<code style="font-size: 1.2em;">'('</code>&nbsp;flag is given otherwise the output will be "-Infinity". These values are not localized.</p> 
      <p><a style="color: #353833;" name="dnint"></a><strong>Byte, Short, Integer, and Long</strong></p> 
      <p>The following conversions may be applied to&nbsp;<code style="font-size: 1.2em;">byte</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Byte.html"><code style="font-size: 1.2em;">Byte</code></a>,&nbsp;<code style="font-size: 1.2em;">short</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Short.html"><code style="font-size: 1.2em;">Short</code></a>,&nbsp;<code style="font-size: 1.2em;">int</code>&nbsp;and&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Integer.html"><code style="font-size: 1.2em;">Integer</code></a>,&nbsp;<code style="font-size: 1.2em;">long</code>, and&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Long.html"><code style="font-size: 1.2em;">Long</code></a>.</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="IntConv" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'d'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0054'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Formats the argument as a decimal integer. The&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#l10n%20algorithm">localization algorithm</a>&nbsp;is applied. <p>If the&nbsp;<code style="font-size: 1.2em;">'0'</code>&nbsp;flag is given and the value is negative, then the zero padding will occur after the sign.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'o'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u006f'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Formats the argument as an integer in base eight. No localization is applied. <p>If&nbsp;<em>x</em>&nbsp;is negative then the result will be an unsigned value generated by adding 2<sup style="font-size: 0.6em;">n</sup>&nbsp;to the value where&nbsp;<code style="font-size: 1.2em;">n</code>&nbsp;is the number of bits in the type as returned by the static&nbsp;<code style="font-size: 1.2em;">SIZE</code>&nbsp;field in the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Byte.html#SIZE">Byte</a>,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Short.html#SIZE">Short</a>,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Integer.html#SIZE">Integer</a>, or&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Long.html#SIZE">Long</a>&nbsp;classes as appropriate.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given then the output will always begin with the radix indicator&nbsp;<code style="font-size: 1.2em;">'0'</code>.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'0'</code>&nbsp;flag is given then the output will be padded with leading zeros to the field width following any indication of sign.</p> <p>If&nbsp;<code style="font-size: 1.2em;">'('</code>,&nbsp;<code style="font-size: 1.2em;">'+'</code>, '&nbsp;&nbsp;', or&nbsp;<code style="font-size: 1.2em;">','</code>&nbsp;flags are given then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'x'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0078'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Formats the argument as an integer in base sixteen. No localization is applied. <p>If&nbsp;<em>x</em>&nbsp;is negative then the result will be an unsigned value generated by adding 2<sup style="font-size: 0.6em;">n</sup>&nbsp;to the value where&nbsp;<code style="font-size: 1.2em;">n</code>&nbsp;is the number of bits in the type as returned by the static&nbsp;<code style="font-size: 1.2em;">SIZE</code>&nbsp;field in the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Byte.html#SIZE">Byte</a>,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Short.html#SIZE">Short</a>,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Integer.html#SIZE">Integer</a>, or&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Long.html#SIZE">Long</a>&nbsp;classes as appropriate.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given then the output will always begin with the radix indicator&nbsp;<code style="font-size: 1.2em;">"0x"</code>.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'0'</code>&nbsp;flag is given then the output will be padded to the field width with leading zeros after the radix indicator or sign (if present).</p> <p>If&nbsp;<code style="font-size: 1.2em;">'('</code>,&nbsp;<tt style="font-size: 1.2em;">'&nbsp;&nbsp;'</tt>,&nbsp;<code style="font-size: 1.2em;">'+'</code>, or&nbsp;<code style="font-size: 1.2em;">','</code>&nbsp;flags are given then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'X'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0058'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">The upper-case variant of&nbsp;<code style="font-size: 1.2em;">'x'</code>. The entire string representing the number will be converted to&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#toUpperCase(java.util.Locale)">upper case</a>&nbsp;including the&nbsp;<code style="font-size: 1.2em;">'x'</code>&nbsp;(if any) and all hexadecimal digits&nbsp;<code style="font-size: 1.2em;">'a'</code>&nbsp;-&nbsp;<code style="font-size: 1.2em;">'f'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0061'</tt>&nbsp;-&nbsp;<tt style="font-size: 1.2em;">'\u0066'</tt>).</td> 
        </tr> 
       </tbody>
      </table> 
      <p>If the conversion is&nbsp;<code style="font-size: 1.2em;">'o'</code>,&nbsp;<code style="font-size: 1.2em;">'x'</code>, or&nbsp;<code style="font-size: 1.2em;">'X'</code>&nbsp;and both the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;and the&nbsp;<code style="font-size: 1.2em;">'0'</code>&nbsp;flags are given, then result will contain the radix indicator (<code style="font-size: 1.2em;">'0'</code>&nbsp;for octal and&nbsp;<code style="font-size: 1.2em;">"0x"</code>&nbsp;or&nbsp;<code style="font-size: 1.2em;">"0X"</code>&nbsp;for hexadecimal), some number of zeros (based on the width), and the value.</p> 
      <p>If the&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;flag is not given, then the space padding will occur before the sign.</p> 
      <p>The following&nbsp;<a style="color: #353833;" name="intFlags"></a>flags&nbsp;apply to numeric integral conversions:</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="intFlags" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'+'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u002b'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to include a positive sign for all positive numbers. If this flag is not given then only negative values will include a sign. <p>If both the&nbsp;<code style="font-size: 1.2em;">'+'</code>&nbsp;and&nbsp;<tt style="font-size: 1.2em;">'&nbsp;&nbsp;'</tt>&nbsp;flags are given then an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatFlagsException.html"><code style="font-size: 1.2em;">IllegalFormatFlagsException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'&nbsp;&nbsp;'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0020'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to include a single extra space (<tt style="font-size: 1.2em;">'\u0020'</tt>) for non-negative values. <p>If both the&nbsp;<code style="font-size: 1.2em;">'+'</code>&nbsp;and&nbsp;<tt style="font-size: 1.2em;">'&nbsp;&nbsp;'</tt>&nbsp;flags are given then an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatFlagsException.html"><code style="font-size: 1.2em;">IllegalFormatFlagsException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'0'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0030'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to be padded with leading&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DecimalFormatSymbols.html#getZeroDigit()">zeros</a>&nbsp;to the minimum field width following any sign or radix indicator except when converting NaN or infinity. If the width is not provided, then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/MissingFormatWidthException.html"><code style="font-size: 1.2em;">MissingFormatWidthException</code></a>&nbsp;will be thrown. <p>If both the&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;and&nbsp;<code style="font-size: 1.2em;">'0'</code>&nbsp;flags are given then an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatFlagsException.html"><code style="font-size: 1.2em;">IllegalFormatFlagsException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">','</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u002c'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to include the locale-specific&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DecimalFormatSymbols.html#getGroupingSeparator()">group separators</a>&nbsp;as described in the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#l10n%20group">"group" section</a>&nbsp;of the localization algorithm.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'('</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0028'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to prepend a&nbsp;<code style="font-size: 1.2em;">'('</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0028'</tt>) and append a&nbsp;<code style="font-size: 1.2em;">')'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0029'</tt>) to negative values.</td> 
        </tr> 
       </tbody>
      </table> 
      <p>If no&nbsp;<a style="color: #353833;" name="intdFlags"></a>flags&nbsp;are given the default formatting is as follows:</p> 
      <ul> 
       <li>The output is right-justified within the&nbsp;<code style="font-size: 1.2em;">width</code> </li> 
       <li>Negative numbers begin with a&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u002d'</tt>)</li> 
       <li>Positive numbers and zero do not include a sign or extra leading space</li> 
       <li>No grouping separators are included</li> 
      </ul> 
      <p>The&nbsp;<a style="color: #353833;" name="intWidth"></a>width&nbsp;is the minimum number of characters to be written to the output. This includes any signs, digits, grouping separators, radix indicator, and parentheses. If the length of the converted value is less than the width then the output will be padded by spaces (<tt style="font-size: 1.2em;">'\u0020'</tt>) until the total number of characters equals width. The padding is on the left by default. If&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;flag is given then the padding will be on the right. If width is not specified then there is no minimum.</p> 
      <p>The precision is not applicable. If precision is specified then an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatPrecisionException.html"><code style="font-size: 1.2em;">IllegalFormatPrecisionException</code></a>&nbsp;will be thrown.</p> 
      <p><a style="color: #353833;" name="dnbint"></a><strong>BigInteger</strong></p> 
      <p>The following conversions may be applied to&nbsp;<a style="color: #4c6b87;" title="class in java.math" href="http://docs.oracle.com/javase/7/docs/api/java/math/BigInteger.html"><code style="font-size: 1.2em;">BigInteger</code></a>.</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="BIntConv" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'d'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0054'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to be formatted as a decimal integer. The&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#l10n%20algorithm">localization algorithm</a>&nbsp;is applied. <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'o'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u006f'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to be formatted as an integer in base eight. No localization is applied. <p>If&nbsp;<em>x</em>&nbsp;is negative then the result will be a signed value beginning with&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u002d'</tt>). Signed output is allowed for this type because unlike the primitive types it is not possible to create an unsigned equivalent without assuming an explicit data-type size.</p> <p>If&nbsp;<em>x</em>&nbsp;is positive or zero and the&nbsp;<code style="font-size: 1.2em;">'+'</code>&nbsp;flag is given then the result will begin with&nbsp;<code style="font-size: 1.2em;">'+'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u002b'</tt>).</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given then the output will always begin with&nbsp;<code style="font-size: 1.2em;">'0'</code>&nbsp;prefix.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'0'</code>&nbsp;flag is given then the output will be padded with leading zeros to the field width following any indication of sign.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">','</code>&nbsp;flag is given then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'x'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0078'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to be formatted as an integer in base sixteen. No localization is applied. <p>If&nbsp;<em>x</em>&nbsp;is negative then the result will be a signed value beginning with&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u002d'</tt>). Signed output is allowed for this type because unlike the primitive types it is not possible to create an unsigned equivalent without assuming an explicit data-type size.</p> <p>If&nbsp;<em>x</em>&nbsp;is positive or zero and the&nbsp;<code style="font-size: 1.2em;">'+'</code>&nbsp;flag is given then the result will begin with&nbsp;<code style="font-size: 1.2em;">'+'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u002b'</tt>).</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given then the output will always begin with the radix indicator&nbsp;<code style="font-size: 1.2em;">"0x"</code>.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'0'</code>&nbsp;flag is given then the output will be padded to the field width with leading zeros after the radix indicator or sign (if present).</p> <p>If the&nbsp;<code style="font-size: 1.2em;">','</code>&nbsp;flag is given then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'X'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0058'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">The upper-case variant of&nbsp;<code style="font-size: 1.2em;">'x'</code>. The entire string representing the number will be converted to&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#toUpperCase(java.util.Locale)">upper case</a>&nbsp;including the&nbsp;<code style="font-size: 1.2em;">'x'</code>&nbsp;(if any) and all hexadecimal digits&nbsp;<code style="font-size: 1.2em;">'a'</code>&nbsp;-&nbsp;<code style="font-size: 1.2em;">'f'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0061'</tt>&nbsp;-&nbsp;<tt style="font-size: 1.2em;">'\u0066'</tt>).</td> 
        </tr> 
       </tbody>
      </table> 
      <p>If the conversion is&nbsp;<code style="font-size: 1.2em;">'o'</code>,&nbsp;<code style="font-size: 1.2em;">'x'</code>, or&nbsp;<code style="font-size: 1.2em;">'X'</code>&nbsp;and both the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;and the&nbsp;<code style="font-size: 1.2em;">'0'</code>&nbsp;flags are given, then result will contain the base indicator (<code style="font-size: 1.2em;">'0'</code>&nbsp;for octal and&nbsp;<code style="font-size: 1.2em;">"0x"</code>&nbsp;or&nbsp;<code style="font-size: 1.2em;">"0X"</code>&nbsp;for hexadecimal), some number of zeros (based on the width), and the value.</p> 
      <p>If the&nbsp;<code style="font-size: 1.2em;">'0'</code>&nbsp;flag is given and the value is negative, then the zero padding will occur after the sign.</p> 
      <p>If the&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;flag is not given, then the space padding will occur before the sign.</p> 
      <p>All&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#intFlags">flags</a>&nbsp;defined for Byte, Short, Integer, and Long apply. The&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#intdFlags">default behavior</a>&nbsp;when no flags are given is the same as for Byte, Short, Integer, and Long.</p> 
      <p>The specification of&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#intWidth">width</a>&nbsp;is the same as defined for Byte, Short, Integer, and Long.</p> 
      <p>The precision is not applicable. If precision is specified then an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatPrecisionException.html"><code style="font-size: 1.2em;">IllegalFormatPrecisionException</code></a>&nbsp;will be thrown.</p> 
      <p><a style="color: #353833;" name="dndec"></a><strong>Float and Double</strong></p> 
      <p>The following conversions may be applied to&nbsp;<code style="font-size: 1.2em;">float</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Float.html"><code style="font-size: 1.2em;">Float</code></a>,&nbsp;<code style="font-size: 1.2em;">double</code>&nbsp;and&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Double.html"><code style="font-size: 1.2em;">Double</code></a>.</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="floatConv" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'e'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0065'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to be formatted using&nbsp;<a style="color: #353833;" name="scientific"></a>computerized scientific notation. The&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#l10n%20algorithm">localization algorithm</a>&nbsp;is applied. <p>The formatting of the magnitude&nbsp;<em>m</em>&nbsp;depends upon its value.</p> <p>If&nbsp;<em>m</em>&nbsp;is NaN or infinite, the literal strings "NaN" or "Infinity", respectively, will be output. These values are not localized.</p> <p>If&nbsp;<em>m</em>&nbsp;is positive-zero or negative-zero, then the exponent will be&nbsp;<code style="font-size: 1.2em;">"+00"</code>.</p> <p>Otherwise, the result is a string that represents the sign and magnitude (absolute value) of the argument. The formatting of the sign is described in the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#l10n%20algorithm">localization algorithm</a>. The formatting of the magnitude&nbsp;<em>m</em>&nbsp;depends upon its value.</p> <p>Let&nbsp;<em>n</em>&nbsp;be the unique integer such that 10<sup style="font-size: 0.6em;"><em>n</em></sup>&nbsp;&lt;=&nbsp;<em>m</em>&nbsp;&lt; 10<sup style="font-size: 0.6em;"><em>n</em>+1</sup>; then let&nbsp;<em>a</em>&nbsp;be the mathematically exact quotient of&nbsp;<em>m</em>&nbsp;and 10<sup style="font-size: 0.6em;"><em>n</em></sup>&nbsp;so that 1 &lt;=&nbsp;<em>a</em>&nbsp;&lt; 10. The magnitude is then represented as the integer part of&nbsp;<em>a</em>, as a single decimal digit, followed by the decimal separator followed by decimal digits representing the fractional part of&nbsp;<em>a</em>, followed by the exponent symbol&nbsp;<code style="font-size: 1.2em;">'e'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0065'</tt>), followed by the sign of the exponent, followed by a representation of&nbsp;<em>n</em>&nbsp;as a decimal integer, as produced by the method&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Long.html#toString(long,%20int)"><code style="font-size: 1.2em;">Long.toString(long, int)</code></a>, and zero-padded to include at least two digits.</p> <p>The number of digits in the result for the fractional part of&nbsp;<em>m</em>&nbsp;or&nbsp;<em>a</em>&nbsp;is equal to the precision. If the precision is not specified then the default value is&nbsp;<code style="font-size: 1.2em;">6</code>. If the precision is less than the number of digits which would appear after the decimal point in the string returned by&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Float.html#toString(float)"><code style="font-size: 1.2em;">Float.toString(float)</code></a>&nbsp;or&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Double.html#toString(double)"><code style="font-size: 1.2em;">Double.toString(double)</code></a>respectively, then the value will be rounded using the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/math/BigDecimal.html#ROUND_HALF_UP">round half up algorithm</a>. Otherwise, zeros may be appended to reach the precision. For a canonical representation of the value, use&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Float.html#toString(float)"><code style="font-size: 1.2em;">Float.toString(float)</code></a>&nbsp;or&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Double.html#toString(double)"><code style="font-size: 1.2em;">Double.toString(double)</code></a>&nbsp;as appropriate.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">','</code>&nbsp;flag is given, then an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'E'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0045'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">The upper-case variant of&nbsp;<code style="font-size: 1.2em;">'e'</code>. The exponent symbol will be&nbsp;<code style="font-size: 1.2em;">'E'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0045'</tt>).</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'g'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0067'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to be formatted in general scientific notation as described below. The&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#l10n%20algorithm">localization algorithm</a>&nbsp;is applied. <p>After rounding for the precision, the formatting of the resulting magnitude&nbsp;<em>m</em>&nbsp;depends on its value.</p> <p>If&nbsp;<em>m</em>&nbsp;is greater than or equal to 10<sup style="font-size: 0.6em;">-4</sup>&nbsp;but less than 10<sup style="font-size: 0.6em;">precision</sup>&nbsp;then it is represented in&nbsp;<em><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#decimal">decimal format</a></em>.</p> <p>If&nbsp;<em>m</em>&nbsp;is less than 10<sup style="font-size: 0.6em;">-4</sup>&nbsp;or greater than or equal to 10<sup style="font-size: 0.6em;">precision</sup>, then it is represented in&nbsp;<em><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#scientific">computerized scientific notation</a></em>.</p> <p>The total number of significant digits in&nbsp;<em>m</em>&nbsp;is equal to the precision. If the precision is not specified, then the default value is&nbsp;<code style="font-size: 1.2em;">6</code>. If the precision is&nbsp;<code style="font-size: 1.2em;">0</code>, then it is taken to be&nbsp;<code style="font-size: 1.2em;">1</code>.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given then an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'G'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0047'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">The upper-case variant of&nbsp;<code style="font-size: 1.2em;">'g'</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'f'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0066'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to be formatted using&nbsp;<a style="color: #353833;" name="decimal"></a>decimal format. The&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#l10n%20algorithm">localization algorithm</a>&nbsp;is applied. <p>The result is a string that represents the sign and magnitude (absolute value) of the argument. The formatting of the sign is described in the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#l10n%20algorithm">localization algorithm</a>. The formatting of the magnitude&nbsp;<em>m</em>&nbsp;depends upon its value.</p> <p>If&nbsp;<em>m</em>&nbsp;NaN or infinite, the literal strings "NaN" or "Infinity", respectively, will be output. These values are not localized.</p> <p>The magnitude is formatted as the integer part of&nbsp;<em>m</em>, with no leading zeroes, followed by the decimal separator followed by one or more decimal digits representing the fractional part of&nbsp;<em>m</em>.</p> <p>The number of digits in the result for the fractional part of&nbsp;<em>m</em>&nbsp;or&nbsp;<em>a</em>&nbsp;is equal to the precision. If the precision is not specified then the default value is&nbsp;<code style="font-size: 1.2em;">6</code>. If the precision is less than the number of digits which would appear after the decimal point in the string returned by&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Float.html#toString(float)"><code style="font-size: 1.2em;">Float.toString(float)</code></a>&nbsp;or&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Double.html#toString(double)"><code style="font-size: 1.2em;">Double.toString(double)</code></a>respectively, then the value will be rounded using the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/math/BigDecimal.html#ROUND_HALF_UP">round half up algorithm</a>. Otherwise, zeros may be appended to reach the precision. For a canonical representation of the value, use&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Float.html#toString(float)"><code style="font-size: 1.2em;">Float.toString(float)</code></a>&nbsp;or&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Double.html#toString(double)"><code style="font-size: 1.2em;">Double.toString(double)</code></a>&nbsp;as appropriate.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'a'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0061'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to be formatted in hexadecimal exponential form. No localization is applied. <p>The result is a string that represents the sign and magnitude (absolute value) of the argument&nbsp;<em>x</em>.</p> <p>If&nbsp;<em>x</em>&nbsp;is negative or a negative-zero value then the result will begin with&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u002d'</tt>).</p> <p>If&nbsp;<em>x</em>&nbsp;is positive or a positive-zero value and the&nbsp;<code style="font-size: 1.2em;">'+'</code>&nbsp;flag is given then the result will begin with&nbsp;<code style="font-size: 1.2em;">'+'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u002b'</tt>).</p> <p>The formatting of the magnitude&nbsp;<em>m</em>&nbsp;depends upon its value.</p> 
          <ul> 
           <li>If the value is NaN or infinite, the literal strings "NaN" or "Infinity", respectively, will be output.</li> 
           <li>If&nbsp;<em>m</em>&nbsp;is zero then it is represented by the string&nbsp;<code style="font-size: 1.2em;">"0x0.0p0"</code>.</li> 
           <li>If&nbsp;<em>m</em>&nbsp;is a&nbsp;<code style="font-size: 1.2em;">double</code>&nbsp;value with a normalized representation then substrings are used to represent the significand and exponent fields. The significand is represented by the characters&nbsp;<code style="font-size: 1.2em;">"0x1."</code>&nbsp;followed by the hexadecimal representation of the rest of the significand as a fraction. The exponent is represented by&nbsp;<code style="font-size: 1.2em;">'p'</code>(<tt style="font-size: 1.2em;">'\u0070'</tt>) followed by a decimal string of the unbiased exponent as if produced by invoking&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Integer.html#toString(int)"><code style="font-size: 1.2em;">Integer.toString</code></a>&nbsp;on the exponent value.</li> 
           <li>If&nbsp;<em>m</em>&nbsp;is a&nbsp;<code style="font-size: 1.2em;">double</code>&nbsp;value with a subnormal representation then the significand is represented by the characters&nbsp;<code style="font-size: 1.2em;">'0x0.'</code>&nbsp;followed by the hexadecimal representation of the rest of the significand as a fraction. The exponent is represented by&nbsp;<code style="font-size: 1.2em;">'p-1022'</code>. Note that there must be at least one nonzero digit in a subnormal significand.</li> 
          </ul> <p>If the&nbsp;<code style="font-size: 1.2em;">'('</code>&nbsp;or&nbsp;<code style="font-size: 1.2em;">','</code>&nbsp;flags are given, then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'A'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0041'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">The upper-case variant of&nbsp;<code style="font-size: 1.2em;">'a'</code>. The entire string representing the number will be converted to upper case including the&nbsp;<code style="font-size: 1.2em;">'x'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0078'</tt>) and&nbsp;<code style="font-size: 1.2em;">'p'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0070'</tt>&nbsp;and all hexadecimal digits&nbsp;<code style="font-size: 1.2em;">'a'</code>&nbsp;-&nbsp;<code style="font-size: 1.2em;">'f'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0061'</tt>&nbsp;-&nbsp;<tt style="font-size: 1.2em;">'\u0066'</tt>).</td> 
        </tr> 
       </tbody>
      </table> 
      <p>All&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#intFlags">flags</a>&nbsp;defined for Byte, Short, Integer, and Long apply.</p> 
      <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given, then the decimal separator will always be present.</p> 
      <p>If no&nbsp;<a style="color: #353833;" name="floatdFlags"></a>flags&nbsp;are given the default formatting is as follows:</p> 
      <ul> 
       <li>The output is right-justified within the&nbsp;<code style="font-size: 1.2em;">width</code> </li> 
       <li>Negative numbers begin with a&nbsp;<code style="font-size: 1.2em;">'-'</code> </li> 
       <li>Positive numbers and positive zero do not include a sign or extra leading space</li> 
       <li>No grouping separators are included</li> 
       <li>The decimal separator will only appear if a digit follows it</li> 
      </ul> 
      <p>The&nbsp;<a style="color: #353833;" name="floatDWidth"></a>width&nbsp;is the minimum number of characters to be written to the output. This includes any signs, digits, grouping separators, decimal separators, exponential symbol, radix indicator, parentheses, and strings representing infinity and NaN as applicable. If the length of the converted value is less than the width then the output will be padded by spaces (<tt style="font-size: 1.2em;">'\u0020'</tt>) until the total number of characters equals width. The padding is on the left by default. If the&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;flag is given then the padding will be on the right. If width is not specified then there is no minimum.</p> 
      <p>If the&nbsp;<a style="color: #353833;" name="floatDPrec"></a>conversion&nbsp;is&nbsp;<code style="font-size: 1.2em;">'e'</code>,&nbsp;<code style="font-size: 1.2em;">'E'</code>&nbsp;or&nbsp;<code style="font-size: 1.2em;">'f'</code>, then the precision is the number of digits after the decimal separator. If the precision is not specified, then it is assumed to be&nbsp;<code style="font-size: 1.2em;">6</code>.</p> 
      <p>If the conversion is&nbsp;<code style="font-size: 1.2em;">'g'</code>&nbsp;or&nbsp;<code style="font-size: 1.2em;">'G'</code>, then the precision is the total number of significant digits in the resulting magnitude after rounding. If the precision is not specified, then the default value is&nbsp;<code style="font-size: 1.2em;">6</code>. If the precision is&nbsp;<code style="font-size: 1.2em;">0</code>, then it is taken to be&nbsp;<code style="font-size: 1.2em;">1</code>.</p> 
      <p>If the conversion is&nbsp;<code style="font-size: 1.2em;">'a'</code>&nbsp;or&nbsp;<code style="font-size: 1.2em;">'A'</code>, then the precision is the number of hexadecimal digits after the decimal separator. If the precision is not provided, then all of the digits as returned by&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Double.html#toHexString(double)"><code style="font-size: 1.2em;">Double.toHexString(double)</code></a>&nbsp;will be output.</p> 
      <p><a style="color: #353833;" name="dnbdec"></a><strong>BigDecimal</strong></p> 
      <p>The following conversions may be applied&nbsp;<a style="color: #4c6b87;" title="class in java.math" href="http://docs.oracle.com/javase/7/docs/api/java/math/BigDecimal.html"><code style="font-size: 1.2em;">BigDecimal</code></a>.</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="floatConv" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'e'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0065'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to be formatted using&nbsp;<a style="color: #353833;" name="bscientific"></a>computerized scientific notation. The&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#l10n%20algorithm">localization algorithm</a>&nbsp;is applied. <p>The formatting of the magnitude&nbsp;<em>m</em>&nbsp;depends upon its value.</p> <p>If&nbsp;<em>m</em>&nbsp;is positive-zero or negative-zero, then the exponent will be&nbsp;<code style="font-size: 1.2em;">"+00"</code>.</p> <p>Otherwise, the result is a string that represents the sign and magnitude (absolute value) of the argument. The formatting of the sign is described in the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#l10n%20algorithm">localization algorithm</a>. The formatting of the magnitude&nbsp;<em>m</em>&nbsp;depends upon its value.</p> <p>Let&nbsp;<em>n</em>&nbsp;be the unique integer such that 10<sup style="font-size: 0.6em;"><em>n</em></sup>&nbsp;&lt;=&nbsp;<em>m</em>&nbsp;&lt; 10<sup style="font-size: 0.6em;"><em>n</em>+1</sup>; then let&nbsp;<em>a</em>&nbsp;be the mathematically exact quotient of&nbsp;<em>m</em>&nbsp;and 10<sup style="font-size: 0.6em;"><em>n</em></sup>&nbsp;so that 1 &lt;=&nbsp;<em>a</em>&nbsp;&lt; 10. The magnitude is then represented as the integer part of&nbsp;<em>a</em>, as a single decimal digit, followed by the decimal separator followed by decimal digits representing the fractional part of&nbsp;<em>a</em>, followed by the exponent symbol&nbsp;<code style="font-size: 1.2em;">'e'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0065'</tt>), followed by the sign of the exponent, followed by a representation of&nbsp;<em>n</em>&nbsp;as a decimal integer, as produced by the method&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Long.html#toString(long,%20int)"><code style="font-size: 1.2em;">Long.toString(long, int)</code></a>, and zero-padded to include at least two digits.</p> <p>The number of digits in the result for the fractional part of&nbsp;<em>m</em>&nbsp;or&nbsp;<em>a</em>&nbsp;is equal to the precision. If the precision is not specified then the default value is&nbsp;<code style="font-size: 1.2em;">6</code>. If the precision is less than the number of digits to the right of the decimal point then the value will be rounded using the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/math/BigDecimal.html#ROUND_HALF_UP">round half up algorithm</a>. Otherwise, zeros may be appended to reach the precision. For a canonical representation of the value, use&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/math/BigDecimal.html#toString()"><code style="font-size: 1.2em;">BigDecimal.toString()</code></a>.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">','</code>&nbsp;flag is given, then an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'E'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0045'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">The upper-case variant of&nbsp;<code style="font-size: 1.2em;">'e'</code>. The exponent symbol will be&nbsp;<code style="font-size: 1.2em;">'E'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0045'</tt>).</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'g'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0067'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to be formatted in general scientific notation as described below. The&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#l10n%20algorithm">localization algorithm</a>&nbsp;is applied. <p>After rounding for the precision, the formatting of the resulting magnitude&nbsp;<em>m</em>&nbsp;depends on its value.</p> <p>If&nbsp;<em>m</em>&nbsp;is greater than or equal to 10<sup style="font-size: 0.6em;">-4</sup>&nbsp;but less than 10<sup style="font-size: 0.6em;">precision</sup>&nbsp;then it is represented in&nbsp;<em><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#bdecimal">decimal format</a></em>.</p> <p>If&nbsp;<em>m</em>&nbsp;is less than 10<sup style="font-size: 0.6em;">-4</sup>&nbsp;or greater than or equal to 10<sup style="font-size: 0.6em;">precision</sup>, then it is represented in&nbsp;<em><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#bscientific">computerized scientific notation</a></em>.</p> <p>The total number of significant digits in&nbsp;<em>m</em>&nbsp;is equal to the precision. If the precision is not specified, then the default value is&nbsp;<code style="font-size: 1.2em;">6</code>. If the precision is&nbsp;<code style="font-size: 1.2em;">0</code>, then it is taken to be&nbsp;<code style="font-size: 1.2em;">1</code>.</p> <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given then an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'G'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0047'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">The upper-case variant of&nbsp;<code style="font-size: 1.2em;">'g'</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'f'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0066'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Requires the output to be formatted using&nbsp;<a style="color: #353833;" name="bdecimal"></a>decimal format. The&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#l10n%20algorithm">localization algorithm</a>&nbsp;is applied. <p>The result is a string that represents the sign and magnitude (absolute value) of the argument. The formatting of the sign is described in the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#l10n%20algorithm">localization algorithm</a>. The formatting of the magnitude&nbsp;<em>m</em>&nbsp;depends upon its value.</p> <p>The magnitude is formatted as the integer part of&nbsp;<em>m</em>, with no leading zeroes, followed by the decimal separator followed by one or more decimal digits representing the fractional part of&nbsp;<em>m</em>.</p> <p>The number of digits in the result for the fractional part of&nbsp;<em>m</em>&nbsp;or&nbsp;<em>a</em>&nbsp;is equal to the precision. If the precision is not specified then the default value is&nbsp;<code style="font-size: 1.2em;">6</code>. If the precision is less than the number of digits to the right of the decimal point then the value will be rounded using the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/math/BigDecimal.html#ROUND_HALF_UP">round half up algorithm</a>. Otherwise, zeros may be appended to reach the precision. For a canonical representation of the value, use&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/math/BigDecimal.html#toString()"><code style="font-size: 1.2em;">BigDecimal.toString()</code></a>.</p> </td> 
        </tr> 
       </tbody>
      </table> 
      <p>All&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#intFlags">flags</a>&nbsp;defined for Byte, Short, Integer, and Long apply.</p> 
      <p>If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given, then the decimal separator will always be present.</p> 
      <p>The&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#floatdFlags">default behavior</a>&nbsp;when no flags are given is the same as for Float and Double.</p> 
      <p>The specification of&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#floatDWidth">width</a>&nbsp;and&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#floatDPrec">precision</a>&nbsp;is the same as defined for Float and Double.</p> 
      <h4 style="font-size: 1.3em;"> <a style="color: #353833;" name="ddt"></a>Date/Time</h4> 
      <p>This conversion may be applied to&nbsp;<code style="font-size: 1.2em;">long</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Long.html"><code style="font-size: 1.2em;">Long</code></a>,&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Calendar.html"><code style="font-size: 1.2em;">Calendar</code></a>, and&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Date.html"><code style="font-size: 1.2em;">Date</code></a>.</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="DTConv" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'t'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0074'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Prefix for date and time conversion characters.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'T'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0054'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">The upper-case variant of&nbsp;<code style="font-size: 1.2em;">'t'</code>.</td> 
        </tr> 
       </tbody>
      </table> 
      <p>The following date and time conversion character suffixes are defined for the&nbsp;<code style="font-size: 1.2em;">'t'</code>&nbsp;and&nbsp;<code style="font-size: 1.2em;">'T'</code>&nbsp;conversions. The types are similar to but not completely identical to those defined by GNU&nbsp;<code style="font-size: 1.2em;">date</code>&nbsp;and POSIX&nbsp;<code style="font-size: 1.2em;">strftime(3c)</code>. Additional conversion types are provided to access Java-specific functionality (e.g.&nbsp;<code style="font-size: 1.2em;">'L'</code>&nbsp;for milliseconds within the second).</p> 
      <p>The following conversion characters are used for formatting times:</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="time" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'H'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0048'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Hour of the day for the 24-hour clock, formatted as two digits with a leading zero as necessary i.e.&nbsp;<code style="font-size: 1.2em;">00 - 23</code>.&nbsp;<code style="font-size: 1.2em;">00</code>&nbsp;corresponds to midnight.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'I'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0049'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Hour for the 12-hour clock, formatted as two digits with a leading zero as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">01 - 12</code>.&nbsp;<code style="font-size: 1.2em;">01</code>&nbsp;corresponds to one o'clock (either morning or afternoon).</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'k'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u006b'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Hour of the day for the 24-hour clock, i.e.&nbsp;<code style="font-size: 1.2em;">0 - 23</code>.&nbsp;<code style="font-size: 1.2em;">0</code>&nbsp;corresponds to midnight.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'l'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u006c'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Hour for the 12-hour clock, i.e.&nbsp;<code style="font-size: 1.2em;">1 - 12</code>.&nbsp;<code style="font-size: 1.2em;">1</code>&nbsp;corresponds to one o'clock (either morning or afternoon).</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'M'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u004d'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Minute within the hour formatted as two digits with a leading zero as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">00 - 59</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'S'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0053'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Seconds within the minute, formatted as two digits with a leading zero as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">00 - 60</code>&nbsp;("<code style="font-size: 1.2em;">60</code>" is a special value required to support leap seconds).</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'L'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u004c'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Millisecond within the second formatted as three digits with leading zeros as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">000 - 999</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'N'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u004e'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Nanosecond within the second, formatted as nine digits with leading zeros as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">000000000 - 999999999</code>. The precision of this value is limited by the resolution of the underlying operating system or hardware.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'p'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0070'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Locale-specific&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DateFormatSymbols.html#getAmPmStrings()">morning or afternoon</a>&nbsp;marker in lower case, e.g."<code style="font-size: 1.2em;">am</code>" or "<code style="font-size: 1.2em;">pm</code>". Use of the conversion prefix&nbsp;<code style="font-size: 1.2em;">'T'</code>&nbsp;forces this output to upper case. (Note that&nbsp;<code style="font-size: 1.2em;">'p'</code>&nbsp;produces lower-case output. This is different from GNU&nbsp;<code style="font-size: 1.2em;">date</code>&nbsp;and POSIX&nbsp;<code style="font-size: 1.2em;">strftime(3c)</code>&nbsp;which produce upper-case output.)</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'z'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u007a'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;"> <a style="color: #4c6b87;" href="http://www.ietf.org/rfc/rfc0822.txt">RFC&nbsp;822</a>&nbsp;style numeric time zone offset from GMT, e.g.&nbsp;<code style="font-size: 1.2em;">-0800</code>. This value will be adjusted as necessary for Daylight Saving Time. For&nbsp;<code style="font-size: 1.2em;">long</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Long.html"><code style="font-size: 1.2em;">Long</code></a>, and&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Date.html"><code style="font-size: 1.2em;">Date</code></a>&nbsp;the time zone used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/TimeZone.html#getDefault()">default time zone</a>&nbsp;for this instance of the Java virtual machine.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'Z'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u005a'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">A string representing the abbreviation for the time zone. This value will be adjusted as necessary for Daylight Saving Time. For&nbsp;<code style="font-size: 1.2em;">long</code>,&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Long.html"><code style="font-size: 1.2em;">Long</code></a>, and&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Date.html"><code style="font-size: 1.2em;">Date</code></a>&nbsp;the time zone used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/TimeZone.html#getDefault()">default time zone</a>&nbsp;for this instance of the Java virtual machine. The Formatter's locale will supersede the locale of the argument (if any).</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'s'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0073'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Seconds since the beginning of the epoch starting at 1 January 1970&nbsp;<code style="font-size: 1.2em;">00:00:00</code>&nbsp;UTC, i.e.&nbsp;<code style="font-size: 1.2em;">Long.MIN_VALUE/1000</code>&nbsp;to&nbsp;<code style="font-size: 1.2em;">Long.MAX_VALUE/1000</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'Q'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u004f'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Milliseconds since the beginning of the epoch starting at 1 January 1970&nbsp;<code style="font-size: 1.2em;">00:00:00</code>&nbsp;UTC, i.e.&nbsp;<code style="font-size: 1.2em;">Long.MIN_VALUE</code>&nbsp;to&nbsp;<code style="font-size: 1.2em;">Long.MAX_VALUE</code>. The precision of this value is limited by the resolution of the underlying operating system or hardware.</td> 
        </tr> 
       </tbody>
      </table> 
      <p>The following conversion characters are used for formatting dates:</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="date" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'B'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0042'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Locale-specific&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DateFormatSymbols.html#getMonths()">full month name</a>, e.g.&nbsp;<code style="font-size: 1.2em;">"January"</code>,&nbsp;<code style="font-size: 1.2em;">"February"</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'b'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0062'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Locale-specific&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DateFormatSymbols.html#getShortMonths()">abbreviated month name</a>, e.g.&nbsp;<code style="font-size: 1.2em;">"Jan"</code>,&nbsp;<code style="font-size: 1.2em;">"Feb"</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'h'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0068'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Same as&nbsp;<code style="font-size: 1.2em;">'b'</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'A'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0041'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Locale-specific full name of the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DateFormatSymbols.html#getWeekdays()">day of the week</a>, e.g.&nbsp;<code style="font-size: 1.2em;">"Sunday"</code>,&nbsp;<code style="font-size: 1.2em;">"Monday"</code> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'a'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0061'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Locale-specific short name of the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/text/DateFormatSymbols.html#getShortWeekdays()">day of the week</a>, e.g.&nbsp;<code style="font-size: 1.2em;">"Sun"</code>,&nbsp;<code style="font-size: 1.2em;">"Mon"</code> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'C'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0043'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Four-digit year divided by&nbsp;<code style="font-size: 1.2em;">100</code>, formatted as two digits with leading zero as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">00 - 99</code> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'Y'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0059'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Year, formatted to at least four digits with leading zeros as necessary, e.g.&nbsp;<code style="font-size: 1.2em;">0092</code>&nbsp;equals&nbsp;<code style="font-size: 1.2em;">92</code>&nbsp;CE for the Gregorian calendar.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'y'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0079'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Last two digits of the year, formatted with leading zeros as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">00 - 99</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'j'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u006a'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Day of year, formatted as three digits with leading zeros as necessary, e.g.&nbsp;<code style="font-size: 1.2em;">001 - 366</code>&nbsp;for the Gregorian calendar.&nbsp;<code style="font-size: 1.2em;">001</code>&nbsp;corresponds to the first day of the year.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'m'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u006d'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Month, formatted as two digits with leading zeros as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">01 - 13</code>, where "<code style="font-size: 1.2em;">01</code>" is the first month of the year and ("<code style="font-size: 1.2em;">13</code>" is a special value required to support lunar calendars).</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'d'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0064'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Day of month, formatted as two digits with leading zeros as necessary, i.e.&nbsp;<code style="font-size: 1.2em;">01 - 31</code>, where "<code style="font-size: 1.2em;">01</code>" is the first day of the month.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'e'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0065'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Day of month, formatted as two digits, i.e.&nbsp;<code style="font-size: 1.2em;">1 - 31</code>&nbsp;where "<code style="font-size: 1.2em;">1</code>" is the first day of the month.</td> 
        </tr> 
       </tbody>
      </table> 
      <p>The following conversion characters are used for formatting common date/time compositions.</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="composites" cellpadding="5">
       <tbody> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'R'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0052'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Time formatted for the 24-hour clock as&nbsp;<code style="font-size: 1.2em;">"%tH:%tM"</code> </td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'T'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0054'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Time formatted for the 24-hour clock as&nbsp;<code style="font-size: 1.2em;">"%tH:%tM:%tS"</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'r'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0072'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Time formatted for the 12-hour clock as&nbsp;<code style="font-size: 1.2em;">"%tI:%tM:%tS %Tp"</code>. The location of the morning or afternoon marker (<code style="font-size: 1.2em;">'%Tp'</code>) may be locale-dependent.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'D'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0044'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Date formatted as&nbsp;<code style="font-size: 1.2em;">"%tm/%td/%ty"</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'F'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0046'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;"> <a style="color: #4c6b87;" href="http://www.w3.org/TR/NOTE-datetime">ISO&nbsp;8601</a>&nbsp;complete date formatted as&nbsp;<code style="font-size: 1.2em;">"%tY-%tm-%td"</code>.</td> 
        </tr> 
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'c'</code></td> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><tt style="font-size: 1.2em;">'\u0063'</tt></td> 
         <td style="padding: 3px 3px 3px 7px;">Date and time formatted as&nbsp;<code style="font-size: 1.2em;">"%ta %tb %td %tT %tZ %tY"</code>, e.g.&nbsp;<code style="font-size: 1.2em;">"Sun Jul 20 16:17:00 EDT 1969"</code>.</td> 
        </tr> 
       </tbody>
      </table> 
      <p>The&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;flag defined for&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#dFlags">General conversions</a>&nbsp;applies. If the&nbsp;<code style="font-size: 1.2em;">'#'</code>&nbsp;flag is given, then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> 
      <p>The&nbsp;<a style="color: #353833;" name="dtWidth"></a>width&nbsp;is the minimum number of characters to be written to the output. If the length of the converted value is less than the&nbsp;<code style="font-size: 1.2em;">width</code>&nbsp;then the output will be padded by spaces (<tt style="font-size: 1.2em;">'\u0020'</tt>) until the total number of characters equals width. The padding is on the left by default. If the&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;flag is given then the padding will be on the right. If width is not specified then there is no minimum.</p> 
      <p>The precision is not applicable. If the precision is specified then an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatPrecisionException.html"><code style="font-size: 1.2em;">IllegalFormatPrecisionException</code></a>&nbsp;will be thrown.</p> 
      <h4 style="font-size: 1.3em;"> <a style="color: #353833;" name="dper"></a>Percent</h4> 
      <p>The conversion does not correspond to any argument.</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="DTConv" cellpadding="5">
       <tbody>
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'%'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">The result is a literal&nbsp;<code style="font-size: 1.2em;">'%'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u0025'</tt>) <p>The&nbsp;<a style="color: #353833;" name="dtWidth"></a>width&nbsp;is the minimum number of characters to be written to the output including the&nbsp;<code style="font-size: 1.2em;">'%'</code>. If the length of the converted value is less than the&nbsp;<code style="font-size: 1.2em;">width</code>&nbsp;then the output will be padded by spaces (<tt style="font-size: 1.2em;">'\u0020'</tt>) until the total number of characters equals width. The padding is on the left. If width is not specified then just the&nbsp;<code style="font-size: 1.2em;">'%'</code>&nbsp;is output.</p> <p>The&nbsp;<code style="font-size: 1.2em;">'-'</code>&nbsp;flag defined for&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#dFlags">General conversions</a>&nbsp;applies. If any other flags are provided, then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatFlagsConversionMismatchException.html"><code style="font-size: 1.2em;">FormatFlagsConversionMismatchException</code></a>&nbsp;will be thrown.</p> <p>The precision is not applicable. If the precision is specified an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatPrecisionException.html"><code style="font-size: 1.2em;">IllegalFormatPrecisionException</code></a>&nbsp;will be thrown.</p> </td> 
        </tr>
       </tbody>
      </table> 
      <h4 style="font-size: 1.3em;"> <a style="color: #353833;" name="dls"></a>Line Separator</h4> 
      <p>The conversion does not correspond to any argument.</p> 
      <table style="border-bottom-style: none; width: 1863px;" summary="DTConv" cellpadding="5">
       <tbody>
        <tr> 
         <td style="padding: 3px 3px 3px 7px;" valign="top"><code style="font-size: 1.2em;">'n'</code></td> 
         <td style="padding: 3px 3px 3px 7px;">the platform-specific line separator as returned by&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/System.html#getProperty(java.lang.String)"><code style="font-size: 1.2em;">System.getProperty("line.separator")</code></a>.</td> 
        </tr>
       </tbody>
      </table> 
      <p>Flags, width, and precision are not applicable. If any are provided an&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatFlagsException.html"><code style="font-size: 1.2em;">IllegalFormatFlagsException</code></a>,&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatWidthException.html"><code style="font-size: 1.2em;">IllegalFormatWidthException</code></a>, and&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatPrecisionException.html"><code style="font-size: 1.2em;">IllegalFormatPrecisionException</code></a>, respectively will be thrown.</p> 
      <h4 style="font-size: 1.3em;"> <a style="color: #353833;" name="dpos"></a>Argument Index</h4> 
      <p>Format specifiers can reference arguments in three ways:</p> 
      <ul> 
       <li> <em>Explicit indexing</em>&nbsp;is used when the format specifier contains an argument index. The argument index is a decimal integer indicating the position of the argument in the argument list. The first argument is referenced by "<code style="font-size: 1.2em;">1$</code>", the second by "<code style="font-size: 1.2em;">2$</code>", etc. An argument may be referenced more than once. <p>For example:</p> 
        <blockquote> 
         <pre>   formatter.format("%4$s %3$s %2$s %1$s %4$s %3$s %2$s %1$s",
                    "a", "b", "c", "d")
   // -&gt; "d c b a d c b a"
 </pre> 
        </blockquote> </li> 
       <li> <em>Relative indexing</em>&nbsp;is used when the format specifier contains a&nbsp;<code style="font-size: 1.2em;">'&lt;'</code>&nbsp;(<tt style="font-size: 1.2em;">'\u003c'</tt>) flag which causes the argument for the previous format specifier to be re-used. If there is no previous argument, then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/MissingFormatArgumentException.html"><code style="font-size: 1.2em;">MissingFormatArgumentException</code></a>&nbsp;is thrown. 
        <blockquote> 
         <pre>    formatter.format("%s %s %&lt;s %&lt;s", "a", "b", "c", "d")
    // -&gt; "a b b b"
    // "c" and "d" are ignored because they are not referenced
 </pre> 
        </blockquote> </li> 
       <li> <em>Ordinary indexing</em>&nbsp;is used when the format specifier contains neither an argument index nor a&nbsp;<code style="font-size: 1.2em;">'&lt;'</code>&nbsp;flag. Each format specifier which uses ordinary indexing is assigned a sequential implicit index into argument list which is independent of the indices used by explicit or relative indexing. 
        <blockquote> 
         <pre>   formatter.format("%s %s %s %s", "a", "b", "c", "d")
   // -&gt; "a b c d"
 </pre> 
        </blockquote> </li> 
      </ul> 
      <p>It is possible to have a format string which uses all forms of indexing, for example:</p> 
      <blockquote> 
       <pre>   formatter.format("%2$s %s %&lt;s %s", "a", "b", "c", "d")
   // -&gt; "b a a b"
   // "c" and "d" are ignored because they are not referenced
 </pre> 
      </blockquote> 
      <p>The maximum number of arguments is limited by the maximum dimension of a Java array as defined by&nbsp;<cite>The Java™ Virtual Machine Specification</cite>. If the argument index is does not correspond to an available argument, then a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/MissingFormatArgumentException.html"><code style="font-size: 1.2em;">MissingFormatArgumentException</code></a>&nbsp;is thrown.</p> 
      <p>If there are more arguments than format specifiers, the extra arguments are ignored.</p> 
      <p>Unless otherwise specified, passing a&nbsp;<code style="font-size: 1.2em;">null</code>&nbsp;argument to any method or constructor in this class will cause a&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/NullPointerException.html"><code style="font-size: 1.2em;">NullPointerException</code></a>&nbsp;to be thrown.</p> 
     </div> 
     <dl> 
      <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
       <span class="strong">Since:</span>
      </dt> 
      <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;">
       1.5
      </dd> 
     </dl> </li> 
   </ul> 
  </div> 
  <div class="summary"> 
   <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
    <li class="blockList" style="margin-bottom: 25px;"> 
     <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
      <li class="blockList" style="margin-bottom: 25px; padding-right: 20px; padding-bottom: 5px; padding-left: 10px; border: 1px solid #9eadc0; background-color: #f9f9f9;"> <a style="color: #353833;" name="nested_class_summary"></a> <h3 style="font-size: 1.4em; margin-top: 15px; margin-bottom: 15px;">Nested Class Summary</h3> 
       <table class="overviewSummary" style="border-bottom-width: 1px; border-bottom-style: solid; border-bottom-color: #9eadc0; width: 1831px; padding: 0px; margin: 0px 0px 12px;" summary="Nested Class Summary table, listing nested classes, and an explanation" border="0" cellspacing="0" cellpadding="3"> 
        <caption style="text-align: left; color: #ffffff; font-weight: bold; clear: none; overflow: hidden; padding: 0px; margin: 0px;"> 
         <span>Nested Classes</span>
         <span class="tabEnd">&nbsp;</span> 
        </caption> 
        <tbody> 
         <tr> 
          <th class="colFirst" style="border-top-width: 1px; border-top-style: solid; border-top-color: #9eadc0; border-bottom-width: 1px; border-bottom-style: solid; border-bottom-color: #9eadc0; padding: 3px 20px 3px 7px; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; white-space: nowrap; width: 429px; vertical-align: top; background: #dee3e9;" scope="col">Modifier and Type</th> 
          <th class="colLast" style="border-top-width: 1px; border-top-style: solid; border-top-color: #9eadc0; border-bottom-width: 1px; border-bottom-style: solid; border-bottom-color: #9eadc0; padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; vertical-align: top; background: #dee3e9;" scope="col">Class and Description</th> 
         </tr> 
         <tr class="altColor" style="background-color: #eeeeef;"> 
          <td class="colFirst" style="padding: 3px 3px 3px 7px; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; white-space: nowrap; width: 446px; vertical-align: top;"><code style="font-size: 1.2em;">static class&nbsp;</code></td> 
          <td class="colLast" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" title="enum in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.BigDecimalLayoutForm.html">Formatter.BigDecimalLayoutForm</a></strong></code>&nbsp;</td> 
         </tr> 
        </tbody> 
       </table> </li> 
     </ul> 
     <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
      <li class="blockList" style="margin-bottom: 25px; padding-right: 20px; padding-bottom: 5px; padding-left: 10px; border: 1px solid #9eadc0; background-color: #f9f9f9;"> <a style="color: #353833;" name="constructor_summary"></a> <h3 style="font-size: 1.4em; margin-top: 15px; margin-bottom: 15px;">Constructor Summary</h3> 
       <table class="overviewSummary" style="border-bottom-width: 1px; border-bottom-style: solid; border-bottom-color: #9eadc0; width: 1831px; padding: 0px; margin: 0px 0px 12px;" summary="Constructor Summary table, listing constructors, and an explanation" border="0" cellspacing="0" cellpadding="3"> 
        <caption style="text-align: left; color: #ffffff; font-weight: bold; clear: none; overflow: hidden; padding: 0px; margin: 0px;"> 
         <span>Constructors</span>
         <span class="tabEnd">&nbsp;</span> 
        </caption> 
        <tbody> 
         <tr>
          <th class="colOne" style="border: 1px solid #9eadc0; padding: 3px 3px 3px 7px; width: 1819px; vertical-align: top; background: #dee3e9;" scope="col">Constructor and Description</th>
         </tr> 
         <tr class="altColor" style="background-color: #eeeeef;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter()">Formatter</a></strong>()</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter.
           </div> </td> 
         </tr> 
         <tr class="rowColor" style="background-color: #ffffff;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter(java.lang.Appendable)">Formatter</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="interface in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Appendable.html">Appendable</a>&nbsp;a)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter with the specified destination.
           </div> </td> 
         </tr> 
         <tr class="altColor" style="background-color: #eeeeef;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter(java.lang.Appendable,%20java.util.Locale)">Formatter</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="interface in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Appendable.html">Appendable</a>&nbsp;a,&nbsp;<a style="color: #4c6b87; font-weight: bold;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a>&nbsp;l)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter with the specified destination and locale.
           </div> </td> 
         </tr> 
         <tr class="rowColor" style="background-color: #ffffff;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter(java.io.File)">Formatter</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/File.html">File</a>&nbsp;file)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter with the specified file.
           </div> </td> 
         </tr> 
         <tr class="altColor" style="background-color: #eeeeef;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter(java.io.File,%20java.lang.String)">Formatter</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/File.html">File</a>&nbsp;file,&nbsp;<a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;csn)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter with the specified file and charset.
           </div> </td> 
         </tr> 
         <tr class="rowColor" style="background-color: #ffffff;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter(java.io.File,%20java.lang.String,%20java.util.Locale)">Formatter</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/File.html">File</a>&nbsp;file,&nbsp;<a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;csn,&nbsp;<a style="color: #4c6b87; font-weight: bold;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a>&nbsp;l)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter with the specified file, charset, and locale.
           </div> </td> 
         </tr> 
         <tr class="altColor" style="background-color: #eeeeef;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter(java.util.Locale)">Formatter</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a>&nbsp;l)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter with the specified locale.
           </div> </td> 
         </tr> 
         <tr class="rowColor" style="background-color: #ffffff;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter(java.io.OutputStream)">Formatter</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/OutputStream.html">OutputStream</a>&nbsp;os)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter with the specified output stream.
           </div> </td> 
         </tr> 
         <tr class="altColor" style="background-color: #eeeeef;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter(java.io.OutputStream,%20java.lang.String)">Formatter</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/OutputStream.html">OutputStream</a>&nbsp;os,&nbsp;<a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;csn)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter with the specified output stream and charset.
           </div> </td> 
         </tr> 
         <tr class="rowColor" style="background-color: #ffffff;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter(java.io.OutputStream,%20java.lang.String,%20java.util.Locale)">Formatter</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/OutputStream.html">OutputStream</a>&nbsp;os,&nbsp;<a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;csn,&nbsp;<a style="color: #4c6b87; font-weight: bold;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a>&nbsp;l)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter with the specified output stream, charset, and locale.
           </div> </td> 
         </tr> 
         <tr class="altColor" style="background-color: #eeeeef;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter(java.io.PrintStream)">Formatter</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/PrintStream.html">PrintStream</a>&nbsp;ps)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter with the specified print stream.
           </div> </td> 
         </tr> 
         <tr class="rowColor" style="background-color: #ffffff;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter(java.lang.String)">Formatter</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;fileName)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter with the specified file name.
           </div> </td> 
         </tr> 
         <tr class="altColor" style="background-color: #eeeeef;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter(java.lang.String,%20java.lang.String)">Formatter</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;fileName,&nbsp;<a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;csn)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter with the specified file name and charset.
           </div> </td> 
         </tr> 
         <tr class="rowColor" style="background-color: #ffffff;"> 
          <td class="colOne" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; width: 1819px; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#Formatter(java.lang.String,%20java.lang.String,%20java.util.Locale)">Formatter</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;fileName,&nbsp;<a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;csn,&nbsp;<a style="color: #4c6b87; font-weight: bold;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a>&nbsp;l)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Constructs a new formatter with the specified file name, charset, and locale.
           </div> </td> 
         </tr> 
        </tbody> 
       </table> </li> 
     </ul> 
     <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
      <li class="blockList" style="margin-bottom: 25px; padding-right: 20px; padding-bottom: 5px; padding-left: 10px; border: 1px solid #9eadc0; background-color: #f9f9f9;"> <a style="color: #353833;" name="method_summary"></a> <h3 style="font-size: 1.4em; margin-top: 15px; margin-bottom: 15px;">Method Summary</h3> 
       <table class="overviewSummary" style="border-bottom-width: 1px; border-bottom-style: solid; border-bottom-color: #9eadc0; width: 1831px; padding: 0px; margin: 0px 0px 12px;" summary="Method Summary table, listing methods, and an explanation" border="0" cellspacing="0" cellpadding="3"> 
        <caption style="text-align: left; color: #ffffff; font-weight: bold; clear: none; overflow: hidden; padding: 0px; margin: 0px;"> 
         <span>Methods</span>
         <span class="tabEnd">&nbsp;</span> 
        </caption> 
        <tbody> 
         <tr> 
          <th class="colFirst" style="border-top-width: 1px; border-top-style: solid; border-top-color: #9eadc0; border-bottom-width: 1px; border-bottom-style: solid; border-bottom-color: #9eadc0; padding: 3px 20px 3px 7px; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; white-space: nowrap; width: 429px; vertical-align: top; background: #dee3e9;" scope="col">Modifier and Type</th> 
          <th class="colLast" style="border-top-width: 1px; border-top-style: solid; border-top-color: #9eadc0; border-bottom-width: 1px; border-bottom-style: solid; border-bottom-color: #9eadc0; padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; vertical-align: top; background: #dee3e9;" scope="col">Method and Description</th> 
         </tr> 
         <tr class="altColor" style="background-color: #eeeeef;"> 
          <td class="colFirst" style="padding: 3px 3px 3px 7px; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; white-space: nowrap; width: 446px; vertical-align: top;"><code style="font-size: 1.2em;">void</code></td> 
          <td class="colLast" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#close()">close</a></strong>()</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Closes this formatter.
           </div> </td> 
         </tr> 
         <tr class="rowColor" style="background-color: #ffffff;"> 
          <td class="colFirst" style="padding: 3px 3px 3px 7px; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; white-space: nowrap; width: 446px; vertical-align: top;"><code style="font-size: 1.2em;">void</code></td> 
          <td class="colLast" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#flush()">flush</a></strong>()</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Flushes this formatter.
           </div> </td> 
         </tr> 
         <tr class="altColor" style="background-color: #eeeeef;"> 
          <td class="colFirst" style="padding: 3px 3px 3px 7px; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; white-space: nowrap; width: 446px; vertical-align: top;"><code style="font-size: 1.2em;"><a style="color: #4c6b87; font-weight: bold;" title="class in java.util">Formatter</a></code></td> 
          <td class="colLast" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#format(java.util.Locale,%20java.lang.String,%20java.lang.Object...)">format</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a>&nbsp;l,&nbsp;<a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;format,&nbsp;<a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html">Object</a>...&nbsp;args)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Writes a formatted string to this object's destination using the specified locale, format string, and arguments.
           </div> </td> 
         </tr> 
         <tr class="rowColor" style="background-color: #ffffff;"> 
          <td class="colFirst" style="padding: 3px 3px 3px 7px; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; white-space: nowrap; width: 446px; vertical-align: top;"><code style="font-size: 1.2em;"><a style="color: #4c6b87; font-weight: bold;" title="class in java.util">Formatter</a></code></td> 
          <td class="colLast" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#format(java.lang.String,%20java.lang.Object...)">format</a></strong>(<a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;format,&nbsp;<a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html">Object</a>...&nbsp;args)</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Writes a formatted string to this object's destination using the specified format string and arguments.
           </div> </td> 
         </tr> 
         <tr class="altColor" style="background-color: #eeeeef;"> 
          <td class="colFirst" style="padding: 3px 3px 3px 7px; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; white-space: nowrap; width: 446px; vertical-align: top;"><code style="font-size: 1.2em;"><a style="color: #4c6b87; font-weight: bold;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/IOException.html">IOException</a></code></td> 
          <td class="colLast" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#ioException()">ioException</a></strong>()</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Returns the&nbsp;
            <code style="font-size: 1.2em;">IOException</code>&nbsp;last thrown by this formatter's&nbsp;
            <a style="color: #4c6b87; font-weight: bold;" title="interface in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Appendable.html"><code style="font-size: 1.2em;">Appendable</code></a>.
           </div> </td> 
         </tr> 
         <tr class="rowColor" style="background-color: #ffffff;"> 
          <td class="colFirst" style="padding: 3px 3px 3px 7px; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; white-space: nowrap; width: 446px; vertical-align: top;"><code style="font-size: 1.2em;"><a style="color: #4c6b87; font-weight: bold;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a></code></td> 
          <td class="colLast" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#locale()">locale</a></strong>()</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Returns the locale set by the construction of this formatter.
           </div> </td> 
         </tr> 
         <tr class="altColor" style="background-color: #eeeeef;"> 
          <td class="colFirst" style="padding: 3px 3px 3px 7px; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; white-space: nowrap; width: 446px; vertical-align: top;"><code style="font-size: 1.2em;"><a style="color: #4c6b87; font-weight: bold;" title="interface in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Appendable.html">Appendable</a></code></td> 
          <td class="colLast" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#out()">out</a></strong>()</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Returns the destination for the output.
           </div> </td> 
         </tr> 
         <tr class="rowColor" style="background-color: #ffffff;"> 
          <td class="colFirst" style="padding: 3px 3px 3px 7px; border-left-width: 1px; border-left-style: solid; border-left-color: #9eadc0; white-space: nowrap; width: 446px; vertical-align: top;"><code style="font-size: 1.2em;"><a style="color: #4c6b87; font-weight: bold;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a></code></td> 
          <td class="colLast" style="padding: 3px 3px 3px 7px; border-right-width: 1px; border-right-style: solid; border-right-color: #9eadc0; vertical-align: top;"> <code style="font-size: 1.2em;"><strong><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#toString()">toString</a></strong>()</code> 
           <div class="block" style="margin: 3px 0px 0px;">
            Returns the result of invoking&nbsp;
            <code style="font-size: 1.2em;">toString()</code>&nbsp;on the destination for the output.
           </div> </td> 
         </tr> 
        </tbody> 
       </table> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <a style="color: #353833;" name="methods_inherited_from_class_java.lang.Object"></a> <h3>Methods inherited from class&nbsp;java.lang.<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html">Object</a> </h3> <code style="font-size: 1.2em;"><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#clone()">clone</a>,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#equals(java.lang.Object)">equals</a>,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#finalize()">finalize</a>,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#getClass()">getClass</a>,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#hashCode()">hashCode</a>,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#notify()">notify</a>,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#notifyAll()">notifyAll</a>,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#wait()">wait</a>,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#wait(long)">wait</a>,&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#wait(long,%20int)">wait</a></code> </li> 
       </ul> </li> 
     </ul> </li> 
   </ul> 
  </div> 
  <div class="details"> 
   <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
    <li class="blockList" style="margin-bottom: 25px;"> 
     <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
      <li class="blockList" style="margin-bottom: 25px; padding-right: 20px; padding-bottom: 5px; padding-left: 10px; border: 1px solid #9eadc0; background-color: #f9f9f9;"> <a style="color: #353833;" name="constructor_detail"></a> <h3 style="font-size: 1.4em; margin-top: 15px; margin-bottom: 15px;">Constructor Detail</h3> <a style="color: #353833;" name="Formatter()"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter()</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter. 
          <p>The destination of the formatted output is a&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/StringBuilder.html"><code style="font-size: 1.2em;">StringBuilder</code></a>&nbsp;which may be retrieved by invoking&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#out()"><code style="font-size: 1.2em;">out()</code></a>&nbsp;and whose current content may be converted into a string by invoking&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#toString()"><code style="font-size: 1.2em;">toString()</code></a>. The locale used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html#getDefault()">default locale</a>&nbsp;for this instance of the Java virtual machine.</p> 
         </div> </li> 
       </ul> <a style="color: #353833;" name="Formatter(java.lang.Appendable)"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter(<a style="color: #4c6b87;" title="interface in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Appendable.html">Appendable</a>&nbsp;a)</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter with the specified destination. 
          <p>The locale used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html#getDefault()">default locale</a>&nbsp;for this instance of the Java virtual machine.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">a</code>&nbsp;- Destination for the formatted output. If&nbsp;
           <code style="font-size: 1.2em;">a</code>&nbsp;is&nbsp;
           <code style="font-size: 1.2em;">null</code>&nbsp;then a&nbsp;
           <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/StringBuilder.html"><code style="font-size: 1.2em;">StringBuilder</code></a>&nbsp;will be created.
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="Formatter(java.util.Locale)"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter(<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a>&nbsp;l)</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter with the specified locale. 
          <p>The destination of the formatted output is a&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/StringBuilder.html"><code style="font-size: 1.2em;">StringBuilder</code></a>&nbsp;which may be retrieved by invoking&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#out()"><code style="font-size: 1.2em;">out()</code></a>&nbsp;and whose current content may be converted into a string by invoking&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#toString()"><code style="font-size: 1.2em;">toString()</code></a>.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">l</code>&nbsp;- The&nbsp;
           <a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">locale</a>&nbsp;to apply during formatting. If&nbsp;
           <code style="font-size: 1.2em;">l</code>&nbsp;is&nbsp;
           <code style="font-size: 1.2em;">null</code>&nbsp;then no localization is applied.
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="Formatter(java.lang.Appendable,%20java.util.Locale)"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter(<a style="color: #4c6b87;" title="interface in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Appendable.html">Appendable</a>&nbsp;a,
         <a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a>&nbsp;l)</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter with the specified destination and locale.
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">a</code>&nbsp;- Destination for the formatted output. If&nbsp;
           <code style="font-size: 1.2em;">a</code>&nbsp;is&nbsp;
           <code style="font-size: 1.2em;">null</code>&nbsp;then a&nbsp;
           <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/StringBuilder.html"><code style="font-size: 1.2em;">StringBuilder</code></a>&nbsp;will be created.
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">l</code>&nbsp;- The&nbsp;
           <a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">locale</a>&nbsp;to apply during formatting. If&nbsp;
           <code style="font-size: 1.2em;">l</code>&nbsp;is&nbsp;
           <code style="font-size: 1.2em;">null</code>&nbsp;then no localization is applied.
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="Formatter(java.lang.String)"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter(<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;fileName)
          throws <a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/FileNotFoundException.html">FileNotFoundException</a></pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter with the specified file name. 
          <p>The charset used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/nio/charset/Charset.html#defaultCharset()">default charset</a>&nbsp;for this instance of the Java virtual machine.</p> 
          <p>The locale used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html#getDefault()">default locale</a>&nbsp;for this instance of the Java virtual machine.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">fileName</code>&nbsp;- The name of the file to use as the destination of this formatter. If the file exists then it will be truncated to zero size; otherwise, a new file will be created. The output will be written to the file and is buffered.
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/SecurityException.html">SecurityException</a></code>&nbsp;- If a security manager is present and&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/SecurityManager.html#checkWrite(java.io.FileDescriptor)"><code style="font-size: 1.2em;">checkWrite(fileName)</code></a>&nbsp;denies write access to the file
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/FileNotFoundException.html">FileNotFoundException</a></code>&nbsp;- If the given file name does not denote an existing, writable regular file and a new regular file of that name cannot be created, or if some other error occurs while opening or creating the file
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="Formatter(java.lang.String,%20java.lang.String)"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter(<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;fileName,
         <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;csn)
          throws <a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/FileNotFoundException.html">FileNotFoundException</a>,
                 <a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/UnsupportedEncodingException.html">UnsupportedEncodingException</a></pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter with the specified file name and charset. 
          <p>The locale used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html#getDefault()">default locale</a>&nbsp;for this instance of the Java virtual machine.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">fileName</code>&nbsp;- The name of the file to use as the destination of this formatter. If the file exists then it will be truncated to zero size; otherwise, a new file will be created. The output will be written to the file and is buffered.
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">csn</code>&nbsp;- The name of a supported&nbsp;
           <a style="color: #4c6b87;" title="class in java.nio.charset" href="http://docs.oracle.com/javase/7/docs/api/java/nio/charset/Charset.html">charset</a> 
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/FileNotFoundException.html">FileNotFoundException</a></code>&nbsp;- If the given file name does not denote an existing, writable regular file and a new regular file of that name cannot be created, or if some other error occurs while opening or creating the file
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/SecurityException.html">SecurityException</a></code>&nbsp;- If a security manager is present and&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/SecurityManager.html#checkWrite(java.io.FileDescriptor)"><code style="font-size: 1.2em;">checkWrite(fileName)</code></a>&nbsp;denies write access to the file
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/UnsupportedEncodingException.html">UnsupportedEncodingException</a></code>&nbsp;- If the named charset is not supported
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="Formatter(java.lang.String,%20java.lang.String,%20java.util.Locale)"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter(<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;fileName,
         <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;csn,
         <a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a>&nbsp;l)
          throws <a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/FileNotFoundException.html">FileNotFoundException</a>,
                 <a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/UnsupportedEncodingException.html">UnsupportedEncodingException</a></pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter with the specified file name, charset, and locale.
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">fileName</code>&nbsp;- The name of the file to use as the destination of this formatter. If the file exists then it will be truncated to zero size; otherwise, a new file will be created. The output will be written to the file and is buffered.
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">csn</code>&nbsp;- The name of a supported&nbsp;
           <a style="color: #4c6b87;" title="class in java.nio.charset" href="http://docs.oracle.com/javase/7/docs/api/java/nio/charset/Charset.html">charset</a> 
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">l</code>&nbsp;- The&nbsp;
           <a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">locale</a>&nbsp;to apply during formatting. If&nbsp;
           <code style="font-size: 1.2em;">l</code>&nbsp;is&nbsp;
           <code style="font-size: 1.2em;">null</code>&nbsp;then no localization is applied.
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/FileNotFoundException.html">FileNotFoundException</a></code>&nbsp;- If the given file name does not denote an existing, writable regular file and a new regular file of that name cannot be created, or if some other error occurs while opening or creating the file
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/SecurityException.html">SecurityException</a></code>&nbsp;- If a security manager is present and&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/SecurityManager.html#checkWrite(java.io.FileDescriptor)"><code style="font-size: 1.2em;">checkWrite(fileName)</code></a>&nbsp;denies write access to the file
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/UnsupportedEncodingException.html">UnsupportedEncodingException</a></code>&nbsp;- If the named charset is not supported
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="Formatter(java.io.File)"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter(<a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/File.html">File</a>&nbsp;file)
          throws <a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/FileNotFoundException.html">FileNotFoundException</a></pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter with the specified file. 
          <p>The charset used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/nio/charset/Charset.html#defaultCharset()">default charset</a>&nbsp;for this instance of the Java virtual machine.</p> 
          <p>The locale used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html#getDefault()">default locale</a>&nbsp;for this instance of the Java virtual machine.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">file</code>&nbsp;- The file to use as the destination of this formatter. If the file exists then it will be truncated to zero size; otherwise, a new file will be created. The output will be written to the file and is buffered.
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/SecurityException.html">SecurityException</a></code>&nbsp;- If a security manager is present and&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/SecurityManager.html#checkWrite(java.io.FileDescriptor)"><code style="font-size: 1.2em;">checkWrite(file.getPath())</code></a>&nbsp;denies write access to the file
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/FileNotFoundException.html">FileNotFoundException</a></code>&nbsp;- If the given file object does not denote an existing, writable regular file and a new regular file of that name cannot be created, or if some other error occurs while opening or creating the file
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="Formatter(java.io.File,%20java.lang.String)"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter(<a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/File.html">File</a>&nbsp;file,
         <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;csn)
          throws <a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/FileNotFoundException.html">FileNotFoundException</a>,
                 <a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/UnsupportedEncodingException.html">UnsupportedEncodingException</a></pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter with the specified file and charset. 
          <p>The locale used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html#getDefault()">default locale</a>&nbsp;for this instance of the Java virtual machine.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">file</code>&nbsp;- The file to use as the destination of this formatter. If the file exists then it will be truncated to zero size; otherwise, a new file will be created. The output will be written to the file and is buffered.
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">csn</code>&nbsp;- The name of a supported&nbsp;
           <a style="color: #4c6b87;" title="class in java.nio.charset" href="http://docs.oracle.com/javase/7/docs/api/java/nio/charset/Charset.html">charset</a> 
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/FileNotFoundException.html">FileNotFoundException</a></code>&nbsp;- If the given file object does not denote an existing, writable regular file and a new regular file of that name cannot be created, or if some other error occurs while opening or creating the file
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/SecurityException.html">SecurityException</a></code>&nbsp;- If a security manager is present and&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/SecurityManager.html#checkWrite(java.io.FileDescriptor)"><code style="font-size: 1.2em;">checkWrite(file.getPath())</code></a>&nbsp;denies write access to the file
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/UnsupportedEncodingException.html">UnsupportedEncodingException</a></code>&nbsp;- If the named charset is not supported
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="Formatter(java.io.File,%20java.lang.String,%20java.util.Locale)"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter(<a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/File.html">File</a>&nbsp;file,
         <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;csn,
         <a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a>&nbsp;l)
          throws <a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/FileNotFoundException.html">FileNotFoundException</a>,
                 <a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/UnsupportedEncodingException.html">UnsupportedEncodingException</a></pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter with the specified file, charset, and locale.
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">file</code>&nbsp;- The file to use as the destination of this formatter. If the file exists then it will be truncated to zero size; otherwise, a new file will be created. The output will be written to the file and is buffered.
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">csn</code>&nbsp;- The name of a supported&nbsp;
           <a style="color: #4c6b87;" title="class in java.nio.charset" href="http://docs.oracle.com/javase/7/docs/api/java/nio/charset/Charset.html">charset</a> 
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">l</code>&nbsp;- The&nbsp;
           <a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">locale</a>&nbsp;to apply during formatting. If&nbsp;
           <code style="font-size: 1.2em;">l</code>&nbsp;is&nbsp;
           <code style="font-size: 1.2em;">null</code>&nbsp;then no localization is applied.
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/FileNotFoundException.html">FileNotFoundException</a></code>&nbsp;- If the given file object does not denote an existing, writable regular file and a new regular file of that name cannot be created, or if some other error occurs while opening or creating the file
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/SecurityException.html">SecurityException</a></code>&nbsp;- If a security manager is present and&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/SecurityManager.html#checkWrite(java.io.FileDescriptor)"><code style="font-size: 1.2em;">checkWrite(file.getPath())</code></a>&nbsp;denies write access to the file
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/UnsupportedEncodingException.html">UnsupportedEncodingException</a></code>&nbsp;- If the named charset is not supported
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="Formatter(java.io.PrintStream)"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter(<a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/PrintStream.html">PrintStream</a>&nbsp;ps)</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter with the specified print stream. 
          <p>The locale used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html#getDefault()">default locale</a>&nbsp;for this instance of the Java virtual machine.</p> 
          <p>Characters are written to the given&nbsp;<a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/PrintStream.html"><code style="font-size: 1.2em;">PrintStream</code></a>&nbsp;object and are therefore encoded using that object's charset.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">ps</code>&nbsp;- The stream to use as the destination of this formatter.
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="Formatter(java.io.OutputStream)"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter(<a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/OutputStream.html">OutputStream</a>&nbsp;os)</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter with the specified output stream. 
          <p>The charset used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/nio/charset/Charset.html#defaultCharset()">default charset</a>&nbsp;for this instance of the Java virtual machine.</p> 
          <p>The locale used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html#getDefault()">default locale</a>&nbsp;for this instance of the Java virtual machine.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">os</code>&nbsp;- The output stream to use as the destination of this formatter. The output will be buffered.
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="Formatter(java.io.OutputStream,%20java.lang.String)"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter(<a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/OutputStream.html">OutputStream</a>&nbsp;os,
         <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;csn)
          throws <a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/UnsupportedEncodingException.html">UnsupportedEncodingException</a></pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter with the specified output stream and charset. 
          <p>The locale used is the&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html#getDefault()">default locale</a>&nbsp;for this instance of the Java virtual machine.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">os</code>&nbsp;- The output stream to use as the destination of this formatter. The output will be buffered.
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">csn</code>&nbsp;- The name of a supported&nbsp;
           <a style="color: #4c6b87;" title="class in java.nio.charset" href="http://docs.oracle.com/javase/7/docs/api/java/nio/charset/Charset.html">charset</a> 
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/UnsupportedEncodingException.html">UnsupportedEncodingException</a></code>&nbsp;- If the named charset is not supported
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="Formatter(java.io.OutputStream,%20java.lang.String,%20java.util.Locale)"></a> 
       <ul class="blockListLast" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>Formatter</h4> <pre>public&nbsp;Formatter(<a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/OutputStream.html">OutputStream</a>&nbsp;os,
         <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;csn,
         <a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a>&nbsp;l)
          throws <a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/UnsupportedEncodingException.html">UnsupportedEncodingException</a></pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Constructs a new formatter with the specified output stream, charset, and locale.
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">os</code>&nbsp;- The output stream to use as the destination of this formatter. The output will be buffered.
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">csn</code>&nbsp;- The name of a supported&nbsp;
           <a style="color: #4c6b87;" title="class in java.nio.charset" href="http://docs.oracle.com/javase/7/docs/api/java/nio/charset/Charset.html">charset</a> 
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">l</code>&nbsp;- The&nbsp;
           <a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">locale</a>&nbsp;to apply during formatting. If&nbsp;
           <code style="font-size: 1.2em;">l</code>&nbsp;is&nbsp;
           <code style="font-size: 1.2em;">null</code>&nbsp;then no localization is applied.
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/UnsupportedEncodingException.html">UnsupportedEncodingException</a></code>&nbsp;- If the named charset is not supported
          </dd> 
         </dl> </li> 
       </ul> </li> 
     </ul> 
     <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
      <li class="blockList" style="margin-bottom: 25px; padding-right: 20px; padding-bottom: 5px; padding-left: 10px; border: 1px solid #9eadc0; background-color: #f9f9f9;"> <a style="color: #353833;" name="method_detail"></a> <h3 style="font-size: 1.4em; margin-top: 15px; margin-bottom: 15px;">Method Detail</h3> <a style="color: #353833;" name="locale()"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>locale</h4> <pre>public&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a>&nbsp;locale()</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Returns the locale set by the construction of this formatter. 
          <p>The&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#format(java.util.Locale,%20java.lang.String,%20java.lang.Object...)"><code style="font-size: 1.2em;">format</code></a>&nbsp;method for this object which has a locale argument does not change this value.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Returns:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">null</code>&nbsp;if no localization is applied, otherwise a locale
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatterClosedException.html">FormatterClosedException</a></code>&nbsp;- If this formatter has been closed by invoking its&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#close()"><code style="font-size: 1.2em;">close()</code></a>&nbsp;method
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="out()"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>out</h4> <pre>public&nbsp;<a style="color: #4c6b87;" title="interface in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Appendable.html">Appendable</a>&nbsp;out()</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Returns the destination for the output.
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Returns:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;">
           The destination for the output
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatterClosedException.html">FormatterClosedException</a></code>&nbsp;- If this formatter has been closed by invoking its&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#close()"><code style="font-size: 1.2em;">close()</code></a>&nbsp;method
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="toString()"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>toString</h4> <pre>public&nbsp;<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;toString()</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Returns the result of invoking&nbsp;
          <code style="font-size: 1.2em;">toString()</code>&nbsp;on the destination for the output. For example, the following code formats text into a&nbsp;
          <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/StringBuilder.html"><code style="font-size: 1.2em;">StringBuilder</code></a>&nbsp;then retrieves the resultant string: 
          <blockquote> 
           <pre>   Formatter f = new Formatter();
   f.format("Last reboot at %tc", lastRebootDate);
   String s = f.toString();
   // -&gt; s == "Last reboot at Sat Jan 01 00:00:00 PST 2000"
 </pre> 
          </blockquote> 
          <p>An invocation of this method behaves in exactly the same way as the invocation</p> 
          <pre>     out().toString() </pre> 
          <p>Depending on the specification of&nbsp;<code style="font-size: 1.2em;">toString</code>&nbsp;for the&nbsp;<a style="color: #4c6b87;" title="interface in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Appendable.html"><code style="font-size: 1.2em;">Appendable</code></a>, the returned string may or may not contain the characters written to the destination. For instance, buffers typically return their contents in&nbsp;<code style="font-size: 1.2em;">toString()</code>, but streams cannot since the data is discarded.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <strong>Overrides:</strong>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#toString()">toString</a></code>&nbsp;in class&nbsp;
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html">Object</a></code> 
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Returns:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;">
           The result of invoking&nbsp;
           <code style="font-size: 1.2em;">toString()</code>&nbsp;on the destination for the output
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatterClosedException.html">FormatterClosedException</a></code>&nbsp;- If this formatter has been closed by invoking its&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#close()"><code style="font-size: 1.2em;">close()</code></a>&nbsp;method
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="flush()"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>flush</h4> <pre>public&nbsp;void&nbsp;flush()</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Flushes this formatter. If the destination implements the&nbsp;
          <a style="color: #4c6b87;" title="interface in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/Flushable.html"><code style="font-size: 1.2em;">Flushable</code></a>&nbsp;interface, its&nbsp;
          <code style="font-size: 1.2em;">flush</code>&nbsp;method will be invoked. 
          <p>Flushing a formatter writes any buffered output in the destination to the underlying stream.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <strong>Specified by:</strong>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/io/Flushable.html#flush()">flush</a></code>&nbsp;in interface&nbsp;
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="interface in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/Flushable.html">Flushable</a></code> 
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatterClosedException.html">FormatterClosedException</a></code>&nbsp;- If this formatter has been closed by invoking its&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#close()"><code style="font-size: 1.2em;">close()</code></a>&nbsp;method
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="close()"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>close</h4> <pre>public&nbsp;void&nbsp;close()</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Closes this formatter. If the destination implements the&nbsp;
          <a style="color: #4c6b87;" title="interface in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/Closeable.html"><code style="font-size: 1.2em;">Closeable</code></a>&nbsp;interface, its&nbsp;
          <code style="font-size: 1.2em;">close</code>&nbsp;method will be invoked. 
          <p>Closing a formatter allows it to release resources it may be holding (such as open files). If the formatter is already closed, then invoking this method has no effect.</p> 
          <p>Attempting to invoke any methods except&nbsp;<a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#ioException()"><code style="font-size: 1.2em;">ioException()</code></a>&nbsp;in this formatter after it has been closed will result in a&nbsp;<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatterClosedException.html"><code style="font-size: 1.2em;">FormatterClosedException</code></a>.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <strong>Specified by:</strong>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/io/Closeable.html#close()">close</a></code>&nbsp;in interface&nbsp;
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="interface in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/Closeable.html">Closeable</a></code> 
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <strong>Specified by:</strong>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/lang/AutoCloseable.html#close()">close</a></code>&nbsp;in interface&nbsp;
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="interface in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/AutoCloseable.html">AutoCloseable</a></code> 
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="ioException()"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>ioException</h4> <pre>public&nbsp;<a style="color: #4c6b87;" title="class in java.io" href="http://docs.oracle.com/javase/7/docs/api/java/io/IOException.html">IOException</a>&nbsp;ioException()</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Returns the&nbsp;
          <code style="font-size: 1.2em;">IOException</code>&nbsp;last thrown by this formatter's&nbsp;
          <a style="color: #4c6b87;" title="interface in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Appendable.html"><code style="font-size: 1.2em;">Appendable</code></a>. 
          <p>If the destination's&nbsp;<code style="font-size: 1.2em;">append()</code>&nbsp;method never throws&nbsp;<code style="font-size: 1.2em;">IOException</code>, then this method will always return&nbsp;<code style="font-size: 1.2em;">null</code>.</p> 
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Returns:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;">
           The last exception thrown by the Appendable or&nbsp;
           <code style="font-size: 1.2em;">null</code>&nbsp;if no such exception exists.
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="format(java.lang.String,%20java.lang.Object...)"></a> 
       <ul class="blockList" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>format</h4> <pre>public&nbsp;<a style="color: #4c6b87;" title="class in java.util">Formatter</a>&nbsp;format(<a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;format,
               <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html">Object</a>...&nbsp;args)</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Writes a formatted string to this object's destination using the specified format string and arguments. The locale used is the one defined during the construction of this formatter.
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">format</code>&nbsp;- A format string as described in&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#syntax">Format string syntax</a>.
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">args</code>&nbsp;- Arguments referenced by the format specifiers in the format string. If there are more arguments than format specifiers, the extra arguments are ignored. The maximum number of arguments is limited by the maximum dimension of a Java array as defined by&nbsp;
           <cite>The Java™ Virtual Machine Specification</cite>.
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Returns:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;">
           This formatter
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatException.html">IllegalFormatException</a></code>&nbsp;- If a format string contains an illegal syntax, a format specifier that is incompatible with the given arguments, insufficient arguments given the format string, or other illegal conditions. For specification of all possible formatting errors, see the&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#detail">Details</a>&nbsp;section of the formatter class specification.
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatterClosedException.html">FormatterClosedException</a></code>&nbsp;- If this formatter has been closed by invoking its&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#close()"><code style="font-size: 1.2em;">close()</code></a>&nbsp;method
          </dd> 
         </dl> </li> 
       </ul> <a style="color: #353833;" name="format(java.util.Locale,%20java.lang.String,%20java.lang.Object...)"></a> 
       <ul class="blockListLast" style="margin-top: 10px; margin-bottom: 10px;"> 
        <li class="blockList" style="margin-bottom: 25px; padding-bottom: 5px; padding-left: 8px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-style: none solid solid; border-right-color: #9eadc0; border-bottom-color: #9eadc0; border-left-color: #9eadc0; background-color: #ffffff;"> <h4>format</h4> <pre>public&nbsp;<a style="color: #4c6b87;" title="class in java.util">Formatter</a>&nbsp;format(<a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">Locale</a>&nbsp;l,
               <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/String.html">String</a>&nbsp;format,
               <a style="color: #4c6b87;" title="class in java.lang" href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html">Object</a>...&nbsp;args)</pre> 
         <div class="block" style="margin: 3px 0px 0px;">
          Writes a formatted string to this object's destination using the specified locale, format string, and arguments.
         </div> 
         <dl> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Parameters:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">l</code>&nbsp;- The&nbsp;
           <a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html">locale</a>&nbsp;to apply during formatting. If&nbsp;
           <code style="font-size: 1.2em;">l</code>&nbsp;is&nbsp;
           <code style="font-size: 1.2em;">null</code>&nbsp;then no localization is applied. This does not change this object's locale that was set during construction.
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">format</code>&nbsp;- A format string as described in&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#syntax">Format string syntax</a> 
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;">args</code>&nbsp;- Arguments referenced by the format specifiers in the format string. If there are more arguments than format specifiers, the extra arguments are ignored. The maximum number of arguments is limited by the maximum dimension of a Java array as defined by&nbsp;
           <cite>The Java™ Virtual Machine Specification</cite>.
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Returns:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;">
           This formatter
          </dd> 
          <dt style="font-size: 1.1em; font-weight: bold; margin-top: 10px; margin-bottom: 0px; color: #4e4e4e;">
           <span class="strong">Throws:</span>
          </dt> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/IllegalFormatException.html">IllegalFormatException</a></code>&nbsp;- If a format string contains an illegal syntax, a format specifier that is incompatible with the given arguments, insufficient arguments given the format string, or other illegal conditions. For specification of all possible formatting errors, see the&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#detail">Details</a>&nbsp;section of the formatter class specification.
          </dd> 
          <dd style="margin-top: 10px; margin-bottom: 10px; margin-left: 20px;"> 
           <code style="font-size: 1.2em;"><a style="color: #4c6b87;" title="class in java.util" href="http://docs.oracle.com/javase/7/docs/api/java/util/FormatterClosedException.html">FormatterClosedException</a></code>&nbsp;- If this formatter has been closed by invoking its&nbsp;
           <a style="color: #4c6b87;" href="http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#close()"><code style="font-size: 1.2em;">close()</code></a>&nbsp;method
          </dd> 
         </dl> </li> 
       </ul> </li> 
     </ul> </li> 
   </ul> 
  </div> 
 </div> 
 <div class="bottomNav"> 
  <a style="color: #353833; font-family: Arial, Helvetica, sans-serif; font-size: 12px; line-height: normal;" name="navbar_bottom"></a>
  <a style="color: #353833; font-family: Arial, Helvetica, sans-serif; font-size: 12px; line-height: normal;" name="navbar_bottom_firstrow"></a> 
 </div> 
</div>