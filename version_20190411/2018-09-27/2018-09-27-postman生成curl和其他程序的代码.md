#postman生成curl和其他程序的代码
###发表时间：2018-09-27
###分类：postman,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2431430" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2431430</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>postman生成curl和其他程序的代码</p> 
 <p>参考地址：&nbsp;<a href="https://www.getpostman.com/docs/v6/postman/sending_api_requests/generate_code_snippets">https://www.getpostman.com/docs/v6/postman/sending_api_requests/generate_code_snippets</a></p> 
 <p>&nbsp;</p> 
 <h2 class="documentation-header" style="font-family: 'Open Sans', sans-serif; line-height: 28px; color: #282828; margin-top: 30px; margin-bottom: 10px; font-size: 24px;">Generate code snippets</h2> 
 <p style="margin-top: 20px; margin-bottom: 20px; color: #808080; font-family: 'Open Sans', sans-serif;">Once you’ve finalized and saved your request in Postman, you might want to make the same request from your own application. Postman lets you generate snippets of code in various languages and frameworks that will help you do this. You’ll need to click the<span style="font-weight: bold;">&nbsp;Code</span>&nbsp;link under the blue&nbsp;<span style="font-weight: bold;">Send</span>&nbsp;button to open the&nbsp;<span style="font-weight: bold;">GENERATE CODE SNIPPETS</span>&nbsp;modal.</p> 
 <p style="margin-top: 20px; margin-bottom: 20px; color: #808080; font-family: 'Open Sans', sans-serif;"><a style="background-color: transparent; color: #ff6c37;" href="https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/58525940.png"><img style="vertical-align: middle; margin: 20px 0px; max-width: 100%;" src="https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/58525940.png" alt="generate code link"></a></p> 
 <h3 id="selecting-a-language" style="font-family: 'Open Sans', sans-serif; line-height: 28px; color: #282828; margin-top: 30px; margin-bottom: 30px; font-size: 20px; padding-top: 25px; border-top: 1px solid #f0f0f0;">Selecting a language</h3> 
 <p style="margin-top: 20px; margin-bottom: 20px; color: #808080; font-family: 'Open Sans', sans-serif;">Use the dropdown menu to select a language - some languages have multiple options. This lets you select different frameworks from which to make your request.</p> 
 <p style="margin-top: 20px; margin-bottom: 20px; color: #808080; font-family: 'Open Sans', sans-serif;"><a style="background-color: transparent; color: #ff6c37;" href="https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/WS-select-language.png"><img style="vertical-align: middle; margin: 20px 0px; max-width: 100%;" src="https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/WS-select-language.png" alt="languages dropdown"></a></p> 
 <h3 id="supported-languagesframeworks" style="font-family: 'Open Sans', sans-serif; line-height: 28px; color: #282828; margin-top: 30px; margin-bottom: 30px; font-size: 20px; padding-top: 25px; border-top: 1px solid #f0f0f0;">Supported languages/frameworks</h3> 
 <p style="margin-top: 20px; margin-bottom: 20px; color: #808080; font-family: 'Open Sans', sans-serif;">Postman currently supports the following options:</p> 
 <table style="border-spacing: 0px; border-collapse: collapse; width: 731px; margin: 20px 0px; color: #808080; font-family: 'Open Sans', sans-serif;"> 
  <thead style="">
   <tr style=""> 
    <th style="padding: 5px 10px;"><span style="">Language</span></th> 
    <th style="padding: 5px 10px;"><span style="">Framework</span></th> 
   </tr>
  </thead> 
  <tbody style=""> 
   <tr style=""> 
    <td style="">HTTP</td> 
    <td style="">None (Raw HTTP request)</td> 
   </tr> 
   <tr style=""> 
    <td style="padding: 5px 10px;">C</td> 
    <td style="padding: 5px 10px;"><a style="background-color: transparent; color: #ff6c37;" href="https://curl.haxx.se/libcurl/c/" target="_blank">LibCurl</a></td> 
   </tr> 
   <tr style=""> 
    <td style="">cURL</td> 
    <td style="">None (Raw&nbsp;<a style="background-color: transparent; color: #ff6c37;" href="https://curl.haxx.se/" target="_blank">cURL</a>&nbsp;command)</td> 
   </tr> 
   <tr style=""> 
    <td style="padding: 5px 10px;">C#</td> 
    <td style="padding: 5px 10px;"><a style="background-color: transparent; color: #ff6c37;" href="http://restsharp.org/" target="_blank">RestSharp</a></td> 
   </tr> 
   <tr style=""> 
    <td style="">Go</td> 
    <td style="">Built-in&nbsp;<a style="background-color: transparent; color: #ff6c37;" href="https://golang.org/pkg/net/http/" target="_blank">http package</a> </td> 
   </tr> 
   <tr style=""> 
    <td style="padding: 5px 10px;">Java</td> 
    <td style="padding: 5px 10px;"><a style="background-color: transparent; color: #ff6c37;" href="https://github.com/square/okhttp" target="_blank">OkHttp</a></td> 
   </tr> 
   <tr style=""> 
    <td style="">Java</td> 
    <td style=""><a style="background-color: transparent; color: #ff6c37;" href="http://unirest.io/java.html" target="_blank">Unirest</a></td> 
   </tr> 
   <tr style=""> 
    <td style="padding: 5px 10px;">JavaScript</td> 
    <td style="padding: 5px 10px;"><a style="background-color: transparent; color: #ff6c37;" href="http://api.jquery.com/jquery.ajax/" target="_blank">jQuery AJAX</a></td> 
   </tr> 
   <tr style=""> 
    <td style="">JavaScript</td> 
    <td style="">Built-in&nbsp;<a style="background-color: transparent; color: #ff6c37;" href="https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest" target="_blank">XHR</a> </td> 
   </tr> 
   <tr style=""> 
    <td style="padding: 5px 10px;">NodeJS</td> 
    <td style="padding: 5px 10px;">Built-in&nbsp;<a style="background-color: transparent; color: #ff6c37;" href="https://nodejs.org/api/http.html" target="_blank">http</a>&nbsp;module</td> 
   </tr> 
   <tr style=""> 
    <td style="">NodeJS</td> 
    <td style=""><a style="background-color: transparent; color: #ff6c37;" href="https://github.com/request/request" target="_blank">Request</a></td> 
   </tr> 
   <tr style=""> 
    <td style="padding: 5px 10px;">NodeJS</td> 
    <td style="padding: 5px 10px;"><a style="background-color: transparent; color: #ff6c37;" href="http://unirest.io/nodejs.html" target="_blank">Unirest</a></td> 
   </tr> 
   <tr style=""> 
    <td style="">Objective-C</td> 
    <td style="">Built-in&nbsp;<a style="background-color: transparent; color: #ff6c37;" href="https://developer.apple.com/library/ios/documentation/Foundation/Reference/NSURLSession_class/" target="_blank">NSURLSession</a> </td> 
   </tr> 
   <tr style=""> 
    <td style="padding: 5px 10px;">OCaml</td> 
    <td style="padding: 5px 10px;"><a style="background-color: transparent; color: #ff6c37;" href="https://github.com/mirage/ocaml-cohttp" target="_blank">Cohttp</a></td> 
   </tr> 
   <tr style=""> 
    <td style="">PHP</td> 
    <td style=""><a style="background-color: transparent; color: #ff6c37;" href="http://php.net/manual/it/httprequest.send.php" target="_blank">HttpRequest</a></td> 
   </tr> 
   <tr style=""> 
    <td style="padding: 5px 10px;">PHP</td> 
    <td style="padding: 5px 10px;"><a style="background-color: transparent; color: #ff6c37;" href="https://mdref.m6w6.name/http" target="_blank">pecl_http</a></td> 
   </tr> 
   <tr style=""> 
    <td style="">PHP</td> 
    <td style="">Built-in&nbsp;<a style="background-color: transparent; color: #ff6c37;" href="http://php.net/manual/en/ref.curl.php">curl</a> </td> 
   </tr> 
   <tr style=""> 
    <td style="padding: 5px 10px;">Python</td> 
    <td style="padding: 5px 10px;">Built-in&nbsp;<a style="background-color: transparent; color: #ff6c37;" href="https://docs.python.org/3/library/http.client.html" target="_blank">http.client</a>&nbsp;(Python 3)</td> 
   </tr> 
   <tr style=""> 
    <td style="">Python</td> 
    <td style=""><a style="background-color: transparent; color: #ff6c37;" href="http://docs.python-requests.org/en/master/" target="_blank">Requests</a></td> 
   </tr> 
   <tr style=""> 
    <td style="padding: 5px 10px;">Ruby</td> 
    <td style="padding: 5px 10px;">Built-in&nbsp;<a style="background-color: transparent; color: #ff6c37;" href="http://docs.ruby-lang.org/en/2.0.0/Net/HTTP.html" target="_blank">NET::Http</a> </td> 
   </tr> 
   <tr style=""> 
    <td style="">Shell</td> 
    <td style=""><a style="background-color: transparent; color: #ff6c37;" href="https://www.gnu.org/software/wget/" target="_blank">wget</a></td> 
   </tr> 
   <tr style=""> 
    <td style="padding: 5px 10px;">Shell</td> 
    <td style="padding: 5px 10px;"><a style="background-color: transparent; color: #ff6c37;" href="https://github.com/jkbrzt/httpie" target="_blank">HTTPie</a></td> 
   </tr> 
   <tr style=""> 
    <td style="">Shell</td> 
    <td style=""><a style="background-color: transparent; color: #ff6c37;" href="https://curl.haxx.se/" target="_blank">cURL</a></td> 
   </tr> 
   <tr style=""> 
    <td style="padding: 5px 10px;">Swift</td> 
    <td style="padding: 5px 10px;">Built-in&nbsp;<a style="background-color: transparent; color: #ff6c37;" href="https://developer.apple.com/library/ios/documentation/Foundation/Reference/NSURLSession_class/" target="_blank">NSURLSession</a> </td> 
   </tr> 
  </tbody> 
 </table> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>