#python的log文件回滚
###发表时间：2020-05-18
###分类：python,log,经验,pylog
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2514188" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2514188</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>python生成按照文件大小进行回滚的日志</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import logging
import logging.handlers as handlers

log_file_path = r'/Users/kanpiaoxue/tmp/20200518/log/hello.log'
log_file_max_bytes = 1024 * 1
log_file_max_count = 10
log_file_level= logging.DEBUG

log_formatter = logging.Formatter('%(asctime)s [PID:%(process)d] [%(threadName)-12.12s] %(levelname)-5.5s [%(filename)s:%(lineno)d] --&gt; %(message)s')
log_handler = handlers.RotatingFileHandler(log_file_path, maxBytes=log_file_max_bytes, backupCount=log_file_max_count)
log_handler.setFormatter(log_formatter)

logger = logging.getLogger(__name__)
logger.setLevel(log_file_level)
logger.addHandler(log_handler)


def test_001():
    while True:
        logger.debug('start to test_001')
        logger.info('start to test_001')
        print 'start to test_001'
    pass


if __name__ == '__main__':
    test_001()
    pass</pre> 
 <p>&nbsp;</p> 
</div>