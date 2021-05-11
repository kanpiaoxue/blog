#Java String Format Examples
###发表时间：2021-02-22
###分类：经验,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2519248" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2519248</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考资料地址：<a href="https://dzone.com/articles/java-string-format-examples">&nbsp;</a></p> 
 <p>文章地址：&nbsp;<a href="https://dzone.com/articles/java-string-format-examples">https://dzone.com/articles/java-string-format-examples</a></p> 
 <p>jdk API地址：&nbsp;<a href="https://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html">https://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Have you tried to read and understand Java’s String&nbsp;<a style="color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html" rel="nofollow" target="_blank">format documentation</a>? I have and found it nearly impenetrable. While it does include all the information, the organization leaves something to be desired.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">This guide is an attempt to bring some clarity and ease the usage of string formatting in Java.</p> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">String Formatting</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The most common way of formatting a string in java is using&nbsp;<em style=""><a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#format-java.lang.String-java.lang.Object...-" target="_blank">String.format()</a></em>. If there were a “java sprintf” then this would be it.</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 412.797px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable" style="">output</span> <span class="cm-operator" style="">=</span> <span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"%s = %d"</span>, <span class="cm-string" style="color: #aa1111;">"joe"</span>, <span class="cm-number" style="color: #116644;">35</span>);</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">For formatted console output, you can use&nbsp;<em style=""><a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/io/PrintStream.html#printf-java.lang.String-java.lang.Object...-" rel="nofollow" target="_blank">printf()</a></em>&nbsp;or the&nbsp;<em style=""><a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/io/PrintStream.html#format-java.lang.String-java.lang.Object...-" rel="nofollow" target="_blank">format()</a></em>&nbsp;method of&nbsp;<em style=""><a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#out" rel="nofollow" target="_blank">System.out</a></em>&nbsp;and&nbsp;<em style=""><a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#err" rel="nofollow" target="_blank">System.err</a></em>&nbsp;PrintStreams.</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 358.141px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">System</span>.<span class="cm-variable" style="">out</span>.<span class="cm-variable" style="">printf</span>(<span class="cm-string" style="color: #aa1111;">"My name is: %s%n"</span>, <span class="cm-string" style="color: #aa1111;">"joe"</span>);</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Create a&nbsp;<em style=""><a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html" rel="nofollow" target="_blank">Formatter&nbsp;</a></em>and link it to a&nbsp;<em style=""><a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html" rel="nofollow" target="_blank">StringBuilder</a></em>.&nbsp;Output formatted using the&nbsp;<em style=""><a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html#format-java.lang.String-java.lang.Object...-" rel="nofollow" target="_blank">format()</a></em>&nbsp;method will be appended to the&nbsp;<em style="">StringBuilder</em>.</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 381.469px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">StringBuilder</span> <span class="cm-variable" style="">sbuf</span> <span class="cm-operator" style="">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-type" style="color: #008855;">StringBuilder</span>();</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">Formatter</span> <span class="cm-variable" style="">fmt</span> <span class="cm-operator" style="">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Formatter</span>(<span class="cm-variable" style="">sbuf</span>);</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">fmt</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"PI = %f%n"</span>, <span class="cm-variable" style="">Math</span>.<span class="cm-variable" style="">PI</span>);</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">System</span>.<span class="cm-variable" style="">out</span>.<span class="cm-variable" style="">print</span>(<span class="cm-variable" style="">sbuf</span>.<span class="cm-variable" style="">toString</span>());</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-comment" style="color: #aa5500;">// you can continue to append data to sbuf here.</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 128px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">Format Specifiers</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Here is a quick reference to&nbsp;all the&nbsp;conversion specifiers supported:</p> 
 <table style="border-collapse: collapse; border-spacing: 0px; width: 853px; margin-bottom: 10px; margin-top: 10px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; display: block; color: #222635; font-size: 19px;"> 
  <thead style="color: #ffffff; letter-spacing: 1px; font-size: 15px; font-weight: 600; background-color: #ff843d !important;">
   <tr style=""> 
    <td style="padding: 5px 10px; border: 1px solid #d9dcdd; font-size: 14px;">SPECIFIER</td> 
    <td style="padding: 5px 10px; border: 1px solid #d9dcdd; font-size: 14px;">APPLIES TO</td> 
    <td style="padding: 5px 10px; border: 1px solid #d9dcdd; font-size: 14px;">OUTPUT</td> 
   </tr>
  </thead> 
  <tbody style=""> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%a</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">floating point (except&nbsp;<em style=""><a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/math/BigDecimal.html" target="_blank">BigDecimal</a></em>)</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Hex output of floating point number</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%b</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Any type</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">“true” if non-null, “false” if null</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%c</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">character</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Unicode character</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%d</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">integer (incl. byte, short, int, long, bigint)</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Decimal Integer</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%e</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">floating point</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">decimal number in scientific notation</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%f</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">floating point</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">decimal number</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%g</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">floating point</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">decimal number, possibly in scientific notation depending on the precision and value.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%h</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">any type</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Hex String of value from hashCode() method.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">&nbsp;%n</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">none</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Platform-specific line separator.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%o</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">integer (incl. byte, short, int, long, bigint)</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Octal number</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%s</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">any type</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">String value</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%t</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Date/Time (incl. long, Calendar, Date and TemporalAccessor)</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%t is the prefix for Date/Time conversions. More formatting flags are needed after this. See Date/Time conversion below.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%x</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">integer (incl. byte, short, int, long, bigint)</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;"> <p style="margin-top: 5px; margin-bottom: 15px;">Hex string.</p> </td> 
   </tr> 
  </tbody> 
 </table> 
 <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Date and Time Formatting</h3> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Note: Using the formatting characters with “%T” instead of “%t” in the table below makes the output uppercase.</p> 
 <table style="border-collapse: collapse; border-spacing: 0px; width: 853px; margin-bottom: 10px; margin-top: 10px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; display: block; color: #222635; font-size: 19px;"> 
  <thead style="color: #ffffff; letter-spacing: 1px; font-size: 15px; font-weight: 600; background-color: #ff843d !important;">
   <tr style=""> 
    <td style="padding: 5px 10px; border: 1px solid #d9dcdd; font-size: 14px;" width="15%">&nbsp;FLAG</td> 
    <td style="padding: 5px 10px; border: 1px solid #d9dcdd; font-size: 14px;">NOTES</td> 
   </tr>
  </thead> 
  <tbody style=""> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">&nbsp;%tA</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Full name of the day of the week, e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Sunday</code>“, “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Monday</code>“</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">&nbsp;%ta</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Abbreviated name of the week day e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Sun</code>“, “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Mon</code>“, etc.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">&nbsp;%tB</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Full name of the month e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">January</code>“, “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">February</code>“, etc.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">&nbsp;%tb</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Abbreviated month name e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Jan</code>“, “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Feb</code>“, etc.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">&nbsp;%tC</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Century part of year formatted with two digits e.g. “00” through “99”.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">&nbsp;%tc</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Date and time formatted with “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">%ta %tb %td %tT %tZ %tY</code>” e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Fri Feb 17 07:45:42 PST 2017</code>“</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">&nbsp;%tD</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Date formatted as “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">%tm/%td/%ty</code>“</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">&nbsp;%td</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Day of the month formatted with two digits. e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">01</code>” to “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">31</code>“.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">&nbsp;%te</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Day of the month formatted without a leading 0 e.g. “1” to “31”.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tF</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">ISO 8601 formatted date with “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">%tY-%tm-%td</code>“.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tH</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Hour of the day for the 24-hour clock e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">00</code>” to “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">23</code>“.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%th</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Same as %tb.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tI</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Hour of the day for the 12-hour clock e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">01</code>” – “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">12</code>“.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tj</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Day of the year formatted with leading 0s e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">001</code>” to “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">366</code>“.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tk</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Hour of the day for the 24 hour clock without a leading 0 e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">0</code>” to “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">23</code>“.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tl</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Hour of the day for the 12-hour click without a leading 0 e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">1</code>” to “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">12</code>“.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tM</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Minute within the hour formatted a leading 0 e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">00</code>” to “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">59</code>“.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tm</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Month formatted with a leading 0 e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">01</code>” to “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">12</code>“.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tN</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Nanosecond formatted with 9 digits and leading 0s e.g. “000000000” to “999999999”.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tp</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Locale specific “am” or “pm” marker.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tQ</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Milliseconds since epoch Jan 1 , 1970 00:00:00 UTC.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tR</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Time formatted as 24-hours e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">%tH:%tM</code>“.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tr</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Time formatted as 12-hours e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">%tI:%tM:%tS %Tp</code>“.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tS</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Seconds within the minute formatted with 2 digits e.g. “00” to “60”. “60” is required to support leap seconds.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%ts</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Seconds since the epoch Jan 1, 1970 00:00:00 UTC.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tT</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Time formatted as 24-hours e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">%tH:%tM:%tS</code>“.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tY</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Year formatted with 4 digits e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">0000</code>” to “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">9999</code>“.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%ty</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Year formatted with 2 digits e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">00</code>” to “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">99</code>“.</td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tZ</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">Time zone abbreviation. e.g. “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">UTC</code>“, “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">PST</code>“, etc.</td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;">%tz</td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;"> <p style="margin-top: 5px; margin-bottom: 15px;">Time Zone Offset from GMT e.g. “</p> <code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">-0800</code> <p style="margin-top: 5px; margin-bottom: 15px;">“.</p> </td> 
   </tr> 
  </tbody> 
 </table> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">Argument Index</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">An argument index is specified as a number ending with a “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">$</code>” after the “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">%</code>” and selects the specified argument in the argument list.</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 428.344px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"%2$s"</span>, <span class="cm-number" style="color: #116644;">32</span>, <span class="cm-string" style="color: #aa1111;">"Hello"</span>); <span class="cm-comment" style="color: #aa5500;">// prints: "Hello"</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">Formatting an Integer</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">With the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">%d</code>&nbsp;format specifier, you can use an argument of all integral types including byte, short, int, long and BigInteger.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Default formatting:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 295.719px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"%d"</span>, <span class="cm-number" style="color: #116644;">93</span>); <span class="cm-comment" style="color: #aa5500;">// prints 93</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Specifying a width:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 498.547px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%20d|"</span>, <span class="cm-number" style="color: #116644;">93</span>); <span class="cm-comment" style="color: #aa5500;">// prints: |                  93| </span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Left-justifying within the specified width:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 498.547px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%-20d|"</span>, <span class="cm-number" style="color: #116644;">93</span>); <span class="cm-comment" style="color: #aa5500;">// prints: |93                  |</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Pad with zeros:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 498.547px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%020d|"</span>, <span class="cm-number" style="color: #116644;">93</span>); <span class="cm-comment" style="color: #aa5500;">// prints: |00000000000000000093|</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Print positive numbers with a “+”:</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;"><em style="">(Negative numbers always have the “-” included):</em></p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 498.516px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%+20d|', 93); // prints: |                 +93|</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">A&nbsp;space before positive numbers.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">A “-” is included for negative numbers as per normal.</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 709.172px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|% d|"</span>, <span class="cm-number" style="color: #116644;">93</span>); <span class="cm-comment" style="color: #aa5500;">// prints: | 93| String.format("|% d|", -36); // prints: |-36|</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Use locale-specific thousands separator:</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">For the US locale, it is “,”:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 451.734px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%,d|"</span>, <span class="cm-number" style="color: #116644;">10000000</span>); <span class="cm-comment" style="color: #aa5500;">// prints: |10,000,000|</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Enclose negative numbers within parentheses (“()”) and skip the "-":</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 365.922px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%(d|"</span>, <span class="cm-operator" style="">-</span><span class="cm-number" style="color: #116644;">36</span>); <span class="cm-comment" style="color: #aa5500;">// prints: |(36)|</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Octal output:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 334.703px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%o|"</span>), <span class="cm-number" style="color: #116644;">93</span>); <span class="cm-comment" style="color: #aa5500;">// prints: 135</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Hex output:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 319.109px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%x|"</span>, <span class="cm-number" style="color: #116644;">93</span>); <span class="cm-comment" style="color: #aa5500;">// prints: 5d</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Alternate representation for octal and hex output:</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Prints octal numbers with a leading “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">0</code>” and hex numbers with leading “<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">0x</code>“.</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 217.688px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%#o|"</span>, <span class="cm-number" style="color: #116644;">93</span>);</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-comment" style="color: #aa5500;">// prints: 0135</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span style="">​</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%#x|"</span>, <span class="cm-number" style="color: #116644;">93</span>);</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-comment" style="color: #aa5500;">// prints: 0x5d</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span style="">​</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%#X|"</span>, <span class="cm-number" style="color: #116644;">93</span>);</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-comment" style="color: #aa5500;">// prints: 0X5D</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 182px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">String and Character Conversion</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Default formatting:</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Prints the whole string.</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 490.734px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%s|"</span>, <span class="cm-string" style="color: #aa1111;">"Hello World"</span>); <span class="cm-comment" style="color: #aa5500;">// prints: "Hello World"</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Specify Field Length</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 514.156px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%30s|"</span>, <span class="cm-string" style="color: #aa1111;">"Hello World"</span>); <span class="cm-comment" style="color: #aa5500;">// prints: | Hello World|</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Left Justify Text</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 521.953px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%-30s|"</span>, <span class="cm-string" style="color: #aa1111;">"Hello World"</span>); <span class="cm-comment" style="color: #aa5500;">// prints: |Hello World |</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Specify Maximum Number of Characters</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 459.547px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%.5s|"</span>, <span class="cm-string" style="color: #aa1111;">"Hello World"</span>); <span class="cm-comment" style="color: #aa5500;">// prints: |Hello|</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Field Width and Maximum Number of Characters</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 397.156px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">format</span>(<span class="cm-string" style="color: #aa1111;">"|%30.5s|"</span>, <span class="cm-string" style="color: #aa1111;">"Hello World"</span>); <span class="cm-operator" style="">|</span> <span class="cm-variable" style="">Hello</span><span class="cm-operator" style="">|</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">Summary</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">This guide explained String formatting in Java. We covered the supported format specifiers. Both numeric and string formatting support a variety of flags for alternative formats. If you want more content on Java Strings, check out the&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://dzone.com/articles/the-dos-and-donts-of-java-strings" target="_blank">Do's and Don'ts of Java Strings</a>.</p> 
 <p>&nbsp;</p> 
</div>