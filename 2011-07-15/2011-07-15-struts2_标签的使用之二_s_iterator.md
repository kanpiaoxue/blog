#struts2 标签的使用之二 s:iterator
###发表时间：2011-07-15
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1125059" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1125059</a>

---

<p><span style="color: #333333; font-family: Arial; font-size: 14px; line-height: 26px;"> </span></p>
<p>&nbsp;struts2的s：iterator 可以遍历 数据栈里面的任何数组，集合等等 以下几个简单的demo：<br>s:iterator 标签有3个属性：<br>&nbsp;&nbsp;&nbsp; value：被迭代的集合<br>&nbsp;&nbsp;&nbsp; id&nbsp;&nbsp; ：指定集合里面的元素的id<br>&nbsp;&nbsp;&nbsp; status 迭代元素的索引<br><br>1:jsp页面定义元素写法 数组或list</p>
<div class="highlighter">
 <ol class="highlighter-c"> 
  <li> <span>&lt;s:iterator&nbsp;value=</span><span class="string">"{'1','2','3','4','5'}"</span><span>&nbsp;id=</span><span class="string">'number'</span><span>&gt;</span> </li> 
  <li class="alt"> <span>&nbsp;&nbsp;&nbsp;&nbsp;&lt;s:property&nbsp;value=</span><span class="string">'number'</span><span>/&gt;A</span> </li> 
  <li><span>&lt;/s:iterator&gt;</span></li> 
 </ol>
</div>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<div class="highlighter">
 <ol class="highlighter-c"> 
  <li> <span>&lt;s:iterator&nbsp;value=</span><span class="string">"{'a','b','c'}"</span><span>&nbsp;id=</span><span class="string">'char'</span><span>&nbsp;status=</span><span class="string">'st'</span><span>&gt;</span> </li> 
  <li class="alt"> <span>&nbsp;&nbsp;&nbsp;&nbsp;&lt;s:</span><span class="keyword">if</span><span>&nbsp;test=</span><span class="string">"#st.Even"</span><span>&gt;</span> </li> 
  <li> <span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;现在的索引是奇数为:&lt;s:property&nbsp;value=</span><span class="string">'#st.index'</span><span>/&gt;</span> </li> 
  <li class="alt"> <span>&nbsp;&nbsp;&nbsp;&nbsp;&lt;/s:</span><span class="keyword">if</span><span>&gt;</span> </li> 
  <li> <span>&nbsp;&nbsp;&nbsp;&nbsp;当前元素值：&lt;s:property&nbsp;value=</span><span class="string">'char'</span><span>/&gt;</span> </li> 
  <li class="alt"><span>&lt;/s:iterator&gt;</span></li> 
 </ol>
</div>
<br>
<br>
<div class="highlighter">
 <ol class="highlighter-c"> 
  <li> <span>value=</span><span class="string">"#{"</span><span>1</span><span class="string">":"</span><span>a</span><span class="string">","</span><span>2</span><span class="string">":"</span><span>b</span><span class="string">"}"</span> </li> 
 </ol>
</div>
<br>
<br>
<br>
<div class="highlighter">
 <ol class="highlighter-c"> 
  <li> <span>&lt;s:iterator&nbsp;value=</span><span class="string">"map"</span><span>&nbsp;id=</span><span class="string">"id"</span><span>&nbsp;status=</span><span class="string">"st"</span><span>&gt;</span> </li> 
  <li class="alt"> <span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;key&nbsp;:&nbsp;&lt;s:property&nbsp;value=</span><span class="string">'key'</span><span>/&gt;</span> </li> 
  <li> <span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value:&lt;s:property&nbsp;vlaue=</span><span class="string">'value'</span><span>/&gt;</span> </li> 
  <li class="alt"><span>&lt;/s:iterator&gt;</span></li> 
 </ol>
</div>
<br>
<br>
<br>
<br>
<br>
<div class="highlighter">
 <ol class="highlighter-c"> 
  <li> <span>&lt;s:iterator&nbsp;value=</span><span class="string">"label"</span><span>&nbsp;id=</span><span class="string">"id"</span><span>&gt;</span> </li> 
  <li class="alt"> <span>&nbsp;&nbsp;&nbsp;&nbsp;&lt;s:property&nbsp;value=</span><span class="string">"#id.attrName"</span><span>&nbsp;/&gt;</span> </li> 
  <li><span>&lt;/s:iterator&gt;</span></li> 
 </ol>
</div>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<div class="highlighter">
 <ol class="highlighter-xml"> 
  <li> <span class="tag">&lt;</span><span class="tag-name">s:iterator</span><span>&nbsp;</span><span class="attribute">value</span><span>=</span><span class="attribute-value">"%{attrN&nbsp;}"</span><span>&nbsp;</span><span class="attribute">id</span><span>=</span><span class="attribute-value">"id"</span><span>&nbsp;&nbsp;&nbsp;</span><span class="attribute">status</span><span>=</span><span class="attribute-value">"status"</span><span class="tag">&gt;</span> </li> 
  <li class="alt"> <span>&nbsp;index&nbsp;&nbsp;&nbsp;&nbsp;is&nbsp;:&nbsp;</span><span class="tag">&lt;</span><span class="tag-name">s:property</span><span>&nbsp;</span><span class="attribute">value</span><span>=</span><span class="attribute-value">'status.index'</span><span class="tag">/&gt;</span> </li> 
  <li> <span>&nbsp;attrName&nbsp;is&nbsp;:&nbsp;</span><span class="tag">&lt;</span><span class="tag-name">s:property</span><span>&nbsp;</span><span class="attribute">value</span><span>=</span><span class="attribute-value">'id'</span><span class="tag">/&gt;</span><span>&nbsp;or&nbsp;</span><span class="tag">&lt;</span><span class="tag-name">s:property</span><span>&nbsp;</span><span class="attribute">value</span><span>=</span><span class="attribute-value">'%{id}'</span><span class="tag">/&gt;</span><span>&nbsp;</span> </li> 
  <li class="alt"> <span>&nbsp;attrName&nbsp;is&nbsp;:&nbsp;</span><span class="tag">&lt;</span><span class="tag-name">s:property</span><span>&nbsp;</span><span class="attribute">value</span><span>=</span><span class="attribute-value">'%{attrV[#status.index]}'</span><span class="tag">/&gt;</span> </li> 
  <li> <span class="tag">&lt;/</span><span class="tag-name">s:iterator</span><span class="tag">&gt;</span><span>&nbsp;&nbsp;</span> </li> 
 </ol>
</div>
<p></p>