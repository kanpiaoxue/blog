#(理解Linux机器负载)Understanding the Load Average on Linux and Other Unix-like Systems
###发表时间：2018-07-24
###分类：Linux,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2427434" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2427434</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>《Understanding the Load Average on Linux and Other Unix-like Systems》<br>参考地址：</p> 
 <p><a href="https://www.howtogeek.com/194642/understanding-the-load-average-on-linux-and-other-unix-like-systems/">https://www.howtogeek.com/194642/understanding-the-load-average-on-linux-and-other-unix-like-systems/</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">Linux, Mac, and other Unix-like systems display “load average” numbers. These numbers tell you how busy your system’s CPU, disk, and other resources are. They’re not self-explanatory at first, but it’s easy to become familiar with them.</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">Whether you’re using a Linux desktop or server, a Linux-based router firmware, a NAS system based on Linux or BSD, or even Mac OS X, you’ve probably seen a “load average” measurement somewhere.</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">&nbsp;</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">On&nbsp;<a style="background-color: transparent; color: #114491; display: inline;" href="https://www.howtogeek.com/182649/htg-explains-what-is-unix/">Unix-like systems</a>, including Linux, the system load is a measurement of the computational work the system is performing. This measurement is displayed as a number. A completely idle computer has a load average of 0. Each running process either using or waiting for CPU resources adds 1 to the load average. So, if your system has a load of 5, five processes are either using or waiting for the CPU.</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">Unix systems traditionally just counted processes waiting for the CPU, but Linux also counts processes waiting for other resources — for example, processes waiting to read from or write to the disk.</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">On its own, the load number doesn’t mean too much. A computer might have a load of 0 one split-second, and a load of 5 the next split-second as several processes use the CPU. Even if you could see the load at any given time, that number would be basically meaningless.</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">That’s why Unix-like systems don’t display the current load. They display the load average — an average of the computer’s load over several periods of time. This allows you to see how much work your computer has been performing.</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">&nbsp;</p> 
 <h2 style="clear: both; font-size: 21px; color: #404040; font-family: 'Open Sans', sans-serif;">Finding the Load Average</h2> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;"><span style="font-weight: 600;">RELATED:</span>&nbsp;<a style="background-color: transparent; color: #114491; display: inline;" href="https://www.howtogeek.com/107217/how-to-manage-processes-from-the-linux-terminal-10-commands-you-need-to-know/"><span style="font-weight: 600;"><em style="">How to Manage Processes from the Linux Terminal: 10 Commands You Need to Know</em></span></a></p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">The load average is shown in many different graphical and terminal utilities, including in&nbsp;<a style="background-color: transparent; color: #114491; display: inline;" href="https://www.howtogeek.com/107217/how-to-manage-processes-from-the-linux-terminal-10-commands-you-need-to-know/">the top command</a>&nbsp;and in the graphical GNOME System Monitor tool. However, the easiest, most standardized way to see your load average is to&nbsp;<a style="background-color: transparent; color: #114491; display: inline;" href="https://www.howtogeek.com/194186/bragging-rights-how-to-find-your-computers-uptime-and-installation-date/">run the uptime command</a>in a terminal. This command shows your computer’s load average as well as how long it’s been powered on.</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">The uptime command works on Linux, Mac OS X, and other Unix-like systems. If you’re using a Linux or BSD-based device with a web interface — such as the DD-WRT router firmware or&nbsp;<a style="background-color: transparent; color: #114491; display: inline;" href="https://www.howtogeek.com/190835/how-to-turn-an-old-pc-into-a-home-file-server/">FreeNAS NAS system</a>&nbsp;— you’ll probably see the load average somewhere in its status page.</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">&nbsp;</p> 
 <h2 style="clear: both; font-size: 21px; color: #404040; font-family: 'Open Sans', sans-serif;">Understanding the Load Average Output</h2> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">The first time you see a load average, the numbers look fairly meaningless. Here’s an example load average readout:</p> 
 <blockquote style=""> 
  <p style="margin-top: 10px; margin-bottom: 10px;">load average: 1.05, 0.70, 5.09</p> 
 </blockquote> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">From left to right, these numbers show you the average load over the last one minute, the last five minutes, and the last fifteen minutes. In other words, the above output means:</p> 
 <blockquote style=""> 
  <p style="margin-top: 10px; margin-bottom: 10px;">load average over the last 1 minute: 1.05</p> 
  <p style="margin-top: 10px; margin-bottom: 10px;">load average over the last 5 minutes: 0.70</p> 
  <p style="margin-top: 10px; margin-bottom: 10px;">load average over the last 15 minutes: 5.09</p> 
 </blockquote> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">The time periods are omitted to save space. Once you’re familiar with the time periods, you can quickly glance at the load average numbers and understand what they mean.</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">&nbsp;</p> 
 <h2 style="clear: both; font-size: 21px; color: #404040; font-family: 'Open Sans', sans-serif;">What Do the Numbers Mean, Exactly?</h2> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">Let’s use the above numbers to understand what the load average actually means. Assuming you’re using a single-CPU system, the numbers tell us that:</p> 
 <blockquote style=""> 
  <p style="margin-top: 10px; margin-bottom: 10px;">over the last 1 minute: The computer was overloaded by 5% on average. On average, .05 processes were waiting for the CPU. (1.05)</p> 
  <p style="margin-top: 10px; margin-bottom: 10px;">over the last 5 minutes: The CPU idled for 30% of the time. (0.70)</p> 
  <p style="margin-top: 10px; margin-bottom: 10px;">over the last 15 minutes: The computer was overloaded by 409% on average. On average, 4.09 processes were waiting for the CPU. (5.09)</p> 
 </blockquote> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">You probably have a system with multiple CPUs or a multi-core CPU. The load average numbers work a bit differently on such a system. For example, if you have a load average of 2 on a single-CPU system, this means your system was overloaded by 100 percent&nbsp;— the entire period of time, one process was using the CPU while one other process was waiting. On a system with two CPUs, this would be complete usage — two different processes were using two different CPUs the entire time. On a system with four CPUs, this would be half usage — two processes were using two CPUs, while two CPUs were sitting idle.</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">To understand the load average number, you need to know how many CPUs your system has. A load average of 6.03 would indicate a system with a single CPU was massively overloaded, but it would be fine on a computer with 8 CPUs.</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">&nbsp;</p> 
 <p style="margin-bottom: 1.5em; color: #404040; font-family: 'Open Sans', sans-serif; font-size: 16px;">The load average is especially useful on servers and embedded systems. You can glance at it to understand how your system is performing. If it’s overloaded, you may need to deal with a process that’s wasting resources, provide more hardware resources, or move some of the workload to another system.</p> 
</div>