#javascript 的输入框输入多条英文逗号分隔记录触发 ajax 的技巧
###发表时间：2017-10-20
###分类：javascript,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2397120" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2397120</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>我们有的时候会让用户在一个 html 是 textarea 的空间中输入很多记录，如：员工的编号。随着记录是输入需要和后台进行交互。但是我们希望交互的次数是合理的，减少后台系统的压力。</p> 
 <p>场景举例：我们有一个 web 页面需要用户在textarea输入人员的手机号码，可以输入多个号码使用英文逗号分隔，在textarea的键盘 keyup 事件中我们希望用户输入手机号码（一般最短的是11位，可能加上前面的国际编号+86等手机号码会超过11位的长度），当输入的内容大于等于11的时候想后台发起一次请求。如果用户在这个号码之后继续输入英文分隔符，不发起后台请求，继续当输入的内容大于等于11的时候想后台发起一次请求。依次循环检查输入内容的合法性，向后台发起请求。我们要求请求数量尽可能的少。</p> 
 <p>我这里假设使用的是 jquery 框架，代码如下：</p> 
 <pre name="code" class="js">$('#textareaId').bind('keyup', function() {
    var teamMembersEmpIdsRegex = /^(?:\d{11,},?)+$/;
    var val = $.trim($(this).val());
    var size = val.length;
    var postion = val.lastIndexOf(',');
    var flag = (postion == size -1); //发现逗号作为字符串的结尾
    // teamMembersEmpIdsRegex 正则表达式中指定了触发的字符串长度
    // 字符串结尾是英文逗号的时候，不出发 ajax 请求
    if (teamMembersEmpIdsRegex.test(val) &amp;&amp; !flag) {
        debug('hello11==world ', val,' flag:',flag,'  val.lastIndexOf(','):',val.lastIndexOf(',') ,'  val.length:',val.length); // TODO
        // ajax code here
    }
});</pre> 
 <p>重点在两处：正则表达式和对最后结尾是英文逗号的判断。&nbsp;</p> 
</div>