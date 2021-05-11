#swagger生成javaAPI的server&client代码
###发表时间：2021-03-25
###分类：springboot,Spring,java,经验,open api,api
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2519910" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2519910</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>文章原文：</p> 
 <p>《Spring Boot: API First Approach》：<a href="https://dzone.com/articles/spring-boot-api-first-approach?edition=664392">https://dzone.com/articles/spring-boot-api-first-approach?edition=664392</a></p> 
 <p>&nbsp;</p> 
 <p>提到的工具：</p> 
 <p>1、<a href="https://editor.swagger.io/">https://editor.swagger.io/</a></p> 
 <p>2、<a href="https://openapi-generator.tech/">https://openapi-generator.tech/</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <div class="header" style="clear: both; color: #333333; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;"> 
  <div class="header-title" style=""> 
   <div class="subhead" style=""> 
    <h3 style="font-family: inherit; font-weight: 500; line-height: 1.1; color: #545f68; margin-top: 3px; margin-bottom: 19px; font-size: 21px; clear: both;">I describe how I created the API definition, then how I created the server and client code from the API definition. Then I will talk about some of the problems I faced.</h3> 
   </div> 
   <div class="publish-meta ng-scope" style=""> 
    <div class="article-author-meta" style="display: inline-block;"> 
     <a style="background: transparent; color: #b6b7ba;" href="https://dzone.com/users/3071353/amrutprabhu.html"><img class="avatar lazyloaded" style="vertical-align: middle; margin-right: 5px; border-radius: 50%;" src="https://dz2cdn1.dzone.com/thumbnail?fid=14133924&amp;w=80&amp;caller=ThumbnailUrl-article.content&amp;uri=/articles/spring-boot-api-first-approach" alt="" width="40">&nbsp;</a>by&nbsp; 
     <div class="author-info" style="display: inline-block;">
      <span class="author-name" style=""><a class="ng-isolate-scope" style="background: transparent; color: #b6b7ba;" href="https://dzone.com/users/3071353/amrutprabhu.html">Amrut Prabhu</a></span>
     </div> &nbsp;·
    </div> &nbsp;
    <span class="author-date" style="">Mar. 21, 21</span>&nbsp;·&nbsp;
    <a id="portal-name" style="background: transparent; color: #b6b7ba;" href="https://dzone.com/java-jdk-development-tutorials-tools-news">Java Zone</a>&nbsp;·&nbsp;Tutorial
   </div> 
  </div> 
 </div> 
 <div class="author-n-useraction" style="border-bottom: 0px solid #d9dcdd; border-top: 0px solid #d9dcdd; background: #ebecef; color: #737981; padding-top: 10px; line-height: 1; padding-left: 15px; padding-right: 15px; clear: both; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-size: 15px !important;"> 
  <div class="like action" style="display: inline-block; font-weight: 600; margin-right: 15px;"> 
   <div class="dz-like icon-thumbs-up" style="background: none; font-weight: 500; width: auto; height: auto; padding: 0px; text-align: center; cursor: pointer;"> 
    <span class="action-label" style=""><span style="">Like</span></span>&nbsp;
    <a style="background: transparent; color: #737981;" href="https://dzone.com/articles/spring-boot-api-first-approach?edition=664392"><span class="ng-binding" style="">(6)</span></a> 
   </div> 
  </div> &nbsp; 
  <div class="comment action" style="display: inline-block; font-weight: 600; margin-right: 15px;"> 
   <p class="ng-isolate-scope" style="margin-bottom: 10px; display: inline-block;">&nbsp;Comment (<span class="comment-after number-of-comments ng-binding" style="">1</span>)</p> 
  </div> &nbsp; 
  <div class="save action" style="display: inline-block; font-weight: 600; margin-right: 15px;">
   Save
  </div> &nbsp; 
  <div class="tweet action" style="display: inline-block; font-weight: 600; margin-right: 15px;">
   <a class="title" style="background: transparent; color: #737981; clear: both;" href="https://dzone.com/articles/spring-boot-api-first-approach?edition=664392" target="_blank">&nbsp;<span class="action-label" style="">Tweet</span></a>
  </div> 
  <div class="pull-right" style="float: right !important;"> 
   <div class="article-views action ng-binding" style="display: inline-block; font-weight: 600; margin-right: 0px; text-align: right;">
    &nbsp;5,120&nbsp;
    <span class="action-label" style="">Views</span> 
   </div> 
  </div> 
 </div> 
 <div class="signin-prompt" style="padding: 12px 10px 15px 20px; background-color: #ecf7ff; font-size: 18px; margin-top: 15px; width: 733px; max-width: 100%; color: #333333; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;"> 
  <p style="margin-right: 14px; color: #2a6f93; display: inline-block;">Join the DZone community and get the full member experience.</p> &nbsp;
  <a id="article-signin-prompt" style="background: #1bd281; color: #ffffff; padding: 5px 10px; border-radius: 2px; font-size: 16px; font-weight: 600; white-space: nowrap;" href="https://dzone.com/articles/spring-boot-api-first-approach?edition=664392">JOIN FOR FREE</a> 
 </div> 
 <div class="arrow-down" style="width: 0px; height: 0px; border-style: solid; border-width: 13px 18px 0px 0px; border-color: #ecf7ff transparent transparent; color: #333333; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">
  &nbsp;
 </div> 
 <div class="ng-scope" style="color: #333333; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">
  &nbsp;
 </div> 
 <div class="ng-scope" style="color: #333333; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;"> 
  <div class="content-html" style="margin-top: 30px; color: #222635 !important; font-size: 19px !important; line-height: 1.45 !important; font-family: Cambria, serif !important;"> 
   <p style="margin-top: 5px; margin-bottom: 15px;">In this blog, I take a practical approach to API first design with Open API 3 specification.</p> 
   <p style="margin-top: 5px; margin-bottom: 15px;">Firstly, I describe how I created the API definition, then how I created the server and the client code from the API definition. Then I will talk about some of the problems I faced.</p> 
   <h2 style="">Advantages of API First Approach</h2> 
   <p style="margin-top: 5px; margin-bottom: 15px;">As we are adopting microservice-based architectures, API first approach has been gaining some traction. There are quite many advantages to using API first approach and I will discuss a few of them.</p> 
   <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;"><strong style="">Clear Contract Definition</strong></h3> 
   <p style="margin-top: 5px; margin-bottom: 15px;">With API first approach, you can create a concrete contract with which you can set clear goals on what will be provided by your application. It also helps to decouple your implementation from the Interface you provide via the API.</p> 
   <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;"><strong style="">Well Documented API</strong></h3> 
   <p style="margin-top: 5px; margin-bottom: 15px;">You follow well-structured documentation of the API you are providing and it helps stakeholders to have a clear understanding of the interface you are providing via your APIs in a human-readable format.</p> 
   <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;"><strong style="">Promotes Development in Parallel</strong></h3> 
   <p style="margin-top: 5px; margin-bottom: 15px;">This is one of the advantages that I really love is that the producer and consumer of the API can work in parallel once you have the API definition in place. The Consumer can easily create mocks with the already agreed API contract and start their end of the development.</p> 
   <h2 style="">Let’s Get Started!</h2> 
   <p style="margin-top: 5px; margin-bottom: 15px;">To start off, I went to&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://editor.swagger.io/" rel="nofollow" target="_blank">https://editor.swagger.io/</a>&nbsp;and created my API definition. I used the Open API 3 specification to create the API definition. There are many other tools to create your API definition, but I choose this as I was familiar with creating Swagger API documentation in Java. I used this online editor as it provides an auto-complete feature (with ctrl + space) depending on the context you are in. This helped me a lot to create the API definition.</p> 
   <p style="margin-top: 5px; margin-bottom: 15px;">However, I am not a fluent API definition creator, So I learned the way to define the API using the&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://github.com/OAI/OpenAPI-Specification/blob/master/examples/v3.0/petstore.yaml" rel="nofollow" target="_blank">petstore</a>&nbsp;API definition example.&nbsp;</p> 
   <p style="margin-top: 5px; margin-bottom: 15px;">To get started, I created a very minimal API definition in which I can create an account using a post request.</p> 
   <img class="fr-fic fr-dib lazyloaded" style="vertical-align: middle; max-width: 100%; height: auto; text-align: center; margin: auto; display: block; width: 600px; float: none !important;" src="https://dzone.com/storage/temp/14527008-1615753228334.png" alt="API Definition Code">
   <h2 style=""><strong style="">Generating Code</strong></h2> 
   <p style="margin-top: 5px; margin-bottom: 15px;">With the API definition all set, let’s start with creating the server and client of the API. For this, I created a spring boot application which I created normally via&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://start.spring.io/" rel="nofollow" target="_blank">https://start.spring.io</a>. The only dependency I added here was&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">spring-web</code>&nbsp;.</p> 
   <p style="margin-top: 5px; margin-bottom: 15px;">Next, I used the&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://openapi-generator.tech/" rel="nofollow" target="_blank">Open API Generator</a>&nbsp;Maven plugin to create the server and the client for me. Let’s see how to do that.</p> 
   <h2 style=""><strong style="">Server-side Code Generation</strong></h2> 
   <p style="margin-top: 5px; margin-bottom: 15px;">To create the server-side code from the API definition, I added the&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://github.com/OpenAPITools/openapi-generator/tree/master/modules/openapi-generator-maven-plugin" rel="nofollow" target="_blank">Open API generator plugin</a>&nbsp;and provided it with the API definition file. Since I am creating a server based on spring, I provided a generation type&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">spring</code>, So that it knows it can use spring classes to create my server code. There are quite a few server code generators that you can find&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://openapi-generator.tech/docs/generators/README#server-generators" rel="nofollow" target="_blank">here</a>. Now, let's look at what the plugin config looks like:</p> 
   <img class="fr-fic fr-dib lazyloaded" style="vertical-align: middle; max-width: 100%; height: auto; text-align: center; margin: auto; display: block; width: 600px; float: none !important;" src="https://dzone.com/storage/temp/14545863-1616280892458.png" alt="Server Plugin Config">
   <p style="margin-top: 5px; margin-bottom: 15px;">Some of the customization options I used here were, which package name to use to create my API and model classes. There are quite a few other options you can specify. E.g., you can define what your model class names can be pre-appended with and you can find the various other options on their&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://github.com/OpenAPITools/openapi-generator/tree/master/modules/openapi-generator-maven-plugin" rel="nofollow" target="_blank">GitHub link</a>.</p> 
   <p style="margin-top: 5px; margin-bottom: 15px;">Now, the code that gets generated from the plugin requires a few more dependencies for it to compile successfully. I exactly found the minimal set I needed and added the following dependencies.</p> 
   <pre name="73d0">&lt;dependency&gt;
    &lt;groupId&gt;javax.validation&lt;/groupId&gt;
    &lt;artifactId&gt;validation-api&lt;/artifactId&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
    &lt;groupId&gt;io.springfox&lt;/groupId&gt;
    &lt;artifactId&gt;springfox-swagger2&lt;/artifactId&gt;
    &lt;version&gt;${springfox-version}&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
    &lt;groupId&gt;org.openapitools&lt;/groupId&gt;
    &lt;artifactId&gt;jackson-databind-nullable&lt;/artifactId&gt;
    &lt;version&gt;${jackson-databind-nullable}&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
    &lt;groupId&gt;io.swagger.core.v3&lt;/groupId&gt;
    &lt;artifactId&gt;swagger-annotations&lt;/artifactId&gt;
    &lt;version&gt;${swagger-annotations-version}&lt;/version&gt;
