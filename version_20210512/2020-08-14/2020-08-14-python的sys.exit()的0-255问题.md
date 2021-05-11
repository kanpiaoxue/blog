#python的sys.exit()的0-255问题
###发表时间：2020-08-14
###分类：python,shell,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2516291" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2516291</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>最近写了一个python脚本用到了sys.exit(exit_code) ，遇到一个奇怪的问题。当exit_code=256的时候，预期python调用sys.exit(exit_code) 之后退出进程之后的退出码应该是256，可实际情况退出码是0. 这引发我这边的程序异常，判断任务是运行成功的。</p> 
 <p>问题的根节就在：sys.exit(256) 的时候python的退出码是0. 我又验证了一下，sys.exit(exit_code)&nbsp; 中的exit_code是256的整数倍的时候，python进程退出码全部是0.</p> 
 <p>找了一些资料，发现这个是python自身的限制问题。&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>如下的资料：</p> 
 <p><a href="http://hk.uwenku.com/question/p-tfxlltaj-bke.html">http://hk.uwenku.com/question/p-tfxlltaj-bke.html</a></p> 
 <p><a href="https://stackoverflow.com/questions/4448339/how-to-bypass-the-0-255-range-limit-for-sys-exit-in-python">https://stackoverflow.com/questions/4448339/how-to-bypass-the-0-255-range-limit-for-sys-exit-in-python</a></p> 
 <p>&nbsp;</p> 
 <p>该如何处理 sys.exit(256)&nbsp; python退出码是 0 的问题？ 保证程序能够按预期退出？</p> 
 <p>做法：</p> 
 <p>1、可以记录一下退出码到日志，然后让python抛出异常，来退出python进程</p> 
 <p>2、使用sys.exit(exit_code) 的时候，让exit_code只能是 0 或者 1 ，避免其他退出码情况的出现</p> 
 <p>3、自己处理一下exit_code=256倍数的情况</p> 
 <p>4、参考上面的参考资料里面的做法，对exit_code进行移位处理</p> 
 <p>&nbsp;</p> 
</div>