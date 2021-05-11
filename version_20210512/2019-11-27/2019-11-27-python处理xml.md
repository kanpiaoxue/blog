#python处理xml
###发表时间：2019-11-27
###分类：python,XML,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2510453" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2510453</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>使用python的内置功能&nbsp;xml.etree.ElementTree 处理 xml</p> 
 <p>参考资料：</p> 
 <p>&nbsp;<a href="https://pycoders-weekly-chinese.readthedocs.io/en/latest/issue6/processing-xml-in-python-with-element-tree.html">https://pycoders-weekly-chinese.readthedocs.io/en/latest/issue6/processing-xml-in-python-with-element-tree.html</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>如何在xml里面添加文档声明的header呢？</p> 
 <pre name="code" class="xml">&lt;?xml version='1.0' encoding='utf-8'?&gt;</pre> 
 <p>&nbsp;代码如下：</p> 
 <pre name="code" class="python">f = '/usr/hello.xml'
tree.write(f, encoding='utf-8', xml_declaration=True) </pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>参考资料：&nbsp;<a href="https://stackoverflow.com/questions/15356641/how-to-write-xml-declaration-using-xml-etree-elementtree">https://stackoverflow.com/questions/15356641/how-to-write-xml-declaration-using-xml-etree-elementtree</a></p> 
</div>