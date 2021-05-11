#使用python自带的http模块（urllib2）发送POST请求
###发表时间：2019-12-30
###分类：python,经验,http,REST
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2511574" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2511574</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>python的requests的package非常好用，但是它必须预装。遇到无法预装的情况如何处理？可以使用python自带的package来处理http请求。</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">import logging
import json
import urllib2

logging.basicConfig(level=logging.DEBUG, format='%(asctime)s [PID:%(process)d] %(levelname)s --&gt; %(message)s')
logger = logging.getLogger(__name__)

def post_cluster():
    
    api_url = 'http://localhost:8080/hello'
    api_token = 'hello-token'

    logger.info('url:%s,api_token:%s', api_url, api_token)

    json_obj = {}
    json_obj['cluster_name'] = 'cluster_name'
    json_obj['host'] = '127.0.0.1'
    json_obj['port'] = 8080

    headers = {'Content-Type': 'application/json', 'authToken': api_token}
    data = json.dumps(json_obj)
    logger.info('data:%s', data)
    req = urllib2.Request(api_url, data, headers=headers)
    response = urllib2.urlopen(req)
    rs = response.read().decode()
    print rs
    result_obj = json.loads(rs)
    if 0 == result_obj['status']:
        logger.info('successfully!')
    else:
        logger.error('failed! ' + result_obj['errorMessage'])
    pass</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>