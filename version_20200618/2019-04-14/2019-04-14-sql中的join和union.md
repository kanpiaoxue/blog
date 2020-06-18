#sql中的join和union
###发表时间：2019-04-14
###分类：sql,database
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2440078" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2440078</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>sql教程：<a href="http://www.w3school.com.cn/sql/index.asp">http://www.w3school.com.cn/sql/index.asp</a></p> 
 <p>&nbsp;</p> 
 <p>下面列出了您可以使用的 JOIN 类型，以及它们之间的差异。</p> 
 <ul> 
  <li>JOIN: 如果表中有至少一个匹配，则返回行。INNER JOIN 与 JOIN 是相同的所有的行</li> 
  <li>RIGHT JOIN: 即使左表中没有匹配，也从右表返回所有的行</li> 
  <li>FULL JOIN: 只要其中一个表中存在匹配，就返回行</li> 
 </ul> 
 <p>INNER JOIN 关键字语法</p> 
 <pre name="code" class="sql">SELECT column_name(s)
FROM table_name1
INNER JOIN table_name2 
ON table_name1.column_name=table_name2.column_name</pre> 
 <p>&nbsp;</p> 
 <p>LEFT JOIN 关键字语法</p> 
 <pre name="code" class="sql">SELECT column_name(s)
FROM table_name1
LEFT JOIN table_name2 
ON table_name1.column_name=table_name2.column_name
-- 注释：在某些数据库中， LEFT JOIN 称为 LEFT OUTER JOIN。</pre> 
 <p>&nbsp;</p> 
 <p>RIGHT JOIN 关键字语法</p> 
 <pre name="code" class="sql">SELECT column_name(s)
FROM table_name1
RIGHT JOIN table_name2 
ON table_name1.column_name=table_name2.column_name
-- 注释：在某些数据库中， RIGHT JOIN 称为 RIGHT OUTER JOIN。</pre> 
 <p>&nbsp;</p> 
 <p>FULL JOIN 关键字语法</p> 
 <pre name="code" class="sql">SELECT column_name(s)
FROM table_name1
FULL JOIN table_name2 
ON table_name1.column_name=table_name2.column_name
-- 注释：在某些数据库中， FULL JOIN 称为 FULL OUTER JOIN。</pre> 
 <p>&nbsp;</p> 
 <p><strong>SQL UNION 操作符</strong></p> 
 <p>UNION 操作符用于合并两个或多个 SELECT 语句的结果集。</p> 
 <p>请注意，UNION 内部的 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每条 SELECT 语句中的列的顺序必须相同。</p> 
 <p>&nbsp;</p> 
 <p>SQL UNION 语法</p> 
 <pre name="code" class="sql">SELECT column_name(s) FROM table_name1
UNION
SELECT column_name(s) FROM table_name2
-- 注释：默认地，UNION 操作符选取不同的值。如果允许重复的值，请使用 UNION ALL。</pre> 
 <p>&nbsp;</p> 
 <p>SQL UNION ALL 语法</p> 
 <pre name="code" class="sql">SELECT column_name(s) FROM table_name1
UNION ALL
SELECT column_name(s) FROM table_name2
-- 另外，UNION 结果集中的列名总是等于 UNION 中第一个 SELECT 语句中的列名。</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;&nbsp;</p> 
</div>