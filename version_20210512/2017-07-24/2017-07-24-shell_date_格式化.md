#shell date 格式化
###发表时间：2017-07-24
###分类：shell
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2386555" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2386555</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>从别的地方找来的：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">1-  echo `date "+%Y-%m-%d %H:%M:%S"`

2014-11-13 15:06:26

 

2-  echo `date "+%y-%m-%d %H:%M:%S"`

14-11-13 15:06:51

注意: "+%y-%m-%d %H:%M:%S" 大小写

给定的格式FORMAT 控制着输出，解释序列如下：

  %%    一个文字的 %
  %a    当前locale 的星期名缩写(例如： 日，代表星期日)
  %A    当前locale 的星期名全称 (如：星期日)
  %b    当前locale 的月名缩写 (如：一，代表一月)
  %B    当前locale 的月名全称 (如：一月)
  %c    当前locale 的日期和时间 (如：2005年3月3日 星期四 23:05:25)
  %C    世纪；比如 %Y，通常为省略当前年份的后两位数字(例如：20)
  %d    按月计的日期(例如：01)
  %D    按月计的日期；等于%m/%d/%y
  %e    按月计的日期，添加空格，等于%_d
  %F    完整日期格式，等价于 %Y-%m-%d
  %g    ISO-8601 格式年份的最后两位 (参见%G)
  %G    ISO-8601 格式年份 (参见%V)，一般只和 %V 结合使用
  %h    等于%b
  %H    小时(00-23)
  %I    小时(00-12)
  %c    按年计的日期(001-366)
  %k    时(0-23)
  %l    时(1-12)
  %m    月份(01-12)
  %M    分(00-59)
  %n    换行
  %N    纳秒(000000000-999999999)
  %p    当前locale 下的"上午"或者"下午"，未知时输出为空
  %P    与%p 类似，但是输出小写字母
  %r    当前locale 下的 12 小时时钟时间 (如：11:11:04 下午)
  %R    24 小时时间的时和分，等价于 %H:%M
  %s    自UTC 时间 1970-01-01 00:00:00 以来所经过的秒数
  %S    秒(00-60)
  %t    输出制表符 Tab
  %T    时间，等于%H:%M:%S
  %u    星期，1 代表星期一
  %U    一年中的第几周，以周日为每星期第一天(00-53)
  %V    ISO-8601 格式规范下的一年中第几周，以周一为每星期第一天(01-53)
  %w    一星期中的第几日(0-6)，0 代表周一
  %W    一年中的第几周，以周一为每星期第一天(00-53)
  %x    当前locale 下的日期描述 (如：12/31/99)
  %X    当前locale 下的时间描述 (如：23:13:48)
  %y    年份最后两位数位 (00-99)
  %Y    年份
  %z +hhmm              数字时区(例如，-0400)
  %:z +hh:mm            数字时区(例如，-04:00)
  %::z +hh:mm:ss        数字时区(例如，-04:00:00)
  %:::z                 数字时区带有必要的精度 (例如，-04，+05:30)
  %Z                    按字母表排序的时区缩写 (例如，EDT)</pre> 
 <p>&nbsp;来自：&nbsp;<a href="http://www.cnblogs.com/galoishelley/p/4095022.html">http://www.cnblogs.com/galoishelley/p/4095022.html</a></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">date命令的帮助信息
 [root@localhost source]# date --help
用法：date [选项]... [+格式]
　或：date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]
以给定的格式显示当前时间，或是设置系统日期。

  -d,--date=字符串              显示指定字符串所描述的时间，而非当前时间
  -f,--file=日期文件            类似--date，从日期文件中按行读入时间描述
  -r, --reference=文件          显示文件指定文件的最后修改时间
  -R, --rfc-2822                以RFC 2822格式输出日期和时间
                                例如：2006年8月7日，星期一 12:34:56 -0600
      --rfc-3339=TIMESPEC       以RFC 3339 格式输出日期和时间。
                                TIMESPEC=`date'，`seconds'，或 `ns' 
                                表示日期和时间的显示精度。
                                日期和时间单元由单个的空格分开：
                                2006-08-07 12:34:56-06:00
  -s, --set=字符串              设置指定字符串来分开时间
  -u, --utc, --universal        输出或者设置协调的通用时间
      --help            显示此帮助信息并退出
      --version         显示版本信息并退出

默认情况下，日期的数字区域以0 填充。
以下可选标记可以跟在"%"后:

  - (连字符)不填充该域
  _ (下划线)以空格填充
  0 (数字0)以0 填充
  ^ 如果可能，使用大写字母
  # 如果可能，使用相反的大小写

在任何标记之后还允许一个可选的域宽度指定，它是一个十进制数字。
作为一个可选的修饰声明，它可以是E，在可能的情况下使用本地环境关联的
表示方式；或者是O，在可能的情况下使用本地环境关联的数字符号。</pre> 
 <p>来自： <a href="http://blog.csdn.net/jk110333/article/details/8590746/">http://blog.csdn.net/jk110333/article/details/8590746/</a>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>