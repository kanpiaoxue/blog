#修改Eclipse注释里的${Date}变量格式
###发表时间：2017-07-07
###分类：eclipse,经验,非技术
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2383537" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2383537</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>在eclipse的 Preference -&gt; Java -&gt; Code Style -&gt; Code Templates 的javadoc中，我们往往会自定义自己的javadoc的模板。如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">/** 
 * ClassName: ${type_name} &lt;br/&gt; 
 * @author ${user} 
 * @version 1.0
 * Create Time: ${date} ${time} &lt;br/&gt; 
 * Description: ${todo} 类的实现描述
 */  </pre> 
 <p>&nbsp;这个时候会出现一点小问题，那就是变量&nbsp;<span style="background-color: #fafafa; font-family: monospace;">${date} 会生成“2016年1月1日”这样的中文格式，而变量 ${time} 则会生成"上午9:00"这样的格式。</span></p> 
 <p>&nbsp;</p> 
 <p><span style="background-color: #fafafa; font-family: monospace;">由于我是个强迫症患者，而且习惯于自己定义的日期时间格式，上面的带有中文格式的日期显然不是我想要的。那怎么办啊？</span></p> 
 <p><span style="background-color: #fafafa; font-family: monospace;">改为如下：</span></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">/** 
 * ClassName: ${type_name} &lt;br/&gt; 
 * @author ${user} 
 * @version 1.0
 * Create Time: ${d:date('yyyy/MM/dd HH:mm:ss')}&lt;br/&gt; 
 * Description: ${todo} 类的实现描述
 */ </pre> 
 <p>&nbsp;注意上面的日期格式化的方法：&nbsp;<span style="background-color: #fafafa; font-family: monospace;">${d:date('yyyy/MM/dd HH:mm:ss')}</span></p> 
 <p>&nbsp;</p> 
 <p><span style="background-color: #fafafa; font-family: monospace;">【格外注意】这种日期变量进行格式化的方法只支持eclipse 4.x以上版本，原因：eclipse 4.x之前的版本没有这个功能，不支持日期的字符串格式化。</span></p> 
 <p><span style="background-color: #fafafa; font-family: monospace;">参考资料地址：&nbsp;</span></p> 
 <p><a href="https://stackoverflow.com/questions/1131712/how-to-set-the-eclipse-date-variable-format"><span style="font-family: monospace;">https://stackoverflow.com/questions/1131712/how-to-set-the-eclipse-date-variable-format</span></a></p> 
 <p>&nbsp;</p> 
 <p><a href="https://stackoverflow.com/questions/32119571/templates-in-eclipse">https://stackoverflow.com/questions/32119571/templates-in-eclipse</a></p> 
</div>