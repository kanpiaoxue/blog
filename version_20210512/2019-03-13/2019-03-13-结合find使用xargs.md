#结合find使用xargs
###发表时间：2019-03-13
###分类：shell,Linux,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2438810" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2438810</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>结合find使用xargs xargs和find算是一对死党。两者结合使用可以让任务变得更轻松。不过人们通常却是以一</p> 
 <p>种错误的组合方式使用它们。例如:</p> 
 <p>&nbsp; &nbsp; &nbsp;$ find . -type f -name "*.txt"&nbsp; -print | xargs rm -f</p> 
 <p>这样做很危险。有时可能会删除不必要删除的文件。我们没法预测分隔find命令输出结果 的定界符究竟是什么('\n'或者' ')。很多文件名中都可能会包含空格符(' ')，因此xargs 很可能会误认为它们是定界符(例如，hell text.txt会被xargs误解为hell和text.txt)。</p> 
 <p>只要我们把find的输出作为xargs的输入，就必须将 -print0与find结合使用，以字符null ('\0')来分隔输出。</p> 
 <p>用find匹配并列出所有的 .txt文件，然后用xargs将这些文件删除:&nbsp;</p> 
 <p>$ find . -type f -name "*.txt" -print0 | xargs -0 rm -f</p> 
 <p>这样就可以删除所有的.txt文件。xargs -0将\0作为输入定界符。</p> 
 <p>&nbsp;</p> 
 <p>删除当前文件下面超过2天没有发生改变的文件夹</p> 
 <p>$ find . -type d -ctime +2 -print0 | xargs -0 rm -rf</p> 
 <p>&nbsp;</p> 
</div>