&lt;/dependency&gt;</pre> 
   <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> 
   <p style="margin-top: 5px; margin-bottom: 15px;">Now comes the main part, i.e., generating the code. After building the code using&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">mvn clean verify</code>, there were a few classes that got generated.</p> 
   <img class="fr-fic fr-dib lazyloaded" style="vertical-align: middle; max-width: 100%; height: auto; text-align: center; margin: auto; display: block; width: 303px; float: none !important;" src="https://dzone.com/storage/temp/14545867-1616281020718.png" alt="Generated Classes">
   <p style="margin-top: 5px; margin-bottom: 15px;">In the API package, there were two main interfaces,&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">AccountApi</code>&nbsp;and&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">AccountApiDeligate</code>&nbsp;. The&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">AccountApi</code>&nbsp;interface contains the actual definition of the API using&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">@postmapping</code>&nbsp;annotation and it also contains the required API documentation using spring swagger annotations. Its implementation class is&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">AccountApiController</code>&nbsp;which calls the delegated service.</p> 
   <p style="margin-top: 5px; margin-bottom: 15px;">The important interface for you is the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">AccountApiDelegate</code>&nbsp;interface. This provides a delegate service pattern, which allows you to provide the implementation of what needs to be handled or done when the API is called. Here you put in your business logic that handles the request. Once you implement the service delegate, you are actually ready to serve requests.</p> 
   <p style="margin-top: 5px; margin-bottom: 15px;">That’s it, you are done with the server-side. Next, the Client.</p> 
   <h2 style=""><strong style="">Client Code Generation</strong></h2> 
   <p style="margin-top: 5px; margin-bottom: 15px;">For the client-side code generation, I use the same plugin, but this time with the generator name as&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">java</code>&nbsp;.&nbsp;</p> 
   <img class="fr-fic fr-dib lazyloaded" style="vertical-align: middle; max-width: 100%; height: auto; text-align: center; margin: auto; display: block; width: 600px; float: none !important;" src="https://dzone.com/storage/temp/14545868-1616281078294.png" alt="Client Code Generation">
   <p style="margin-top: 5px; margin-bottom: 15px;">I also provide some config properties, Like the library to use for making the rest client. Here I wanted it to use&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">restemplate</code>&nbsp;for making the calls to the server. There are quite a few options you can configure that you can find from their documentation&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://openapi-generator.tech/docs/generators/java" rel="nofollow" target="_blank">here</a>.</p> 
   <p style="margin-top: 5px; margin-bottom: 15px;">You would also require some more dependencies to help you compile the generated code.&nbsp;</p> 
   <pre name="1b38">&lt;dependency&gt;
   &lt;groupId&gt;com.google.code.gson&lt;/groupId&gt;
   &lt;artifactId&gt;gson&lt;/artifactId&gt;
   &lt;version&gt;${gson.version}&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
   &lt;groupId&gt;io.swagger.core.v3&lt;/groupId&gt;
   &lt;artifactId&gt;swagger-annotations&lt;/artifactId&gt;
   &lt;version&gt;${swagger-annotations-version}&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
   &lt;groupId&gt;io.springfox&lt;/groupId&gt;
   &lt;artifactId&gt;springfox-swagger2&lt;/artifactId&gt;
   &lt;version&gt;${springfox-version}&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
   &lt;groupId&gt;com.squareup.okhttp3&lt;/groupId&gt;
   &lt;artifactId&gt;okhttp&lt;/artifactId&gt;
   &lt;version&gt;${okhttp.version}&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
   &lt;groupId&gt;com.google.code.findbugs&lt;/groupId&gt;
   &lt;artifactId&gt;jsr305&lt;/artifactId&gt;
   &lt;version&gt;${jsr305.version}&lt;/version&gt;
