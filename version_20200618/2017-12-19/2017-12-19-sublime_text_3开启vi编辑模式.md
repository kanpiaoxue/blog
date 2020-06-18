#sublime text 3开启vi编辑模式
###发表时间：2017-12-19
###分类：sublime,经验,mac
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2405062" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2405062</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>sublime支持原始的vi编辑器模式。默认的配置中是不开启vi支持的。该如何开启sublime的vi模式呢？</p> 
 <p>在菜单栏中： Preferences -&gt; Setting - User 即可打开配置文件进行编辑，将 ignored_packages 项的[]里面"Vintage"内容注释掉或者删除掉，如下：</p> 
 <pre name="code" class="js">"ignored_packages":
[
     // "Vintage"
]</pre> 
 <p>&nbsp;再按 Esc 退出编辑模式，即进入了 Vi 模式。</p> 
</div>