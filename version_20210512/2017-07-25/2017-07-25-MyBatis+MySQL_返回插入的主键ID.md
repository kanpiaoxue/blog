#MyBatis+MySQL 返回插入的主键ID
###发表时间：2017-07-25
###分类：java,mybatis
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2386822" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2386822</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>来源地址：&nbsp;<a href="http://chenzhou123520.iteye.com/blog/1849881">http://chenzhou123520.iteye.com/blog/1849881</a></p> 
 <p>&nbsp;</p> 
 <p>== 下面的内容是我从别人的 BLOG 转载过来的，用以自己收藏================================</p> 
 <p>&nbsp;</p> 
 <p>需求：使用MyBatis往MySQL数据库中插入一条记录后，需要返回该条记录的自增主键值。</p> 
 <p>&nbsp;</p> 
 <p>方法：在mapper中指定keyProperty属性，示例如下：</p> 
 <div id="" class="dp-highlighter" style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; width: 679px; overflow: auto; margin-left: 9px; padding: 1px;"> 
  <div class="bar"> 
   <div class="tools" style="padding: 3px; margin: 0px; font-weight: bold;">
    Xml代码&nbsp;&nbsp;
    <a style="color: #108ac6;" title="收藏这段代码"><img class="star" src="http://chenzhou123520.iteye.com/images/icon_star.png" alt="收藏代码"></a> 
   </div> 
  </div> 
  <ol class="dp-xml" style="margin-bottom: 1px; padding-top: 2px; padding-bottom: 2px; border: 1px solid #d1d7dc; color: #2b91af;" start="1"> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;"><span class="tag" style="color: #006699; font-weight: bold;">&lt;</span><span class="tag-name" style="color: #006699; font-weight: bold;">insert</span>&nbsp;<span class="attribute" style="color: red;">id</span>=<span class="attribute-value" style="color: blue;">"insertAndGetId"</span>&nbsp;<span class="attribute" style="color: red;">useGeneratedKeys</span>=<span class="attribute-value" style="color: blue;">"true"</span>&nbsp;<span class="attribute" style="color: red;">keyProperty</span>=<span class="attribute-value" style="color: blue;">"userId"</span>&nbsp;<span class="attribute" style="color: red;">parameterType</span>=<span class="attribute-value" style="color: blue;">"com.chenzhou.mybatis.User"</span><span class="tag" style="color: #006699; font-weight: bold;">&gt;</span>&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">&nbsp;&nbsp;&nbsp;&nbsp;insert&nbsp;into&nbsp;user(userName,password,comment)&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">&nbsp;&nbsp;&nbsp;&nbsp;values(#{userName},#{password},#{comment})&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;"><span class="tag" style="color: #006699; font-weight: bold;">&lt;/</span><span class="tag-name" style="color: #006699; font-weight: bold;">insert</span><span class="tag" style="color: #006699; font-weight: bold;">&gt;</span>&nbsp;&nbsp;</span></li> 
  </ol> 
 </div> 
 <p>&nbsp;如上所示，我们在insert中指定了keyProperty="userId"，其中userId代表插入的User对象的主键属性。</p> 
 <p>&nbsp;</p> 
 <p>User.java</p> 
 <div id="" class="dp-highlighter" style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; width: 679px; overflow: auto; margin-left: 9px; padding: 1px;"> 
  <div class="bar"> 
   <div class="tools" style="padding: 3px; margin: 0px; font-weight: bold;">
    Java代码&nbsp;&nbsp;
    <a style="color: #108ac6;" title="收藏这段代码"><img class="star" src="http://chenzhou123520.iteye.com/images/icon_star.png" alt="收藏代码"></a> 
   </div> 
  </div> 
  <ol class="dp-j" style="margin-bottom: 1px; padding-top: 2px; padding-bottom: 2px; border: 1px solid #d1d7dc; color: #2b91af;" start="1"> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;"><span class="keyword" style="color: #7f0055; font-weight: bold;">public</span>&nbsp;<span class="keyword" style="color: #7f0055; font-weight: bold;">class</span>&nbsp;User&nbsp;{&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword" style="color: #7f0055; font-weight: bold;">private</span>&nbsp;<span class="keyword" style="color: #7f0055; font-weight: bold;">int</span>&nbsp;userId;&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword" style="color: #7f0055; font-weight: bold;">private</span>&nbsp;String&nbsp;userName;&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword" style="color: #7f0055; font-weight: bold;">private</span>&nbsp;String&nbsp;password;&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword" style="color: #7f0055; font-weight: bold;">private</span>&nbsp;String&nbsp;comment;&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">&nbsp;&nbsp;&nbsp;&nbsp;<span class="comment" style="color: #008200; padding: 0px; margin: 0px; width: auto; border: 0px;">//setter&nbsp;and&nbsp;getter</span>&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">}&nbsp;&nbsp;</span></li> 
  </ol> 
 </div> 
 <p>&nbsp;UserDao.java</p> 
 <div id="" class="dp-highlighter" style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; width: 679px; overflow: auto; margin-left: 9px; padding: 1px;"> 
  <div class="bar"> 
   <div class="tools" style="padding: 3px; margin: 0px; font-weight: bold;">
    Java代码&nbsp;&nbsp;
    <a style="color: #108ac6;" title="收藏这段代码"><img class="star" src="http://chenzhou123520.iteye.com/images/icon_star.png" alt="收藏代码"></a> 
   </div> 
  </div> 
  <ol class="dp-j" style="margin-bottom: 1px; padding-top: 2px; padding-bottom: 2px; border: 1px solid #d1d7dc; color: #2b91af;" start="1"> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;"><span class="keyword" style="color: #7f0055; font-weight: bold;">public</span>&nbsp;<span class="keyword" style="color: #7f0055; font-weight: bold;">interface</span>&nbsp;UserDao&nbsp;{&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword" style="color: #7f0055; font-weight: bold;">public</span>&nbsp;<span class="keyword" style="color: #7f0055; font-weight: bold;">int</span>&nbsp;insertAndGetId(User&nbsp;user);&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">}&nbsp;&nbsp;</span></li> 
  </ol> 
 </div> 
 <p>&nbsp;测试：</p> 
 <div id="" class="dp-highlighter" style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; width: 679px; overflow: auto; margin-left: 9px; padding: 1px;"> 
  <div class="bar"> 
   <div class="tools" style="padding: 3px; margin: 0px; font-weight: bold;">
    Java代码&nbsp;&nbsp;
    <a style="color: #108ac6;" title="收藏这段代码"><img class="star" src="http://chenzhou123520.iteye.com/images/icon_star.png" alt="收藏代码"></a> 
   </div> 
  </div> 
  <ol class="dp-j" style="margin-bottom: 1px; padding-top: 2px; padding-bottom: 2px; border: 1px solid #d1d7dc; color: #2b91af;" start="1"> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">User&nbsp;user&nbsp;=&nbsp;<span class="keyword" style="color: #7f0055; font-weight: bold;">new</span>&nbsp;User();&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">user.setUserName(<span class="string" style="color: blue;">"chenzhou"</span>);&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">user.setPassword(<span class="string" style="color: blue;">"xxxx"</span>);&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">user.setComment(<span class="string" style="color: blue;">"测试插入数据返回主键功能"</span>);&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">System.out.println(<span class="string" style="color: blue;">"插入前主键为："</span>+user.getUserId());&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">userDao.insertAndGetId(user);<span class="comment" style="color: #008200; padding: 0px; margin: 0px; width: auto; border: 0px;">//插入操作</span>&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">System.out.println(<span class="string" style="color: blue;">"插入后主键为："</span>+user.getUserId());&nbsp;&nbsp;</span></li> 
  </ol> 
 </div> 
 <p>&nbsp;输出：</p> 
 <div id="" class="dp-highlighter" style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; width: 679px; overflow: auto; margin-left: 9px; padding: 1px;"> 
  <div class="bar"> 
   <div class="tools" style="padding: 3px; margin: 0px; font-weight: bold;">
    Shell代码&nbsp;&nbsp;
    <a style="color: #108ac6;" title="收藏这段代码"><img class="star" src="http://chenzhou123520.iteye.com/images/icon_star.png" alt="收藏代码"></a> 
   </div> 
  </div> 
  <ol class="dp-default" style="margin-bottom: 1px; padding-top: 2px; padding-bottom: 2px; border: 1px solid #d1d7dc; color: #2b91af;" start="1"> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">插入前主键为：<span class="number" style="color: #c00000;">0</span>&nbsp;&nbsp;</span></li> 
   <li style="margin-bottom: 0px; margin-left: 38px; padding-left: 10px; border-left: 1px solid #d1d7dc; background-color: #fafafa; line-height: 18px;"><span style="color: black;">插入后主键为：<span class="number" style="color: #c00000;">15</span>&nbsp;&nbsp;</span></li> 
  </ol> 
 </div> 
 <p>&nbsp;查询数据库：</p> 
 <p><img src="http://dl.iteye.com/upload/picture/pic/124990/efddf3ae-4485-3287-aed3-bfe5a65b8b0f.jpg" alt="" width="616" height="61"></p> 
 <p>&nbsp;</p> 
 <p>如上所示，刚刚插入的记录主键id为15</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>