&lt;/dependency&gt;</pre> 
   <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> 
   <img class="fr-fic fr-dib lazyloaded" style="vertical-align: middle; max-width: 100%; height: auto; text-align: center; margin: auto; display: block; width: 400px; float: none !important;" src="https://dzone.com/storage/temp/14545869-1616281115879.png" alt="Client Code Dependencies">
   <p style="margin-top: 5px; margin-bottom: 15px;">After the code generation, You can find classes that provide you how to configure the client to talk to the server. It also provides some basic authentication, using bearer token or basic auth.</p> 
   <p style="margin-top: 5px; margin-bottom: 15px;">Now you need to create an instance/bean of the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">ApiClient</code>&nbsp;. This contains the host config of the server you want to communicate. This is then used in the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">AccountApi</code>&nbsp;class to help you make requests to the server. To make a request, you would only have to call the API function from the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">AccountApi</code>&nbsp;class.</p> 
   <p style="margin-top: 5px; margin-bottom: 15px;">There we have it now. You have successfully generated the client code and you can now check the interaction between the client and the server.</p> 
   <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;"><strong style="">Problems I Encountered</strong></h3> 
   <p style="margin-top: 5px; margin-bottom: 15px;">There are quite a few bugs in the latest version of the plugin that I was using (5.0.1).</p> 
   <ul style="margin-bottom: 10px;"> 
    <li style="padding-bottom: 8px;">For&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">spring</code>&nbsp;generator, there are some unused imports from spring data that get added by the generator while creating the controller. Hence you would have to add spring data dependency, Even if you not using a database with the service. This may not be a big problem, because mostly you would have a database that you connect to with your service. You can check the current open bug&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://github.com/OpenAPITools/openapi-generator/issues/8360" rel="nofollow" target="_blank">here</a>.</li> 
    <li style="padding-bottom: 8px;">Usually, you would define the schema for request and response in the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">components</code>&nbsp;section of the API definition file and then use the reference to these schemas in the API using the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">$ref:</code>&nbsp;property. This is currently not working as excepted. The way to get around it was to define the inline schema for each request and response. Hence the model names get generated with a prefix&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">Inline*</code>&nbsp;. You can track this bug&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://github.com/OpenAPITools/openapi-generator/issues/7922" rel="nofollow" target="_blank">here</a>.</li> 
   </ul> 
   <p style="margin-top: 5px; margin-bottom: 15px;">If you use the older version, i.e,&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; white-space: nowrap; border-radius: 4px;">4.3.1</code>&nbsp;; it's free from these bugs and the plugin works well as expected.&nbsp;</p> 
   <p style="margin-top: 5px; margin-bottom: 15px;">As usual, I have uploaded the code to&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://github.com/amrutprabhu/spring-boot-api-first-approach" rel="nofollow" target="_blank">GitHub</a>. Enjoy!!</p> 
  </div> 
 </div> 
 <div class="ng-scope" style="color: #333333; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">
  &nbsp;
 </div> 
 <div class="article-topics" style="margin: 20px 0px; color: #333333; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;"> 
  <div class="topic-label" style="width: 50px; display: inline;">
   Topics:
  </div> &nbsp; 
  <div class="topics" style=""> 
   <span class="topics-tag" style="margin-right: 3px; font-size: 12px; color: #737981; display: inline-block;">JAVA,</span>&nbsp;
   <span class="topics-tag" style="margin-right: 3px; font-size: 12px; color: #737981; display: inline-block;">OPEN API,</span>&nbsp;
   <span class="topics-tag" style="margin-right: 3px; font-size: 12px; color: #737981; display: inline-block;">SPRING BOOT,</span>&nbsp;
   <span class="topics-tag" style="margin-right: 3px; font-size: 12px; color: #737981; display: inline-block;">TUTORIAL</span> 
  </div> 
 </div> 
</div>