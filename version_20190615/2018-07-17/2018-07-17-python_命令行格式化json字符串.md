#python 命令行格式化json字符串
###发表时间：2018-07-17
###分类：python,json,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2426996" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2426996</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>命令行：</p> 
 <pre name="code" class="java">echo '{"id":343,"name":"kanpiaoxue"}' | python -m json.tool</pre> 
 <p>&nbsp;输出：</p> 
 <div class="quote_div">
  {
  <br> "id": 343,
  <br> "name": "kanpiaoxue"
  <br>}
 </div> 
 <p>&nbsp;</p> 
 <p>命令行：</p> 
 <pre name="code" class="java">echo '[{"id":0,"name":"kanpiaoxue0"},{"id":1,"name":"kanpiaoxue1"},{"id":2,"name":"kanpiaoxue2"}]' | python -m json.tool</pre> 
 <p>&nbsp;&nbsp;输出：</p> 
 <pre name="code" class="java">[
    {
        "id": 0,
        "name": "kanpiaoxue0"
    },
    {
        "id": 1,
        "name": "kanpiaoxue1"
    },
    {
        "id": 2,
        "name": "kanpiaoxue2"
    }
]</pre> 
 <p>&nbsp;</p> 
</div>