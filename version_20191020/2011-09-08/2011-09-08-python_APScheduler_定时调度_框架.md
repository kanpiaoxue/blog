#python APScheduler 定时调度 框架
###发表时间：2011-09-08
###分类：python
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1168778" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1168778</a>

---

<p>python APScheduler 框架，模仿Java的Quartz框架写的，强大给力。</p>
<p>它的主页是：<a href="http://packages.python.org/APScheduler/index.html">http://packages.python.org/APScheduler/index.html</a></p>
<p>提问的地方：<a href="http://groups.google.com/group/apscheduler">http://groups.google.com/group/apscheduler</a>&nbsp;（老外很认真的回答你的问题）</p>
<p>它的按照很简单：参考主要的install就可以了，就两三步</p>
<p>例子如下：</p>
<p>&nbsp;</p>
<pre name="code" class="python">from apscheduler.scheduler import Scheduler
import time

# Start the scheduler
sched = Scheduler()


def job_function():
    print "Hello World"

print 'start to sleep'
print 'wake'
sched.daemonic = False
sched.add_cron_job(job_function,day_of_week='mon-fri', hour='*', minute='0-59',second='*/5')
sched.start()</pre>
<p>&nbsp;这个是最简单的例子（目前我初学，呵呵）</p>
<p>这里要提到的是：</p>
<p>apscheduler会创建一个线程，这个线程默认是daemon=True，也就是默认的是线程守护的。</p>
<p>在上面的代码里面，要是不加上sched.daemonic=False的话，这个脚本就不会运行。</p>
<p>因为上面的脚本要是没有sched.daemonic=False的话，它会创建一个守护线程。这个过程中，会创建scheduler的实例。但是由于脚本很小，运行速度很快，主线程mainthread会马上结束，而此时定时任务的线程还没来得及执行，就跟随主线程结束而结束了。（守护线程和主线程之间的关系决定的）。要让脚本运行正常，必须设置该脚本为非守护线程。sched.daemonic=False</p>
<p>=================== end ======================</p>
<p>&nbsp;</p>
<p>补充：</p>
<p>&nbsp;</p>
<p> </p>
<pre name="code" class="python">#-*-coding:utf-8-*-
from apscheduler.scheduler import Scheduler

def job_function(a):
    print a

if __name__ == '__main__':
    hello = 'hello world'
    sched = Scheduler(daemonic=False) # 注意这里，要设置 daemonic=False
    sched.add_cron_job(job_function, day_of_week='mon-fri', hour='*', minute='0-59', second='*/5', args=[hello]) # args=[] 用来给job函数传递参数
    sched.start()

# ----------- 源码  -------------------------------   
#   def add_cron_job(self, func, year=None, month=None, day=None, week=None,
#                    day_of_week=None, hour=None, minute=None, second=None,
#                    start_date=None, args=None, kwargs=None, **options):
#       """
#       Schedules a job to be completed on times that match the given
#       expressions.
#
#       :param func: callable to run
#       :param year: year to run on
#       :param month: month to run on
#       :param day: day of month to run on
#       :param week: week of the year to run on
#       :param day_of_week: weekday to run on (0 = Monday)
#       :param hour: hour to run on
#       :param second: second to run on
#       :param args: list of positional arguments to call func with
#       :param kwargs: dict of keyword arguments to call func with
#       :param name: name of the job
#       :param jobstore: alias of the job store to add the job to
#       :param misfire_grace_time: seconds after the designated run time that
#           the job is still allowed to be run
#       :return: the scheduled job
#       :rtype: :class:`~apscheduler.job.Job`
#       """
#</pre>
<p>&nbsp;</p>