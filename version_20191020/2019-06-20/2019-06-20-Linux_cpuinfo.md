#Linux cpuinfo
###发表时间：2019-06-20
###分类：Linux,经验,shell
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2441995" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2441995</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>参考地址：&nbsp;<a href="https://blog.51cto.com/icooke/757555">https://blog.51cto.com/icooke/757555</a></p> 
 <p>通过cat /proc/cpuinfo来检查</p> 
 <p>&nbsp;</p> 
 <p>#逻辑CPU个数</p> 
 <p>cat /proc/cpuinfo | grep "processor" | wc -l</p> 
 <p>&nbsp;</p> 
 <p>#物理CPU个数：</p> 
 <p>cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l</p> 
 <p>&nbsp;</p> 
 <p>#每个物理CPU中Core的个数：</p> 
 <p>cat /proc/cpuinfo | grep "cpu cores" | uniq | awk -F: '{print $2}'</p> 
 <p>&nbsp;</p> 
 <p>#每个物理CPU中逻辑CPU(可能是core, threads或both)的个数：</p> 
 <p>cat /proc/cpuinfo | grep "siblings"</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>processor 条目包括这一逻辑处理器的唯一标识符。</p> 
 <p>physical id 条目包括每个物理封装的唯一标识符。</p> 
 <p>core id 条目保存每个内核的唯一标识符。</p> 
 <p>siblings 条目列出了位于相同物理封装中的逻辑处理器的数量。</p> 
 <p>cpu cores 条目包含位于相同物理封装中的内核数量。</p> 
 <p>如果处理器为英特尔处理器，则 vendor id 条目中的字符串是 GenuineIntel。</p> 
</div>