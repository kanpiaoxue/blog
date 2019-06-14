#setFirstDayOfWeek in Calendar 不起作用，失效，不能用
###发表时间：2012-03-06
###分类：java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1441893" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1441893</a>

---

<p>在使用Calendar的时候，往往因为国外和中国的习惯不同，而造成迥异。比如，老外习惯周日作为每周的起始第一天，而中国习惯用周一作为每周的起始第一天。</p>
<p>我看见Calendar的API里面有<span style="background-color: #ffffff; font-size: x-small;">&nbsp;<span style="font-family: verdana, arial, helvetica, sans-serif; text-align: left;">setFirstDayOfWeek()。</span></span></p>
<p><span style="background-color: #ffffff; font-size: x-small;"><span style="font-family: verdana, arial, helvetica, sans-serif; text-align: left;">所以我设置setFirstDayOfWeek(Calendar.MONDAY)</span></span></p>
<p>但是发现使用cal.get(Calendar.DAY_OF_WEEK)得到的，还是以周日为起始第一天的结果。很是郁闷。上网找了，老外也有遇到这个问题的。老外遇到的问题：</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<ol class="dp-j" style="margin-top: 0px !important; margin-right: 0px !important; margin-bottom: 1px !important; margin-left: 45px !important; background-color: #dec7a4; color: #5c5c5c; font-family: 'Courier New', Courier, mono, serif; line-height: 18px; padding: 0px;"> 
 <li class="alt" style="padding-top: 0px !important; padding-right: 3px !important; padding-bottom: 0px !important; padding-left: 10px !important; border-top-style: none; border-right-style: none; border-bottom-style: none; border-left-style: solid; border-color: initial; border-left-width: 3px; border-left-color: #dec7a4; background-color: #eadbc4; color: inherit; line-height: 14px; margin: 0px !important;"><span style="background-color: inherit; padding: 0px; margin: 0px;"><span style="background-color: inherit; padding: 0px; margin: 0px;">&nbsp;Calendar&nbsp;myCalendar&nbsp;=&nbsp;Calendar.getInstance();&nbsp;&nbsp;</span></span></li> 
 <li style="padding-top: 0px !important; padding-right: 3px !important; padding-bottom: 0px !important; padding-left: 10px !important; border-top-style: none; border-right-style: none; border-bottom-style: none; border-left-style: solid; border-color: initial; border-left-width: 3px; border-left-color: #dec7a4; background-color: #f0e6d5; line-height: 14px; margin: 0px !important;"><span style="background-color: inherit; padding: 0px; margin: 0px;">&nbsp;&nbsp;myCalendar.setTime(<span class="keyword" style="color: #006699; background-color: inherit; font-weight: bold; padding: 0px; margin: 0px;">new</span><span style="background-color: inherit; padding: 0px; margin: 0px;">&nbsp;Date());&nbsp;&nbsp;</span></span></li> 
 <li class="alt" style="padding-top: 0px !important; padding-right: 3px !important; padding-bottom: 0px !important; padding-left: 10px !important; border-top-style: none; border-right-style: none; border-bottom-style: none; border-left-style: solid; border-color: initial; border-left-width: 3px; border-left-color: #dec7a4; background-color: #eadbc4; color: inherit; line-height: 14px; margin: 0px !important;"><span style="background-color: inherit; padding: 0px; margin: 0px;">&nbsp;&nbsp;System.out.println(myCalendar.get(Calendar.DAY_OF_WEEK);&nbsp;&nbsp;</span></li> 
 <li style="padding-top: 0px !important; padding-right: 3px !important; padding-bottom: 0px !important; padding-left: 10px !important; border-top-style: none; border-right-style: none; border-bottom-style: none; border-left-style: solid; border-color: initial; border-left-width: 3px; border-left-color: #dec7a4; background-color: #f0e6d5; line-height: 14px; margin: 0px !important;"><span style="background-color: inherit; padding: 0px; margin: 0px;">&nbsp;&nbsp;myCalendar.setFirstDayOfWeek(Calendar.MONDAY);&nbsp;&nbsp;</span></li> 
 <li class="alt" style="padding-top: 0px !important; padding-right: 3px !important; padding-bottom: 0px !important; padding-left: 10px !important; border-top-style: none; border-right-style: none; border-bottom-style: none; border-left-style: solid; border-color: initial; border-left-width: 3px; border-left-color: #dec7a4; background-color: #eadbc4; color: inherit; line-height: 14px; margin: 0px !important;"><span style="background-color: inherit; padding: 0px; margin: 0px;">&nbsp;&nbsp;System.out.println(myCalendar.get(Calendar.DAY_OF_WEEK);&nbsp;</span></li> 
</ol>
<div>
 <br>
</div>
<div> 
 <span style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #f0e6d5;">Calendar returns the same value before and after setFirstDayOfWeek.</span>
 <br style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #f0e6d5;">
 <span style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #f0e6d5;">Any ideas on why this doesn't work and how to get it to work?</span> 
</div>
<div>
 <br>
</div>
<div>
 另一个老外给出了结论，才让我恍然大悟：
</div>
<div>
 <br>
</div>
<div> 
 <span style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">This is one of many ways in which&nbsp;</span>
 <a class="api" style="text-decoration: none; border-bottom-width: 1px; border-bottom-style: dotted; border-bottom-color: #555555; font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;" title="Java API" href="http://docs.oracle.com/javase/7/docs/api/java/util/Calendar.html" target="_new">java.util.Calendar</a>
 <span style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">&nbsp;is counterintuitive. It does work, but not the way you're expecting. Look at the documentation[ for the&nbsp;</span>
 <a style="color: #000080; font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;" href="http://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html#DAY_OF_WEEK" target="_blank">DAY_OF_WEEK</a>
 <span style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">&nbsp;field: "This field takes values SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, and SATURDAY." When your program prints 6, it's telling you that the day of week is&nbsp;</span>
 <a style="color: #000080; font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;" href="http://java.sun.com/j2se/1.5.0/docs/api/constant-values.html#java.util.Calendar.FRIDAY" target="_blank">FRIDAY</a>
 <span style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">. This constant value has nothing to do with the beginning of the week - it's just a constant that means FRIDAY. It does coincidentally happen to be the same as the day of the week if the first day of the week is SUNDAY (1) - but it doesn't change if the first day of the week is redefined.</span>
 <br style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">
 <br style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">
 <span style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">Compare this to the API for&nbsp;</span>
 <a style="color: #000080; font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;" href="http://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html#WEEK_OF_MONTH" target="_blank">WEEK_OF_MONTH</a>
 <span style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">&nbsp;and&nbsp;</span>
 <a style="color: #000080; font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;" href="http://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html#WEEK_OF_YEAR" target="_blank">WEEK_OF_YEAR</a>
 <span style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">, which&nbsp;</span>
 <em style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">do</em>
 <span style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">&nbsp;say that they depend on the first day of the week. You can&nbsp;</span>
 <a class="api" style="text-decoration: none; border-bottom-width: 1px; border-bottom-style: dotted; border-bottom-color: #555555; font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;" title="article: Evil Unit Testing" href="http://www.javaranch.com/unit-testing.jsp" target="_new">test</a>
 <span style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">&nbsp;to see if this works correctly for your purposes.</span>
 <br style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">
 <br style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">
 <span style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">If you really need a number representing day of week with 1 meaning Monday and 7 meaning Sunday, you can get it with a tiny bit of math:</span>
 <br style="font-family: verdana, arial, helvetica, sans-serif; line-height: 18px; background-color: #eadbc4;">
 <div class="dp-highlighter" style="font-family: 'Courier New', Courier, mono, serif; background-color: #eadbc4; width: 960px; margin-top: 18px !important; margin-right: 0px !important; margin-bottom: 18px !important; margin-left: 0px !important; padding-top: 1px;"> 
  <div class="bar" style="line-height: 18px; padding-left: 45px;"> 
   <div class="tools"> 
    <a style="color: #a0a0a0; text-decoration: none; background-image: none; background-color: inherit; margin-top: 0px; margin-right: 10px; margin-bottom: 0px; margin-left: 0px; font-size: 9px; padding: 0px;" href="http://www.coderanch.com/t/381293/java/java/setFirstDayOfWeek-Calendar">view plain</a>
    <a style="color: #a0a0a0; text-decoration: none; background-image: none; background-color: inherit; margin-top: 0px; margin-right: 10px; margin-bottom: 0px; margin-left: 0px; font-size: 9px; padding: 0px;" href="http://www.coderanch.com/t/381293/java/java/setFirstDayOfWeek-Calendar">copy to clipboard</a>
    <a style="color: #a0a0a0; text-decoration: none; background-image: none; background-color: inherit; margin-top: 0px; margin-right: 10px; margin-bottom: 0px; margin-left: 0px; font-size: 9px; padding: 0px;" href="http://www.coderanch.com/t/381293/java/java/setFirstDayOfWeek-Calendar">print</a>
    <a style="color: #a0a0a0; text-decoration: none; background-image: none; background-color: inherit; margin-top: 0px; margin-right: 10px; margin-bottom: 0px; margin-left: 0px; font-size: 9px; padding: 0px;" href="http://www.coderanch.com/t/381293/java/java/setFirstDayOfWeek-Calendar">?</a> 
   </div> 
  </div> 
  <ol class="dp-j" style="line-height: 18px; margin-top: 0px !important; margin-right: 0px !important; margin-bottom: 1px !important; margin-left: 45px !important; background-color: #ffffff; color: #5c5c5c; padding: 0px;"> 
   <li class="alt" style="padding-top: 0px !important; padding-right: 3px !important; padding-bottom: 0px !important; padding-left: 10px !important; border-top-style: none; border-right-style: none; border-bottom-style: none; border-left-style: solid; border-color: initial; border-left-width: 3px; border-left-color: #dec7a4; background-color: #eadbc4; color: inherit; line-height: 14px; margin: 0px !important;"><span style="background-color: inherit; padding: 0px; margin: 0px;"><span class="keyword" style="color: #006699; background-color: inherit; font-weight: bold; padding: 0px; margin: 0px;">int</span><span style="background-color: inherit; padding: 0px; margin: 0px;">&nbsp;dayOfWeek&nbsp;=&nbsp;myCalendar.get(Calendar.DAY_OF_WEEK)&nbsp;-&nbsp;</span><span class="number" style="color: #c00000; background-color: inherit; padding: 0px; margin: 0px;">1</span><span style="background-color: inherit; padding: 0px; margin: 0px;">;&nbsp;&nbsp;</span></span></li> 
   <li style="padding-top: 0px !important; padding-right: 3px !important; padding-bottom: 0px !important; padding-left: 10px !important; border-top-style: none; border-right-style: none; border-bottom-style: none; border-left-style: solid; border-color: initial; border-left-width: 3px; border-left-color: #dec7a4; background-color: #f0e6d5; line-height: 14px; margin: 0px !important;"><span style="background-color: inherit; padding: 0px; margin: 0px;"><span class="keyword" style="color: #006699; background-color: inherit; font-weight: bold; padding: 0px; margin: 0px;">if</span><span style="background-color: inherit; padding: 0px; margin: 0px;">&nbsp;(dayOfWeek&nbsp;==&nbsp;</span><span class="number" style="color: #c00000; background-color: inherit; padding: 0px; margin: 0px;">0</span><span style="background-color: inherit; padding: 0px; margin: 0px;">)&nbsp;&nbsp;</span></span></li> 
   <li class="alt" style="padding-top: 0px !important; padding-right: 3px !important; padding-bottom: 0px !important; padding-left: 10px !important; border-top-style: none; border-right-style: none; border-bottom-style: none; border-left-style: solid; border-color: initial; border-left-width: 3px; border-left-color: #dec7a4; background-color: #eadbc4; color: inherit; line-height: 14px; margin: 0px !important;"><span style="background-color: inherit; padding: 0px; margin: 0px;">&nbsp;&nbsp;&nbsp;&nbsp;dayOfWeek&nbsp;=&nbsp;<span class="number" style="color: #c00000; background-color: inherit; padding: 0px; margin: 0px;">7</span><span style="background-color: inherit; padding: 0px; margin: 0px;">; &nbsp;</span></span></li> 
  </ol> 
  <div>
   <br>
  </div> 
 </div> 
 <div>
  看完了，就明白了。
 </div> 
 <div> 
  <pre name="code" class="java">public int getDayOfWeek(String dateString){
	SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd");
	try {
		Date date = format.parse(dateString);
		Calendar cal = Calendar.getInstance();
		cal.setTime(date);
		cal.setFirstDayOfWeek(Calendar.MONDAY);
		int tmp = cal.get(Calendar.DAY_OF_WEEK) - 1;
		if (0 == tmp) {
			tmp = 7;
		}
		return tmp;
	} catch (ParseException e) {
		e.printStackTrace();
		return -1;
	}
}</pre> &nbsp;
 </div> 
 <div>
  下面是链接：&nbsp;
  <a href="http://www.coderanch.com/t/381293/java/java/setFirstDayOfWeek-Calendar">http://www.coderanch.com/t/381293/java/java/setFirstDayOfWeek-Calendar</a> 
 </div> 
</div>
<div>
 <br>
</div>
<div>
 <br>
</div>