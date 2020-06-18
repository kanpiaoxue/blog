#python通过stomp协议和hornetq进行连接
###发表时间：2012-02-20
###分类：python,HornetQ
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1413898" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1413898</a>

---

<div class="iteye-blog-content-contain"> 
 <p style="font-size: 14px;">=============<span style="font-size: 12px; line-height: 1.5;">=============</span><span style="font-size: 12px; line-height: 1.5;">=========== 2014-03-28 ==</span><span style="font-size: 12px; line-height: 1.5;">=============</span><span style="font-size: 12px; line-height: 1.5;">=============</span><span style="font-size: 12px; line-height: 1.5;">=============</span></p> 
 <p style="font-size: 14px;"><span style="font-size: 12px; line-height: 18px;">stomp.py 的官网地址：<a href="https://pypi.python.org/pypi/stomp.py">https://pypi.python.org/pypi/stomp.py</a></span></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">例子地址：<a href="https://github.com/jasonrbriggs/stomp.py/wiki/Simple-Example">&nbsp;https://github.com/jasonrbriggs/stomp.py/wiki/Simple-Example</a></p> 
 <h1 style="font-family: Georgia, 'Bitstream Vera Serif', 'New York', Palatino, serif; font-weight: normal; line-height: 1em; font-size: 23px; color: #234764; margin-top: 0.7em; margin-bottom: 0.7em;">stomp.py 4.0.11 见附件</h1> 
 <p style="font-size: 14px;">例子代码：</p> 
 <pre name="code" class="python"># -*-coding:utf-8-*-
'''
Created on 2014-3-28

@author: xuepeng
'''

from logging.handlers import TimedRotatingFileHandler
import logging
import os
import stomp
import sys
import time


def initLogger(logFileName):
        if not os.path.isfile(logFileName):
            logPath = logFileName[0:logFileName.rfind('/') + 1]
            if not os.path.isdir(logPath):
                os.makedirs(logPath)
            f = open(logFileName, 'w')
            f.close()
        format = '%(asctime)s [%(threadName)s](%(levelname)s) %(pathname)s(%(funcName)s:%(lineno)s) --&gt; %(message)s'
        filemode = 'a'
        # level = logging.DEBUG
        level = logging.INFO
        logging.basicConfig(filemode=filemode, level=level, format=format)
        hdlr0 = TimedRotatingFileHandler(logFileName, when='D', interval=1, backupCount=0, encoding='utf-8', delay=False, utc=False)
        formatter = logging.Formatter(format)
        hdlr0.setFormatter(formatter)
        logger = logging.getLogger()
        logger.addHandler(hdlr0)
        return logger


logger = initLogger('e:/logs/simple.log')

class MyListener(object):
    def on_error(self, headers, message):
        print('received an error %s' % message)
    def on_message(self, headers, message):
        print('-----&gt;received a message %s' % message)

def main():         
    dest = 'jms.queue.com.wanmei.mq.test.xuepeng'
    
    conn = stomp.Connection(host_and_ports=[ ('mq-node1', 61613) ])
    conn.set_listener('', MyListener())
    conn.start()
    conn.connect()
    conn.subscribe(destination=dest, id=1, ack='auto')
    
    msg = ' '.join(sys.argv[1:])
    num = 0
    while num &lt; 1000:
        conn.send(body=msg, destination=dest)
        print 'send message ', msg
        num = num + 1 
    
    time.sleep(2)
    conn.disconnect()

if __name__ == '__main__':
    main()
</pre> 
 <p style="font-size: 14px;">&nbsp;执行这段代码：</p> 
 <p>python E:\workspace_python\Demo\src\com\wanmei\stomp\simple.py hello world 123</p> 
 <p style="font-size: 14px;">=============<span style="font-size: 12px; line-height: 1.5;">=============</span><span style="font-size: 12px; line-height: 1.5;">=============</span><span style="font-size: 12px; line-height: 1.5;">=============</span><span style="font-size: 12px; line-height: 1.5;">=============</span><span style="font-size: 12px; line-height: 1.5;">=============</span></p> 
 <p style="font-size: 14px;">再看HornetQ，因为自己学了python，所以不仅仅希望用Java来连接HornetQ，也希望用python来连接，进行开发。看了HornetQ的手册，里面说的很清楚，HornetQ不支持对stomp消息的持久化。这算是很大的一个缺点。但是毕竟支持了跨计算机语言的功能。我尝试了，并且写了简单的测试。发现开始运行的时候，会有数据丢失。这个问题在JBoss那里有提到，具体的我还有继续研究。HornetQ的stomp支持，请参考手册。测试了很久，发现就在开始的短暂时间有数据丢失，中间运行还是很稳定的。如果对于数据丢失不是很敏感的应用，可以进行测试。需要进行深入研究。</p> 
 <p style="font-size: 14px;">下面是例子的代码：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="python">#-*-coding:utf-8-*-
'''
Created on 2012-2-20

'''
import logging
import stomp
import time


 
logging.basicConfig()
dest = 'jms.queue.TestQueue' 
#dest = 'jms.topic.TestTopic' 

