#python requests的例子
###发表时间：2019-10-08
###分类：REST,python,requests
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2508629" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2508629</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="python"># get
import requests

url = "http://hello.com/api/sendMail"
querystring = {"date":"20190925","offset":"7"}
headers = {
    'authToken': "3434dfsaflfladdlsajr32k432432=",
    'Content-Type': "application/json",
    'cache-control': "no-cache"
    }

response = requests.request("GET", url, headers=headers, params=querystring)

print(response.text)</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python"># post
import requests

url = "http://hello.com/api/indicator"
payload = "{\"date\": 20191007,\"max\": 1000,\"expr\": 4000}"
headers = {
    'authToken': "3434dfsaflfladdlsajr32k432432=",
    'Content-Type': "application/json",
    'cache-control': "no-cache"
    }

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)</pre> 
 <p>&nbsp;</p> 
</div>