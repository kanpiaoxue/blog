#python 的log格式
###发表时间：2015-05-28
###分类：python,log
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2215010" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2215010</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <ul class="simple"> 
  <li>log.py</li> 
 </ul> 
 <pre name="code" class="python">import logging
import logging.handlers
import os

def init_log(log_path, level=logging.INFO, when="D", backup=7,
             format='%(asctime)s:[%(levelname)s][%(threadName)s] %(filename)s:%(lineno)d --&gt; %(message)s',
             datefmt='%Y-%m-%d %H:%M:%S'):
    """
    init_log - initialize log module

    Args:
      log_path      - Log file path prefix.
                      Log data will go to two files: log_path.log and log_path.log.wf
                      Any non-exist parent directories will be created automatically
      level         - msg above the level will be displayed
                      DEBUG &lt; INFO &lt; WARNING &lt; ERROR &lt; CRITICAL
                      the default value is logging.INFO
      when          - how to split the log file by time interval
                      'S' : Seconds
                      'M' : Minutes
                      'H' : Hours
                      'D' : Days
                      'W' : Week day
                      default value: 'D'
      format        - format of the log
                      default format:
                      %(levelname)s: %(asctime)s: %(filename)s:%(lineno)d * %(thread)d %(message)s
                      INFO: 12-09 18:02:42: log.py:40 * 139814749787872 HELLO WORLD
      backup        - how many backup file to keep
                      default value: 7

    Raises:
        OSError: fail to create log directories
        IOError: fail to open log file
    """
    formatter = logging.Formatter(format, datefmt)
    logger = logging.getLogger()
    logger.setLevel(level)

    # add console log
    consoleHandler = logging.StreamHandler()
    consoleHandler.setLevel(level)
    consoleHandler.setFormatter(formatter)
    logger.addHandler(consoleHandler)
        
    log_dir = os.path.dirname(log_path)
    if not os.path.isdir(log_dir):
        os.makedirs(log_dir)

    handler = logging.handlers.TimedRotatingFileHandler(log_path + '.log',
                                                        when=when,
                                                        backupCount=backup)
    handler.setLevel(level)
    handler.setFormatter(formatter)
    logger.addHandler(handler)</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <ul class="simple"> 
  <li>你可以把上面的代码拷贝到自己的项目中。在程序初始化时，调用<tt class="docutils literal" style="font-family: Consolas, 'Deja Vu Sans Mono', 'Bitstream Vera Sans Mono', monospace; font-size: 0.95em; letter-spacing: 0.01em; border-bottom-width: 1px; border-bottom-style: solid; border-bottom-color: #dddddd; color: #333333; background-color: #f2f2f2;"><span class="pre">init_log</span></tt>即可使日志打印符合规范</li> 
 </ul> 
 <div class="highlight-python"> 
  <div class="highlight"> 
   <pre><span class="kn" style="color: #007020;">import</span> <span class="nn" style="color: #0e84b5;">log</span>
<span class="k" style="color: #007020;">def</span> <span class="nf" style="color: #06287e;">main</span><span class="p">():</span>
    <span class="n">log</span><span class="o" style="color: #666666;">.</span><span class="n">init_log</span><span class="p">(</span><span class="s" style="color: #4070a0;">"./log/my_program"</span><span class="p">)</span>  <span class="c" style="color: #408090; font-style: italic;"># 日志保存到./log/my_program.log和./log/my_program.log.wf，按天切割，保留7天</span>
    <span class="n">logging</span><span class="o" style="color: #666666;">.</span><span class="n">info</span><span class="p">(</span><span class="s" style="color: #4070a0;">"Hello World!!!"</span><span class="p">)</span>
</pre> 
  </div> 
 </div> 
 <p><strong>参考</strong></p> 
 <p><a href="http://styleguide.baidu.com/style/python/index.html#id10">*</a><a class="reference external" href="http://docs.python.org/2.7/library/logging.html">logging — Logging facility for Python</a></p> 
</div>