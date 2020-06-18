#python2的datetime格式化
###发表时间：2020-06-03
###分类：python,DateTime,pydatetime,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2514547" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2514547</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>官网地址：&nbsp;<a href="https://docs.python.org/2/library/datetime.html#strftime-and-strptime-behavior">https://docs.python.org/2/library/datetime.html#strftime-and-strptime-behavior</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <h2 style=""> <span class="section-number">8.1.7.&nbsp;</span><code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">strftime()</span></code>&nbsp;and&nbsp;<code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">strptime()</span></code>&nbsp;Behavior</h2> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;"><a class="reference internal" style="color: #355f7c;" title="datetime.date" href="https://docs.python.org/2/library/datetime.html#datetime.date"><code class="xref py py-class docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">date</span></code></a>,&nbsp;<a class="reference internal" style="color: #355f7c;" title="datetime.datetime" href="https://docs.python.org/2/library/datetime.html#datetime.datetime"><code class="xref py py-class docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">datetime</span></code></a>, and&nbsp;<a class="reference internal" style="color: #355f7c;" title="datetime.time" href="https://docs.python.org/2/library/datetime.html#datetime.time"><code class="xref py py-class docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">time</span></code></a>&nbsp;objects all support a&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">strftime(format)</span></code>&nbsp;method, to create a string representing the time under the control of an explicit format string. Broadly speaking,&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">d.strftime(fmt)</span></code>&nbsp;acts like the&nbsp;<a class="reference internal" style="color: #355f7c;" title="time: Time access and conversions." href="https://docs.python.org/2/library/time.html#module-time"><code class="xref py py-mod docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">time</span></code></a>&nbsp;module’s&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">time.strftime(fmt,</span>&nbsp;<span class="pre">d.timetuple())</span></code>&nbsp;although not all objects support a&nbsp;<code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">timetuple()</span></code>&nbsp;method.</p> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">Conversely, the&nbsp;<a class="reference internal" style="color: #355f7c;" title="datetime.datetime.strptime" href="https://docs.python.org/2/library/datetime.html#datetime.datetime.strptime"><code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">datetime.strptime()</span></code></a>&nbsp;class method creates a&nbsp;<a class="reference internal" style="color: #355f7c;" title="datetime.datetime" href="https://docs.python.org/2/library/datetime.html#datetime.datetime"><code class="xref py py-class docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">datetime</span></code></a>&nbsp;object from a string representing a date and time and a corresponding format string.&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">datetime.strptime(date_string,</span>&nbsp;<span class="pre">format)</span></code>&nbsp;is equivalent to&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">datetime(*(time.strptime(date_string,</span>&nbsp;<span class="pre">format)[0:6]))</span></code>, except when the format includes sub-second components or timezone offset information, which are supported in&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">datetime.strptime</span></code>&nbsp;but are discarded by&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">time.strptime</span></code>.</p> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">For&nbsp;<a class="reference internal" style="color: #355f7c;" title="datetime.time" href="https://docs.python.org/2/library/datetime.html#datetime.time"><code class="xref py py-class docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">time</span></code></a>&nbsp;objects, the format codes for year, month, and day should not be used, as time objects have no such values. If they’re used anyway,&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">1900</span></code>&nbsp;is substituted for the year, and&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">1</span></code>&nbsp;for the month and day.</p> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">For&nbsp;<a class="reference internal" style="color: #355f7c;" title="datetime.date" href="https://docs.python.org/2/library/datetime.html#datetime.date"><code class="xref py py-class docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">date</span></code></a>&nbsp;objects, the format codes for hours, minutes, seconds, and microseconds should not be used, as&nbsp;<a class="reference internal" style="color: #355f7c;" title="datetime.date" href="https://docs.python.org/2/library/datetime.html#datetime.date"><code class="xref py py-class docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">date</span></code></a>&nbsp;objects have no such values. If they’re used anyway,&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">0</span></code>&nbsp;is substituted for them.</p> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">The full set of format codes supported varies across platforms, because Python calls the platform C library’s&nbsp;<code class="xref py py-func docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">strftime()</span></code>&nbsp;function, and platform variations are common. To see the full set of format codes supported on your platform, consult the&nbsp;<em class="manpage">strftime(3)</em>&nbsp;documentation.</p> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">For the same reason, handling of format strings containing Unicode code points that can’t be represented in the charset of the current locale is also platform-dependent. On some platforms such code points are preserved intact in the output, while on others&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">strftime</span></code>&nbsp;may raise&nbsp;<a class="reference internal" style="color: #355f7c;" title="exceptions.UnicodeError" href="https://docs.python.org/2/library/exceptions.html#exceptions.UnicodeError"><code class="xref py py-exc docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">UnicodeError</span></code></a>&nbsp;or return an empty string instead.</p> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">The following is a list of all the format codes that the C standard (1989 version) requires, and these work on all platforms with a standard C implementation. Note that the 1999 version of the C standard added additional format codes.</p> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">The exact range of years for which&nbsp;<code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">strftime()</span></code>&nbsp;works also varies across platforms. Regardless of platform, years before 1900 cannot be used.</p> 
 <table class="docutils align-default" style="border: 0px solid #ddccee; border-collapse: collapse; font-family: sans-serif; font-size: 16px;"> 
  <colgroup> 
   <col style="width: 0px;"> 
   <col style="width: 0px;"> 
   <col style="width: 0px;"> 
   <col style="width: 0px;"> 
  </colgroup> 
  <thead>
   <tr class="row-odd"> 
    <th class="head" style="text-align: center; padding: 2px 5px; background-color: #eeddee; border-left: 0px; border-top: 1px solid #ccaacc;"> <p style="text-align: justify; line-height: 20.8px;">Directive</p> </th> 
    <th class="head" style="text-align: center; padding: 2px 5px; background-color: #eeddee; border-left: 0px; border-top: 1px solid #ccaacc;"> <p style="text-align: justify; line-height: 20.8px;">Meaning</p> </th> 
    <th class="head" style="text-align: center; padding: 2px 5px; background-color: #eeddee; border-left: 0px; border-top: 1px solid #ccaacc;"> <p style="text-align: justify; line-height: 20.8px;">Example</p> </th> 
    <th class="head" style="text-align: center; padding: 2px 5px; background-color: #eeddee; border-left: 0px; border-top: 1px solid #ccaacc;"> <p style="text-align: justify; line-height: 20.8px;">Notes</p> </th> 
   </tr>
  </thead> 
  <tbody> 
   <tr class="row-even"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%a</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Weekday as locale’s abbreviated name.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> 
     <div class="line-block"> 
      <div class="line">
       Sun, Mon, …, Sat (en_US);
      </div> 
      <div class="line">
       So, Mo, …, Sa (de_DE)
      </div> 
     </div> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(1)</p> </td> 
   </tr> 
   <tr class="row-odd"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%A</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Weekday as locale’s full name.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> 
     <div class="line-block"> 
      <div class="line">
       Sunday, Monday, …, Saturday (en_US);
      </div> 
      <div class="line">
       Sonntag, Montag, …, Samstag (de_DE)
      </div> 
     </div> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(1)</p> </td> 
   </tr> 
   <tr class="row-even"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%w</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Weekday as a decimal number, where 0 is Sunday and 6 is Saturday.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">0, 1, …, 6</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;">&nbsp;</td> 
   </tr> 
   <tr class="row-odd"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%d</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Day of the month as a zero-padded decimal number.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">01, 02, …, 31</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;">&nbsp;</td> 
   </tr> 
   <tr class="row-even"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%b</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Month as locale’s abbreviated name.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> 
     <div class="line-block"> 
      <div class="line">
       Jan, Feb, …, Dec (en_US);
      </div> 
      <div class="line">
       Jan, Feb, …, Dez (de_DE)
      </div> 
     </div> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(1)</p> </td> 
   </tr> 
   <tr class="row-odd"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%B</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Month as locale’s full name.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> 
     <div class="line-block"> 
      <div class="line">
       January, February, …, December (en_US);
      </div> 
      <div class="line">
       Januar, Februar, …, Dezember (de_DE)
      </div> 
     </div> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(1)</p> </td> 
   </tr> 
   <tr class="row-even"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%m</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Month as a zero-padded decimal number.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">01, 02, …, 12</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;">&nbsp;</td> 
   </tr> 
   <tr class="row-odd"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%y</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Year without century as a zero-padded decimal number.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">00, 01, …, 99</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;">&nbsp;</td> 
   </tr> 
   <tr class="row-even"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%Y</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Year with century as a decimal number.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">1970, 1988, 2001, 2013</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;">&nbsp;</td> 
   </tr> 
   <tr class="row-odd"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%H</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Hour (24-hour clock) as a zero-padded decimal number.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">00, 01, …, 23</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;">&nbsp;</td> 
   </tr> 
   <tr class="row-even"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%I</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Hour (12-hour clock) as a zero-padded decimal number.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">01, 02, …, 12</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;">&nbsp;</td> 
   </tr> 
   <tr class="row-odd"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%p</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Locale’s equivalent of either AM or PM.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> 
     <div class="line-block"> 
      <div class="line">
       AM, PM (en_US);
      </div> 
      <div class="line">
       am, pm (de_DE)
      </div> 
     </div> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(1), (2)</p> </td> 
   </tr> 
   <tr class="row-even"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%M</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Minute as a zero-padded decimal number.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">00, 01, …, 59</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;">&nbsp;</td> 
   </tr> 
   <tr class="row-odd"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%S</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Second as a zero-padded decimal number.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">00, 01, …, 59</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(3)</p> </td> 
   </tr> 
   <tr class="row-even"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%f</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Microsecond as a decimal number, zero-padded on the left.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">000000, 000001, …, 999999</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(4)</p> </td> 
   </tr> 
   <tr class="row-odd"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%z</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">UTC offset in the form +HHMM or -HHMM (empty string if the the object is naive).</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(empty), +0000, -0400, +1030</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(5)</p> </td> 
   </tr> 
   <tr class="row-even"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%Z</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Time zone name (empty string if the object is naive).</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(empty), UTC, EST, CST</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;">&nbsp;</td> 
   </tr> 
   <tr class="row-odd"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%j</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Day of the year as a zero-padded decimal number.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">001, 002, …, 366</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;">&nbsp;</td> 
   </tr> 
   <tr class="row-even"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%U</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Week number of the year (Sunday as the first day of the week) as a zero padded decimal number. All days in a new year preceding the first Sunday are considered to be in week 0.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">00, 01, …, 53</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(6)</p> </td> 
   </tr> 
   <tr class="row-odd"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%W</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Week number of the year (Monday as the first day of the week) as a decimal number. All days in a new year preceding the first Monday are considered to be in week 0.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">00, 01, …, 53</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(6)</p> </td> 
   </tr> 
   <tr class="row-even"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%c</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Locale’s appropriate date and time representation.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> 
     <div class="line-block"> 
      <div class="line">
       Tue Aug 16 21:30:00 1988 (en_US);
      </div> 
      <div class="line">
       Di 16 Aug 21:30:00 1988 (de_DE)
      </div> 
     </div> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(1)</p> </td> 
   </tr> 
   <tr class="row-odd"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%x</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Locale’s appropriate date representation.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> 
     <div class="line-block"> 
      <div class="line">
       08/16/88 (None);
      </div> 
      <div class="line">
       08/16/1988 (en_US);
      </div> 
      <div class="line">
       16.08.1988 (de_DE)
      </div> 
     </div> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(1)</p> </td> 
   </tr> 
   <tr class="row-even"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%X</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">Locale’s appropriate time representation.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> 
     <div class="line-block"> 
      <div class="line">
       21:30:00 (en_US);
      </div> 
      <div class="line">
       21:30:00 (de_DE)
      </div> 
     </div> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">(1)</p> </td> 
   </tr> 
   <tr class="row-odd"> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%%</span></code></p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">A literal&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">'%'</span></code>&nbsp;character.</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;"> <p style="text-align: justify; line-height: 20.8px;">%</p> </td> 
    <td style="padding: 2px 5px; border-left: 0px; background-color: #eeeeff;">&nbsp;</td> 
   </tr> 
  </tbody> 
 </table> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">Notes:</p> 
 <ol class="arabic" style="font-family: sans-serif; font-size: 16px;"> 
  <li style="text-align: justify; line-height: 20.8px;"> <p style="line-height: 20.8px;">Because the format depends on the current locale, care should be taken when making assumptions about the output value. Field orderings will vary (for example, “month/day/year” versus “day/month/year”), and the output may contain Unicode characters encoded using the locale’s default encoding (for example, if the current locale is&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">ja_JP</span></code>, the default encoding could be any one of&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">eucJP</span></code>,&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">SJIS</span></code>, or&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">utf-8</span></code>; use&nbsp;<a class="reference internal" style="color: #355f7c;" title="locale.getlocale" href="https://docs.python.org/2/library/locale.html#locale.getlocale"><code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">locale.getlocale()</span></code></a>&nbsp;to determine the current locale’s encoding).</p> </li> 
  <li style="text-align: justify; line-height: 20.8px;"> <p style="line-height: 20.8px;">When used with the&nbsp;<code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">strptime()</span></code>&nbsp;method, the&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%p</span></code>&nbsp;directive only affects the output hour field if the&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%I</span></code>&nbsp;directive is used to parse the hour.</p> </li> 
  <li style="text-align: justify; line-height: 20.8px;"> <p style="line-height: 20.8px;">Unlike the&nbsp;<a class="reference internal" style="color: #355f7c;" title="time: Time access and conversions." href="https://docs.python.org/2/library/time.html#module-time"><code class="xref py py-mod docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">time</span></code></a>&nbsp;module, the&nbsp;<a class="reference internal" style="color: #355f7c;" title="datetime: Basic date and time types." href="https://docs.python.org/2/library/datetime.html#module-datetime"><code class="xref py py-mod docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">datetime</span></code></a>&nbsp;module does not support leap seconds.</p> </li> 
  <li style="text-align: justify; line-height: 20.8px;"> <p style="line-height: 20.8px;"><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%f</span></code>&nbsp;is an extension to the set of format characters in the C standard (but implemented separately in datetime objects, and therefore always available). When used with the&nbsp;<code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">strptime()</span></code>&nbsp;method, the&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%f</span></code>&nbsp;directive accepts from one to six digits and zero pads on the right.</p> 
   <div class="versionadded"> 
    <p style="line-height: 20.8px;"><span class="versionmodified added" style="font-style: italic;">New in version 2.6.</span></p> 
   </div> </li> 
  <li style="text-align: justify; line-height: 20.8px;"> <p style="line-height: 20.8px;">For a naive object, the&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%z</span></code>&nbsp;and&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%Z</span></code>&nbsp;format codes are replaced by empty strings.</p> <p style="line-height: 20.8px;">For an aware object:</p> 
   <dl class="simple" style="margin-bottom: 15px;"> 
    <dt>
     <code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%z</span></code>
    </dt> 
    <dd style="margin-top: 3px; margin-bottom: 10px; line-height: 20.8px;"> 
     <p style="line-height: 20.8px;"><code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">utcoffset()</span></code>&nbsp;is transformed into a 5-character string of the form +HHMM or -HHMM, where HH is a 2-digit string giving the number of UTC offset hours, and MM is a 2-digit string giving the number of UTC offset minutes. For example, if&nbsp;<code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">utcoffset()</span></code>&nbsp;returns&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">timedelta(hours=-3,</span>&nbsp;<span class="pre">minutes=-30)</span></code>,&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%z</span></code>&nbsp;is replaced with the string&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">'-0330'</span></code>.</p> 
    </dd> 
    <dt>
     <code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%Z</span></code>
    </dt> 
    <dd style="margin-top: 3px; margin-bottom: 10px; line-height: 20.8px;"> 
     <p style="line-height: 20.8px;">If&nbsp;<code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">tzname()</span></code>&nbsp;returns&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">None</span></code>,&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%Z</span></code>&nbsp;is replaced by an empty string. Otherwise&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%Z</span></code>&nbsp;is replaced by the returned value, which must be a string.</p> 
    </dd> 
   </dl> </li> 
  <li style="text-align: justify; line-height: 20.8px;"> <p style="line-height: 20.8px;">When used with the&nbsp;<code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">strptime()</span></code>&nbsp;method,&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%U</span></code>&nbsp;and&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">%W</span></code>&nbsp;are only used in calculations when the day of the week and the year are specified.</p> </li> 
 </ol> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>