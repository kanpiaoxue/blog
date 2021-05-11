#Python变量名解析：LEGB原则
###发表时间：2012-05-06
###分类：经验,python
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1513295" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1513295</a>

---

<p>---- 来源于《Python学习手册》Page 419</p>
<p>Python的变量名解析机制称为：LEGB法则。L：本地作用域；E：上一层结构中def或lambda的本地作用域；G：全局作用域；B：内置作用域</p>
<p>LEGB作用域查找原则：当引用一个变量时，Python按以下顺序依次进行查找：从本地变量中，在任意上层函数的作用域，在全局作用域，最后在内置作用域中查找。第一个能够完成查找的就算成功。变量在代码中被赋值的位置通常就决定了它的作用域。在Python3.0中，nonlocal声明也可以迫使名称映射到函数内部的作用域中，而不管是否对其赋值。</p>
<p>这些规则仅对简单的变量名有效。</p>