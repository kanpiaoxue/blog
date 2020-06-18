#HQL: Hibernate查询语言
###发表时间：2010-04-13
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/643002" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/643002</a>

---

<p>HQL: Hibernate查询语言 <br>Hibernate配备了一种非常强大的查询语言，这种语言看上去很像SQL。但是不要被语法结构 上的相似所迷惑，HQL是非常有意识的被设计为完全面向对象的查询，它可以理解如继承、多态 和关联之类的概念。 </p>
<p><br>第 15 章 HQL: Hibernate查询语言<br>Hibernate配备了一种非常强大的查询语言，这种语言看上去很像SQL。但是不要被语法结构 上的相似所迷惑，HQL是非常有意识的被设计为完全面向对象的查询，它可以理解如继承、多态 和关联之类的概念。 </p>
<p>15.1. 大小写敏感性问题<br>除了Java类与属性的名称外，查询语句对大小写并不敏感。 所以 SeLeCT 与 sELEct 以及 SELECT 是相同的，但是 org.hibernate.eg.FOO 并不等价于 org.hibernate.eg.Foo 并且 foo.barSet 也不等价于 foo.BARSET。 </p>
<p>本手册中的HQL关键字将使用小写字母. 很多用户发现使用完全大写的关键字会使查询语句 的可读性更强, 但我们发现，当把查询语句嵌入到Java语句中的时候使用大写关键字比较难看。 </p>
<p>15.2. from子句<br>Hibernate中最简单的查询语句的形式如下： </p>
<p>from eg.Cat<br>该子句简单的返回eg.Cat类的所有实例。 通常我们不需要使用类的全限定名, 因为 auto-import（自动引入） 是缺省的情况。 所以我们几乎只使用如下的简单写法： </p>
<p>from Cat<br>大多数情况下, 你需要指定一个别名, 原因是你可能需要 在查询语句的其它部分引用到Cat </p>
<p>from Cat as cat<br>这个语句把别名cat指定给类Cat 的实例, 这样我们就可以在随后的查询中使用此别名了。 关键字as 是可选的，我们也可以这样写: </p>
<p>from Cat cat<br>子句中可以同时出现多个类, 其查询结果是产生一个笛卡儿积或产生跨表的连接。 </p>
<p>from Formula, Parameter<br>from Formula as form, Parameter as param<br>查询语句中别名的开头部分小写被认为是实践中的好习惯， 这样做与Java变量的命名标准保持了一致 (比如，domesticCat)。 </p>
<p>15.3. 关联(Association)与连接(Join)<br>我们也可以为相关联的实体甚至是对一个集合中的全部元素指定一个别名, 这时要使用关键字join。 </p>
<p>from Cat as cat <br>&nbsp;&nbsp;&nbsp; inner join cat.mate as mate<br>&nbsp;&nbsp;&nbsp; left outer join cat.kittens as kitten<br>from Cat as cat left join cat.mate.kittens as kittens<br>from Formula form full join form.parameter param<br>受支持的连接类型是从ANSI SQL中借鉴来的。 </p>
<p>inner join（内连接） </p>
<p>left outer join（左外连接） </p>
<p>right outer join（右外连接） </p>
<p>full join (全连接，并不常用) </p>
<p>语句inner join, left outer join 以及 right outer join 可以简写。 </p>
<p>from Cat as cat <br>&nbsp;&nbsp;&nbsp; join cat.mate as mate<br>&nbsp;&nbsp;&nbsp; left join cat.kittens as kitten<br>还有，一个"fetch"连接允许仅仅使用一个选择语句就将相关联的对象或一组值的集合随着他们的父对象的初始化而被初始化，这种方法在使用到集合的情况下尤其有用，对于关联和集合来说，它有效的代替了映射文件中的外联接 与延迟声明（lazy declarations）. 查看 第 20.1 节 “ 抓取策略(Fetching strategies) ” 以获得等多的信息。 </p>
<p>from Cat as cat <br>&nbsp;&nbsp;&nbsp; inner join fetch cat.mate<br>&nbsp;&nbsp;&nbsp; left join fetch cat.kittens<br>一个fetch连接通常不需要被指定别名, 因为相关联的对象不应当被用在 where 子句 (或其它任何子句)中。同时，相关联的对象 并不在查询的结果中直接返回，但可以通过他们的父对象来访问到他们。 </p>
<p>注意fetch构造变量在使用了scroll() 或 iterate()函数 的查询中是不能使用的。最后注意，使用full join fetch 与 right join fetch是没有意义的。 </p>
<p>如果你使用属性级别的延迟获取（lazy fetching）（这是通过重新编写字节码实现的），可以使用 fetch all properties 来强制Hibernate立即取得那些原本需要延迟加载的属性（在第一个查询中）。 </p>
<p>from Document fetch all properties order by name<br>from Document doc fetch all properties where lower(doc.name) like '%cats%'<br>15.4. select子句<br>select 子句选择将哪些对象与属性返 回到查询结果集中. 考虑如下情况: </p>
<p>select mate <br>from Cat as cat <br>&nbsp;&nbsp;&nbsp; inner join cat.mate as mate<br>该语句将选择mates of other Cats。（其他猫的配偶） 实际上, 你可以更简洁的用以下的查询语句表达相同的含义: </p>
<p>select cat.mate from Cat cat<br>查询语句可以返回值为任何类型的属性，包括返回类型为某种组件(Component)的属性: </p>
<p>select cat.name from DomesticCat cat<br>where cat.name like 'fri%'<br>select cust.name.firstName from Customer as cust<br>查询语句可以返回多个对象和（或）属性，存放在 Object[]队列中, </p>
<p>select mother, offspr, mate.name <br>from DomesticCat as mother<br>&nbsp;&nbsp;&nbsp; inner join mother.mate as mate<br>&nbsp;&nbsp;&nbsp; left outer join mother.kittens as offspr<br>或存放在一个List对象中, </p>
<p>select new list(mother, offspr, mate.name)<br>from DomesticCat as mother<br>&nbsp;&nbsp;&nbsp; inner join mother.mate as mate<br>&nbsp;&nbsp;&nbsp; left outer join mother.kittens as offspr<br>也可能直接返回一个实际的类型安全的Java对象, </p>
<p>select new Family(mother, mate, offspr)<br>from DomesticCat as mother<br>&nbsp;&nbsp;&nbsp; join mother.mate as mate<br>&nbsp;&nbsp;&nbsp; left join mother.kittens as offspr<br>假设类Family有一个合适的构造函数. </p>
<p>你可以使用关键字as给“被选择了的表达式”指派别名: </p>
<p>select max(bodyWeight) as max, min(bodyWeight) as min, count(*) as n<br>from Cat cat<br>这种做法在与子句select new map一起使用时最有用: </p>
<p>select new map( max(bodyWeight) as max, min(bodyWeight) as min, count(*) as n )<br>from Cat cat<br>该查询返回了一个Map的对象，内容是别名与被选择的值组成的名-值映射。 </p>
<p>15.5. 聚集函数<br>HQL查询甚至可以返回作用于属性之上的聚集函数的计算结果: </p>
<p>select avg(cat.weight), sum(cat.weight), max(cat.weight), count(cat)<br>from Cat cat<br>受支持的聚集函数如下： </p>
<p>avg(...), sum(...), min(...), max(...) </p>
<p>count(*) </p>
<p>count(...), count(distinct ...), count(all...) </p>
<p>你可以在选择子句中使用数学操作符、连接以及经过验证的SQL函数： </p>
<p>select cat.weight + sum(kitten.weight) <br>from Cat cat <br>&nbsp;&nbsp;&nbsp; join cat.kittens kitten<br>group by cat.id, cat.weight<br>select firstName||' '||initial||' '||upper(lastName) from Person<br>关键字distinct与all 也可以使用，它们具有与SQL相同的语义. </p>
<p>select distinct cat.name from Cat cat</p>
<p>select count(distinct cat.name), count(cat) from Cat cat<br>15.6. 多态查询<br>一个如下的查询语句: </p>
<p>from Cat as cat<br>不仅返回Cat类的实例, 也同时返回子类 DomesticCat的实例. Hibernate 可以在from子句中指定任何 Java 类或接口. 查询会返回继承了该类的所有持久化子类 的实例或返回声明了该接口的所有持久化类的实例。下面的查询语句返回所有的被持久化的对象： </p>
<p>from java.lang.Object o<br>接口Named 可能被各种各样的持久化类声明： </p>
<p>from Named n, Named m where n.name = m.name<br>注意，最后的两个查询将需要超过一个的SQL SELECT.这表明order by子句 没有对整个结果集进行正确的排序. (这也说明你不能对这样的查询使用Query.scroll()方法.) </p>
<p>15.7. where子句<br>where子句允许你将返回的实例列表的范围缩小. 如果没有指定别名，你可以使用属性名来直接引用属性: </p>
<p>from Cat where name='Fritz'<br>如果指派了别名，需要使用完整的属性名: </p>
<p>from Cat as cat where cat.name='Fritz'<br>返回名为（属性name等于）'Fritz'的Cat类的实例。 </p>
<p>select foo <br>from Foo foo, Bar bar<br>where foo.startDate = bar.date<br>将返回所有满足下面条件的Foo类的实例： 存在如下的bar的一个实例，其date属性等于 Foo的startDate属性。 复合路径表达式使得where子句非常的强大，考虑如下情况： </p>
<p>from Cat cat where cat.mate.name is not null<br>该查询将被翻译成为一个含有表连接（内连接）的SQL查询。如果你打算写像这样的查询语句 </p>
<p>from Foo foo&nbsp; <br>where foo.bar.baz.customer.address.city is not null<br>在SQL中，你为达此目的将需要进行一个四表连接的查询。 </p>
<p>=运算符不仅可以被用来比较属性的值，也可以用来比较实例： </p>
<p>from Cat cat, Cat rival where cat.mate = rival.mate<br>select cat, mate <br>from Cat cat, Cat mate<br>where cat.mate = mate<br>特殊属性（小写）id可以用来表示一个对象的唯一的标识符。（你也可以使用该对象的属性名。） </p>
<p>from Cat as cat where cat.id = 123</p>
<p>from Cat as cat where cat.mate.id = 69<br>第二个查询是有效的。此时不需要进行表连接！ </p>
<p>同样也可以使用复合标识符。比如Person类有一个复合标识符，它由country属性 与medicareNumber属性组成。 </p>
<p>from bank.Person person<br>where person.id.country = 'AU' <br>&nbsp;&nbsp;&nbsp; and person.id.medicareNumber = 123456<br>from bank.Account account<br>where account.owner.id.country = 'AU' <br>&nbsp;&nbsp;&nbsp; and account.owner.id.medicareNumber = 123456<br>第二个查询也不需要进行表连接。 </p>
<p>同样的，特殊属性class在进行多态持久化的情况下被用来存取一个实例的鉴别值（discriminator value）。 一个嵌入到where子句中的Java类的名字将被转换为该类的鉴别值。 </p>
<p>from Cat cat where cat.class = DomesticCat<br>你也可以声明一个属性的类型是组件或者复合用户类型（以及由组件构成的组件等等）。永远不要尝试使用以组件类型来结尾的路径表达式（path-expression） （与此相反，你应当使用组件的一个属性来结尾）。 举例来说，如果store.owner含有一个包含了组件的实体address </p>
<p>store.owner.address.city&nbsp;&nbsp;&nbsp; // 正确<br>store.owner.address&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // 错误!<br>一个“任意”类型有两个特殊的属性id和class, 来允许我们按照下面的方式表达一个连接（AuditLog.item 是一个属性，该属性被映射为&lt;any&gt;）。 </p>
<p>from AuditLog log, Payment payment <br>where log.item.class = 'Payment' and log.item.id = payment.id<br>注意，在上面的查询与句中，log.item.class 和 payment.class 将涉及到完全不同的数据库中的列。 </p>
<p>15.8. 表达式<br>在where子句中允许使用的表达式包括 大多数你可以在SQL使用的表达式种类: </p>
<p>数学运算符+, -, *, / </p>
<p>二进制比较运算符=, &gt;=, &lt;=, &lt;&gt;, !=, like </p>
<p>逻辑运算符and, or, not </p>
<p>in, not in, between, is null, is not null, is empty, is not empty, member of and not member of </p>
<p>"简单的" case, case ... when ... then ... else ... end,和 "搜索" case, case when ... then ... else ... end </p>
<p>字符串连接符...||... or concat(...,...) </p>
<p>current_date(), current_time(), current_timestamp() </p>
<p>second(...), minute(...), hour(...), day(...), month(...), year(...), </p>
<p>EJB-QL 3.0定义的任何函数或操作：substring(), trim(), lower(), upper(), length(), locate(), abs(), sqrt(), bit_length() </p>
<p>coalesce() 和 nullif() </p>
<p>cast(... as ...), 其第二个参数是某Hibernate类型的名字，以及extract(... from ...)，只要ANSI cast() 和 extract() 被底层数据库支持 </p>
<p>任何数据库支持的SQL标量函数，比如sign(), trunc(), rtrim(), sin() </p>
<p>JDBC参数传入 ? </p>
<p>命名参数:name, :start_date, :x1 </p>
<p>SQL 直接常量 'foo', 69, '1970-01-01 10:00:01.0' </p>
<p>Java public static final 类型的常量 eg.Color.TABBY </p>
<p>关键字in与between可按如下方法使用: </p>
<p>from DomesticCat cat where cat.name between 'A' and 'B'<br>from DomesticCat cat where cat.name in ( 'Foo', 'Bar', 'Baz' )<br>而且否定的格式也可以如下书写： </p>
<p>from DomesticCat cat where cat.name not between 'A' and 'B'<br>from DomesticCat cat where cat.name not in ( 'Foo', 'Bar', 'Baz' )<br>同样, 子句is null与is not null可以被用来测试空值(null). </p>
<p>在Hibernate配置文件中声明HQL“查询替代（query substitutions）”之后， 布尔表达式（Booleans）可以在其他表达式中轻松的使用: </p>
<p>&lt;property name="hibernate.query.substitutions"&gt;true 1, false 0&lt;/property&gt;<br>系统将该HQL转换为SQL语句时，该设置表明将用字符 1 和 0 来 取代关键字true 和 false: </p>
<p>from Cat cat where cat.alive = true<br>你可以用特殊属性size, 或是特殊函数size()测试一个集合的大小。 </p>
<p>from Cat cat where cat.kittens.size &gt; 0<br>from Cat cat where size(cat.kittens) &gt; 0<br>对于索引了（有序）的集合，你可以使用minindex 与 maxindex函数来引用到最小与最大的索引序数。 同理，你可以使用minelement 与 maxelement函数来 引用到一个基本数据类型的集合中最小与最大的元素。 </p>
<p>from Calendar cal where maxelement(cal.holidays) &gt; current date<br>from Order order where maxindex(order.items) &gt; 100<br>from Order order where minelement(order.items) &gt; 10000<br>在传递一个集合的索引集或者是元素集(elements与indices 函数) 或者传递一个子查询的结果的时候，可以使用SQL函数any, some, all, exists, in </p>
<p>select mother from Cat as mother, Cat as kit<br>where kit in elements(foo.kittens)<br>select p from NameList list, Person p<br>where p.name = some elements(list.names)<br>from Cat cat where exists elements(cat.kittens)<br>from Player p where 3 &gt; all elements(p.scores)<br>from Show show where 'fizard' in indices(show.acts)<br>注意，在Hibernate3种，这些结构变量- size, elements, indices, minindex, maxindex, minelement, maxelement - 只能在where子句中使用。 </p>
<p>一个被索引过的（有序的）集合的元素(arrays, lists, maps)可以在其他索引中被引用（只能在where子句中）： </p>
<p>from Order order where order.items[0].id = 1234<br>select person from Person person, Calendar calendar<br>where calendar.holidays['national day'] = person.birthDay<br>&nbsp;&nbsp;&nbsp; and person.nationality.calendar = calendar<br>select item from Item item, Order order<br>where order.items[ order.deliveredItemIndices[0] ] = item and order.id = 11<br>select item from Item item, Order order<br>where order.items[ maxindex(order.items) ] = item and order.id = 11<br>在[]中的表达式甚至可以是一个算数表达式。 </p>
<p>select item from Item item, Order order<br>where order.items[ size(order.items) - 1 ] = item<br>对于一个一对多的关联（one-to-many association）或是值的集合中的元素， HQL也提供内建的index()函数， </p>
<p>select item, index(item) from Order order <br>&nbsp;&nbsp;&nbsp; join order.items item<br>where index(item) &lt; 5<br>如果底层数据库支持标量的SQL函数，它们也可以被使用 </p>
<p>from DomesticCat cat where upper(cat.name) like 'FRI%'<br>如果你还不能对所有的这些深信不疑，想想下面的查询。如果使用SQL，语句长度会增长多少，可读性会下降多少： </p>
<p>select cust<br>from Product prod,<br>&nbsp;&nbsp;&nbsp; Store store<br>&nbsp;&nbsp;&nbsp; inner join store.customers cust<br>where prod.name = 'widget'<br>&nbsp;&nbsp;&nbsp; and store.location.name in ( 'Melbourne', 'Sydney' )<br>&nbsp;&nbsp;&nbsp; and prod = all elements(cust.currentOrder.lineItems)<br>提示: 会像如下的语句 </p>
<p>SELECT cust.name, cust.address, cust.phone, cust.id, cust.current_order<br>FROM customers cust,<br>&nbsp;&nbsp;&nbsp; stores store,<br>&nbsp;&nbsp;&nbsp; locations loc,<br>&nbsp;&nbsp;&nbsp; store_customers sc,<br>&nbsp;&nbsp;&nbsp; product prod<br>WHERE prod.name = 'widget'<br>&nbsp;&nbsp;&nbsp; AND store.loc_id = loc.id<br>&nbsp;&nbsp;&nbsp; AND loc.name IN ( 'Melbourne', 'Sydney' )<br>&nbsp;&nbsp;&nbsp; AND sc.store_id = store.id<br>&nbsp;&nbsp;&nbsp; AND sc.cust_id = cust.id<br>&nbsp;&nbsp;&nbsp; AND prod.id = ALL(<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; SELECT item.prod_id<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; FROM line_items item, orders o<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; WHERE item.order_id = o.id<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; AND cust.current_order = o.id<br>&nbsp;&nbsp;&nbsp; )<br>15.9. order by子句<br>查询返回的列表(list)可以按照一个返回的类或组件（components)中的任何属性（property）进行排序： </p>
<p>from DomesticCat cat<br>order by cat.name asc, cat.weight desc, cat.birthdate<br>可选的asc或desc关键字指明了按照升序或降序进行排序. </p>
<p>15.10. group by子句<br>一个返回聚集值(aggregate values)的查询可以按照一个返回的类或组件（components)中的任何属性（property）进行分组： </p>
<p>select cat.color, sum(cat.weight), count(cat) <br>from Cat cat<br>group by cat.color<br>select foo.id, avg(name), max(name) <br>from Foo foo join foo.names name<br>group by foo.id<br>having子句在这里也允许使用. </p>
<p>select cat.color, sum(cat.weight), count(cat) <br>from Cat cat<br>group by cat.color <br>having cat.color in (eg.Color.TABBY, eg.Color.BLACK)<br>如果底层的数据库支持的话(例如不能在MySQL中使用)，SQL的一般函数与聚集函数也可以出现 在having与order by 子句中。 </p>
<p>select cat<br>from Cat cat<br>&nbsp;&nbsp;&nbsp; join cat.kittens kitten<br>group by cat<br>having avg(kitten.weight) &gt; 100<br>order by count(kitten) asc, sum(kitten.weight) desc<br>注意group by子句与 order by子句中都不能包含算术表达式（arithmetic expressions）. </p>
<p>15.11. 子查询<br>对于支持子查询的数据库，Hibernate支持在查询中使用子查询。一个子查询必须被圆括号包围起来（经常是SQL聚集函数的圆括号）。 甚至相互关联的子查询（引用到外部查询中的别名的子查询）也是允许的。 </p>
<p>from Cat as fatcat <br>where fatcat.weight &gt; ( <br>&nbsp;&nbsp;&nbsp; select avg(cat.weight) from DomesticCat cat <br>)<br>from DomesticCat as cat <br>where cat.name = some ( <br>&nbsp;&nbsp;&nbsp; select name.nickName from Name as name <br>)<br>from Cat as cat <br>where not exists ( <br>&nbsp;&nbsp;&nbsp; from Cat as mate where mate.mate = cat <br>)<br>from DomesticCat as cat <br>where cat.name not in ( <br>&nbsp;&nbsp;&nbsp; select name.nickName from Name as name <br>)<br>在select列表中包含一个表达式以上的子查询，你可以使用一个元组构造符（tuple constructors）： </p>
<p>from Cat as cat <br>where not ( cat.name, cat.color ) in ( <br>&nbsp;&nbsp;&nbsp; select cat.name, cat.color from DomesticCat cat <br>)<br>注意在某些数据库中（不包括Oracle与HSQL），你也可以在其他语境中使用元组构造符， 比如查询用户类型的组件与组合： </p>
<p>from Person where name = ('Gavin', 'A', 'King')<br>该查询等价于更复杂的： </p>
<p>from Person where name.first = 'Gavin' and name.initial = 'A' and name.last = 'King')<br>有两个很好的理由使你不应当作这样的事情：首先，它不完全适用于各个数据库平台；其次，查询现在依赖于映射文件中属性的顺序。 </p>
<p>15.12. HQL示例<br>Hibernate查询可以非常的强大与复杂。实际上，Hibernate的一个主要卖点就是查询语句的威力。这里有一些例子，它们与我在最近的 一个项目中使用的查询非常相似。注意你能用到的大多数查询比这些要简单的多！ </p>
<p>下面的查询对于某个特定的客户的所有未支付的账单，在给定给最小总价值的情况下，返回订单的id，条目的数量和总价值， 返回值按照总价值的结果进行排序。为了决定价格，查询使用了当前目录。作为转换结果的SQL查询，使用了ORDER, ORDER_LINE, PRODUCT, CATALOG 和PRICE 库表。 </p>
<p>select order.id, sum(price.amount), count(item)<br>from Order as order<br>&nbsp;&nbsp;&nbsp; join order.lineItems as item<br>&nbsp;&nbsp;&nbsp; join item.product as product,<br>&nbsp;&nbsp;&nbsp; Catalog as catalog<br>&nbsp;&nbsp;&nbsp; join catalog.prices as price<br>where order.paid = false<br>&nbsp;&nbsp;&nbsp; and order.customer = :customer<br>&nbsp;&nbsp;&nbsp; and price.product = product<br>&nbsp;&nbsp;&nbsp; and catalog.effectiveDate &lt; sysdate<br>&nbsp;&nbsp;&nbsp; and catalog.effectiveDate &gt;= all (<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; select cat.effectiveDate <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; from Catalog as cat<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; where cat.effectiveDate &lt; sysdate<br>&nbsp;&nbsp;&nbsp; )<br>group by order<br>having sum(price.amount) &gt; :minAmount<br>order by sum(price.amount) desc<br>这简直是一个怪物！实际上，在现实生活中，我并不热衷于子查询，所以我的查询语句看起来更像这个： </p>
<p>select order.id, sum(price.amount), count(item)<br>from Order as order<br>&nbsp;&nbsp;&nbsp; join order.lineItems as item<br>&nbsp;&nbsp;&nbsp; join item.product as product,<br>&nbsp;&nbsp;&nbsp; Catalog as catalog<br>&nbsp;&nbsp;&nbsp; join catalog.prices as price<br>where order.paid = false<br>&nbsp;&nbsp;&nbsp; and order.customer = :customer<br>&nbsp;&nbsp;&nbsp; and price.product = product<br>&nbsp;&nbsp;&nbsp; and catalog = :currentCatalog<br>group by order<br>having sum(price.amount) &gt; :minAmount<br>order by sum(price.amount) desc<br>下面一个查询计算每一种状态下的支付的数目，除去所有处于AWAITING_APPROVAL状态的支付，因为在该状态下 当前的用户作出了状态的最新改变。该查询被转换成含有两个内连接以及一个相关联的子选择的SQL查询，该查询使用了表 PAYMENT, PAYMENT_STATUS 以及 PAYMENT_STATUS_CHANGE。 </p>
<p>select count(payment), status.name <br>from Payment as payment <br>&nbsp;&nbsp;&nbsp; join payment.currentStatus as status<br>&nbsp;&nbsp;&nbsp; join payment.statusChanges as statusChange<br>where payment.status.name &lt;&gt; PaymentStatus.AWAITING_APPROVAL<br>&nbsp;&nbsp;&nbsp; or (<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; statusChange.timeStamp = ( <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; select max(change.timeStamp) <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; from PaymentStatusChange change <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; where change.payment = payment<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; )<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; and statusChange.user &lt;&gt; :currentUser<br>&nbsp;&nbsp;&nbsp; )<br>group by status.name, status.sortOrder<br>order by status.sortOrder<br>如果我把statusChanges实例集映射为一个列表（list）而不是一个集合（set）, 书写查询语句将更加简单. </p>
<p>select count(payment), status.name <br>from Payment as payment<br>&nbsp;&nbsp;&nbsp; join payment.currentStatus as status<br>where payment.status.name &lt;&gt; PaymentStatus.AWAITING_APPROVAL<br>&nbsp;&nbsp;&nbsp; or payment.statusChanges[ maxIndex(payment.statusChanges) ].user &lt;&gt; :currentUser<br>group by status.name, status.sortOrder<br>order by status.sortOrder<br>下面一个查询使用了MS SQL Server的 isNull()函数用以返回当前用户所属组织的组织帐号及组织未支付的账。 它被转换成一个对表ACCOUNT, PAYMENT, PAYMENT_STATUS, ACCOUNT_TYPE, ORGANIZATION 以及 ORG_USER进行的三个内连接， 一个外连接和一个子选择的SQL查询。 </p>
<p>select account, payment<br>from Account as account<br>&nbsp;&nbsp;&nbsp; left outer join account.payments as payment<br>where :currentUser in elements(account.holder.users)<br>&nbsp;&nbsp;&nbsp; and PaymentStatus.UNPAID = isNull(payment.currentStatus.name, PaymentStatus.UNPAID)<br>order by account.type.sortOrder, account.accountNumber, payment.dueDate<br>对于一些数据库，我们需要弃用（相关的）子选择。 </p>
<p>select account, payment<br>from Account as account<br>&nbsp;&nbsp;&nbsp; join account.holder.users as user<br>&nbsp;&nbsp;&nbsp; left outer join account.payments as payment<br>where :currentUser = user<br>&nbsp;&nbsp;&nbsp; and PaymentStatus.UNPAID = isNull(payment.currentStatus.name, PaymentStatus.UNPAID)<br>order by account.type.sortOrder, account.accountNumber, payment.dueDate<br>15.13. 批量的UPDATE &amp; DELETE语句<br>HQL现在支持UPDATE与DELETE语句. 查阅 第 14.3 节 “大批量更新/删除（Bulk update/delete）” 以获得更多信息。 </p>
<p>15.14. 小技巧 &amp; 小窍门<br>你可以统计查询结果的数目而不必实际的返回他们： </p>
<p>( (Integer) session.iterate("select count(*) from ....").next() ).intValue()<br>若想根据一个集合的大小来进行排序，可以使用如下的语句： </p>
<p>select usr.id, usr.name<br>from User as usr <br>&nbsp;&nbsp;&nbsp; left join usr.messages as msg<br>group by usr.id, usr.name<br>order by count(msg)<br>如果你的数据库支持子选择，你可以在你的查询的where子句中为选择的大小（selection size）指定一个条件: </p>
<p>from User usr where size(usr.messages) &gt;= 1<br>如果你的数据库不支持子选择语句，使用下面的查询： </p>
<p>select usr.id, usr.name<br>from User usr.name<br>&nbsp;&nbsp;&nbsp; join usr.messages msg<br>group by usr.id, usr.name<br>having count(msg) &gt;= 1<br>因为内连接（inner join）的原因，这个解决方案不能返回含有零个信息的User 类的实例, 所以这种情况下使用下面的格式将是有帮助的: </p>
<p>select usr.id, usr.name<br>from User as usr<br>&nbsp;&nbsp;&nbsp; left join usr.messages as msg<br>group by usr.id, usr.name<br>having count(msg) = 0<br>JavaBean的属性可以被绑定到一个命名查询（named query）的参数上： </p>
<p>Query q = s.createQuery("from foo Foo as foo where foo.name=:name and foo.size=:size");<br>q.setProperties(fooBean); // fooBean包含方法getName()与getSize()<br>List foos = q.list();<br>通过将接口Query与一个过滤器（filter）一起使用，集合（Collections）是可以分页的： </p>
<p>Query q = s.createFilter( collection, "" ); // 一个简单的过滤器<br>q.setMaxResults(PAGE_SIZE);<br>q.setFirstResult(PAGE_SIZE * pageNumber);<br>List page = q.list();<br>通过使用查询过滤器（query filter）可以将集合（Collection）的原素分组或排序: </p>
<p>Collection orderedCollection = s.filter( collection, "order by this.amount" );<br>Collection counts = s.filter( collection, "select this.type, count(this) group by this.type" );<br>不用通过初始化，你就可以知道一个集合（Collection）的大小： </p>
<p>( (Integer) session.iterate("select count(*) from ....").next() ).intValue();<br>&nbsp;</p>