logging.basicConfig()
class MyListener(stomp.ConnectionListener):     
    def on_error(self, headers, message):         
        print('received an error %s' % message)     
    def on_message(self, headers, message):
        print '--------------------------------------'
        #for k, v in headers.iteritems():             
        #    print('header: key %s , value %s' % (k, v))         
        print('received message\n %s' % message)   

    def on_disconnected(self):
        """
        Called by the STOMP connection when a TCP/IP connection to the
        STOMP server has been lost.  No messages should be sent via
        the connection until it has been reestablished.
        """
        pass
    
    def on_connecting(self, host_and_port):
        """
        Called by the STOMP connection once a TCP/IP connection to the
        STOMP server has been established or re-established. Note that
        at this point, no connection has been established on the STOMP
        protocol level. For this, you need to invoke the "connect"
        method on the connection.

        \param host_and_port a tuple containing the host name and port
        number to which the connection has been established.
        """
        pass

    def on_connected(self, headers, body):
        """
        Called by the STOMP connection when a CONNECTED frame is
        received, that is after a connection has been established or
        re-established.

        \param headers a dictionary containing all headers sent by the
        server as key/value pairs.

        \param body the frame's payload. This is usually empty for
        CONNECTED frames.
        """
        pass
        
    def on_heartbeat_timeout(self):
        """
        Called by the STOMP connection when a heartbeat message has not been
        received beyond the specified period.
        """
        pass

    def on_receipt(self, headers, body):
        """
        Called by the STOMP connection when a RECEIPT frame is
        received, sent by the server if requested by the client using
        the 'receipt' header.

        \param headers a dictionary containing all headers sent by the
        server as key/value pairs.

        \param body the frame's payload. This is usually empty for
        RECEIPT frames.
        """
        pass

    
    def on_send(self, headers, body):
        """
        Called by the STOMP connection when it is in the process of sending a message
        
        \param headers a dictionary containing the headers that will be sent with this message
        
        \param body the message payload
        """
        pass

try:
    conn = stomp.Connection([('192.168.123.74', 61613)]) 
    conn.set_listener('somename', MyListener())
    print('set up Connection') 
    
    conn.start() 
    print('started connection')  
    conn.connect(wait=True) 
    print('connected') 
     
    while True:
        num = 0
        count = 99999
        while num &lt; count:
            try:
                num += 1
                message = 'hello world ' + str(num) 
                conn.send(message=message, destination=dest, headers={'type':'textMessage'}, ack='auto') 
                #print 'sent message:', message
            except Exception , e:
                print '==============', e
        print 'It has produce ' + str(count) + ' messages'
        time.sleep(2) 
except Exception , e:
    print '----------------- ', e
    
print('slept') 
conn.disconnect() 
print('disconnected')
    
    

</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="python">#-*-coding:utf-8-*-
'''
Created on 2012-2-20

'''
import logging
import stomp
import time

logging.basicConfig()
class MyListener(stomp.ConnectionListener):
    def __init__(self,conn,headers): 
        super(MyListener,self).__init__()
        self.conn = conn
        self.headers = headers
    def on_error(self, headers, message):         
        print('received an error %s' % message)     
    def on_message(self, headers, message):
        print '--------------------------------------'
        #for k, v in headers.iteritems():             
        #    print('header: key %s , value %s' % (k, v))         
        print('received message\n %s' % message)   


    def on_disconnected(self):
        """
        Called by the STOMP connection when a TCP/IP connection to the
        STOMP server has been lost.  No messages should be sent via
        the connection until it has been reestablished.
        """
        if not  self.conn.is_connected():
            print 'Error: conn failure! try to connection again'
        sleepTime = 5
        print '+++++++++++++++++++++++++++++++++++++++++++'
        print 'it will sleep ' + str(sleepTime) + ' seconds.'
        time.sleep(sleepTime)

        consume()
        pass
    
    def on_connecting(self, host_and_port):
        """
        Called by the STOMP connection once a TCP/IP connection to the
        STOMP server has been established or re-established. Note that
        at this point, no connection has been established on the STOMP
        protocol level. For this, you need to invoke the "connect"
        method on the connection.

        \param host_and_port a tuple containing the host name and port
        number to which the connection has been established.
        """
        pass

    def on_connected(self, headers, body):
        """
        Called by the STOMP connection when a CONNECTED frame is
        received, that is after a connection has been established or
        re-established.

        \param headers a dictionary containing all headers sent by the
        server as key/value pairs.

        \param body the frame's payload. This is usually empty for
        CONNECTED frames.
        """
        pass
        
    def on_heartbeat_timeout(self):
        """
        Called by the STOMP connection when a heartbeat message has not been
        received beyond the specified period.
        """
        pass

    def on_receipt(self, headers, body):
        """
        Called by the STOMP connection when a RECEIPT frame is
        received, sent by the server if requested by the client using
        the 'receipt' header.

        \param headers a dictionary containing all headers sent by the
        server as key/value pairs.

        \param body the frame's payload. This is usually empty for
        RECEIPT frames.
        """
        pass

    
    def on_send(self, headers, body):
        """
        Called by the STOMP connection when it is in the process of sending a message
        
        \param headers a dictionary containing the headers that will be sent with this message
        
        \param body the message payload
        """
        pass


def consume():
    
    dest = 'jms.queue.TestQueue' 
    clientId = 919191
    headers={'client-id':clientId}
    #dest = 'jms.topic.TestTopic' 
    
    conn = stomp.Connection([('192.168.123.74', 61613)]) 
    print('set up Connection') 
    conn.set_listener('somename', MyListener(conn,headers)) 
    print('Set up listener')  
    conn.start()
    print('started connection')  
    conn.connect(wait=True,headers=headers) 
    print('connected')
    
    conn.subscribe(destination=dest, ack='auto') 
    print('subscribed')
    while True:
        pass
    print('slept') 
    conn.disconnect() 
    print('disconnected')
    
if __name__ == '__main__':
    
    consume()
</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>