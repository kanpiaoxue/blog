#(API 设计)Top Seven Tips for Building an API
###发表时间：2018-06-19
###分类：api,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2425147" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2425147</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>引用地址：<a href="https://dzone.com/articles/7-tips-for-building-an-api?utm_source=Top%205&amp;utm_medium=email&amp;utm_campaign=Top%205%202018-06-153">https://dzone.com/articles/7-tips-for-building-an-api?utm_source=Top%205&amp;utm_medium=email&amp;utm_campaign=Top%205%202018-06-153</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <div class="title ng-scope" style="color: #262626; clear: both; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;"> 
  <h1 class="article-title" style="font-size: 42px; margin-top: 14px; margin-bottom: 10px; font-family: inherit; line-height: 1.1; color: #000100;">Top Seven Tips for Building an API</h1> 
 </div> 
 <div class="subhead" style="color: #333333; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;"> 
  <h3 style="font-family: inherit; font-weight: 500; line-height: 1.1; color: #545f68; margin-top: 3px; margin-bottom: 19px; font-size: 21px; clear: both;">Here are seven important tips for building an API, emphasizing the creation of a specification framework, and versioning strategy using REST and HATEOAS.</h3> 
  <div class="ng-scope" style=""> 
   <div class="content-html" style="margin-top: 20px; color: #262626; font-size: 19px; line-height: 1.45; font-family: Georgia, serif;"> 
    <p style="margin-top: 5px; margin-bottom: 15px;">As of 2018, businesses are relying more and more on APIs to serve their clients. Microservices and serverless architectures are becoming increasingly prevalent.&nbsp; This creates a higher number of required API integration points to ensure a competitive advantage and business visibility.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">APIs should be designed from the ground up with these needs in mind. In this article, I will discuss seven design tips for APIs that can help to meet these goals (I should note that these insights are based on my experience building APIs for mobile clients, but the lessons apply more broadly to include API designs of any type).</p> 
    <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">1. Treat Your API as a Product</h2> 
    <p style="margin-top: 5px; margin-bottom: 15px;">A key factor when starting with any sort of development is the notion of the product. It defines the stand-alone entity that exposes useful functionality and benefits to the market. It is no easy task to design and implement an API that is easily consumable, scalable, properly documented, and secured without having a strong sense of responsibility and ownership in the process.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">Thus, it's only fair that your API is treated like one, complete with its own board, backlog, and sprint plan. In addition, a product owner needs to be assigned to convey the vision of the ideal API to the agile team. Developers and testers must devise a plan to work with the best API practices and also to avoid&nbsp;<a style="background: transparent; color: #0288d1;" href="https://blog.runscope.com/posts/6-common-api-testing-mistakes-and-how-to-avoid-them" rel="nofollow" target="_blank">common mistakes</a>. As a result, the end product needs to be production-ready from day one.</p> 
    <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">2. Use an API Specification Framework</h2> 
    <p style="margin-top: 5px; margin-bottom: 15px;">API frameworks are an attempt to standardize development processes across industries. Typically, they consist of an arsenal of tools that cover the whole development lifecycle, from concept to production. While it's true that adhering to a specification like&nbsp;<a style="background: transparent; color: #0288d1;" href="https://blog.runscope.com/posts/openapi-swagger-resource-list-for-api-developers" rel="nofollow" target="_blank">OpenAPI/Swagger</a>&nbsp;while developing an API is more opinionated, it provides better tooling interoperability. Everyone loves automation. Having the ability to generate documentation, SDKs, and UI interaction points every time the code changes is very useful. If you care about standards and want to provide conventional tools when describing your APIs, then this is a very solid option that pays back in advance.</p> 
    <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">3. Use a Versioning Strategy</h2> 
    <p style="margin-top: 5px; margin-bottom: 15px;">Your API is your product and it evolves over time as business requirements change. As a product, it has a specific version, so clients expect the right responses. Changing a published and used API interface is a ticking bomb. The last thing you want is to introduce breaking changes without clients knowing about it. This is especially true for mobile applications when users may still have old versions installed on their phones.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">There are multiple ways to enforce versioning information upon your APIs. Most API designers opt for putting the version information in the URL, as it is practical. For example, the following URL represents a customer's resource endpoint:</p> 
    <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; color: black; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
     <div class="CodeMirror-scroll" style=""> 
      <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
       <div style=""> 
        <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
         <div style=""> 
          <div class="CodeMirror-code" style=""> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">/api/v1/customers</span></pre> 
           </div> 
          </div> 
         </div> 
        </div> 
       </div> 
      </div> 
      <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 26px;">
       &nbsp;
      </div> 
     </div> 
    </div> 
    <p style="margin-top: 5px; margin-bottom: 15px;">It is very important to stick to a&nbsp;<a style="background: transparent; color: #0288d1;" href="https://stripe.com/blog/api-versioning" rel="nofollow" target="_blank">version strategy</a>&nbsp;that is suitable for the business and the available tooling. Later on, if you decide to change a version, it will be easier to provide warnings, updates, and other mechanisms.</p> 
    <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">4. Use Filtering and Pagination</h2> 
    <p style="margin-top: 5px; margin-bottom: 15px;">One common mistake when developing an API is not offering a way to filter or paginate results. When you expose an API that returns a list of items that can change over time, you need to establish a pagination strategy. The reason is simple. Clients, especially mobile ones, cannot view hundreds of list items at once. For example, you can show the first 10. If your API returns the whole database listing for each request, then a lot of resources are being wasted and the performance degrades substantially.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">Modern frameworks offer a way to paginate results, but you can also customize your own. A common approach is to use LIMIT and OFFSET statements on your queries. For example, see this MySQL statement for returning a slice of the total result:</p> 
    <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; color: black; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
     <div class="CodeMirror-scroll" style=""> 
      <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
       <div style=""> 
        <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
         <div style=""> 
          <div class="CodeMirror-code" style=""> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;"><span class="cm-keyword" style="color: #770088;">SELECT</span> * <span class="cm-keyword" style="color: #770088;">from</span> customers <span class="cm-keyword" style="color: #770088;">LIMIT</span> <span class="cm-number" style="color: #116644;">5</span>,<span class="cm-number" style="color: #116644;">10</span></span></pre> 
           </div> 
          </div> 
         </div> 
        </div> 
       </div> 
      </div> 
      <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 26px;">
       &nbsp;
      </div> 
     </div> 
    </div> 
    <p style="margin-top: 5px; margin-bottom: 15px;">This statement will retrieve rows 6-16 from the database so you can provide a JSON response that gives links to the first, next, previous, and last page of that query based on the LIMIT parameters:</p> 
    <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; color: black; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
     <div class="CodeMirror-scroll" style=""> 
      <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
       <div style=""> 
        <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
         <div style=""> 
          <div class="CodeMirror-code" style=""> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;"><span class="cm-comment" style="color: #aa5500;">// _links</span></span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">{</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">  <span class="cm-property" style="">“first”</span>: <span class="cm-variable" style="">“</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">api</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">v1</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">customers</span><span class="cm-operator" style="">?</span><span class="cm-variable" style="">page</span><span class="cm-operator" style="">=</span><span class="cm-number" style="color: #116644;">1</span><span class="cm-variable" style="">”</span>,</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">  <span class="cm-variable" style="">“prev”</span>: <span class="cm-variable" style="">“</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">api</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">v1</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">customers</span><span class="cm-operator" style="">?</span><span class="cm-variable" style="">page</span><span class="cm-operator" style="">=</span><span class="cm-number" style="color: #116644;">1</span><span class="cm-variable" style="">”</span>,</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">  <span class="cm-variable" style="">“next”</span>: <span class="cm-variable" style="">“</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">api</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">v1</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">customers</span><span class="cm-operator" style="">?</span><span class="cm-variable" style="">page</span><span class="cm-operator" style="">=</span><span class="cm-number" style="color: #116644;">3</span><span class="cm-variable" style="">”</span>,</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">  <span class="cm-variable" style="">“last”</span>: <span class="cm-variable" style="">“</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">api</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">v1</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">customers</span><span class="cm-operator" style="">?</span><span class="cm-variable" style="">page</span><span class="cm-operator" style="">=</span><span class="cm-number" style="color: #116644;">9</span><span class="cm-variable" style="">”</span></span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">}</span></pre> 
           </div> 
          </div> 
         </div> 
        </div> 
       </div> 
      </div> 
      <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 134px;">
       &nbsp;
      </div> 
     </div> 
    </div> 
    <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 40px; color: inherit; margin-bottom: 5px; font-size: 24px; clear: both;">5. Use REST and HATEOAS</h2> 
    <p style="margin-top: 5px; margin-bottom: 15px;">REST is a proven and battle-tested architectural approach to designing Web services, and it is independent of any underlying protocol. Thus, it is very suitable for designing APIs. By using REST principles, you can apply some design considerations, such as:</p> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">Treating endpoints as resources that have a conventional naming scheme. For example, if you want to expose a list of orders, you expose the following endpoint:</li> 
    </ul> 
    <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; color: black; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
     <div class="CodeMirror-scroll" style=""> 
      <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
       <div style=""> 
        <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
         <div style=""> 
          <div class="CodeMirror-code" style=""> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;"><span class="cm-keyword" style="color: #770088;">GET</span> <span class="cm-string-2" style="color: #ff5500;">/api/v1/orders</span></span></pre> 
           </div> 
          </div> 
         </div> 
        </div> 
       </div> 
      </div> 
      <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 26px;">
       &nbsp;
      </div> 
     </div> 
    </div> 
    <p style="margin-top: 5px; margin-bottom: 15px;">If you want to find a specific order, you’ll supply an ID parameter:</p> 
    <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; color: black; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
     <div class="CodeMirror-scroll" style=""> 
      <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
       <div style=""> 
        <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
         <div style=""> 
          <div class="CodeMirror-code" style=""> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;"><span class="cm-keyword" style="color: #770088;">GET</span> <span class="cm-string-2" style="color: #ff5500;">/api/v1/orders/1</span></span></pre> 
           </div> 
          </div> 
         </div> 
        </div> 
       </div> 
      </div> 
      <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 26px;">
       &nbsp;
      </div> 
     </div> 
    </div> 
    <p style="margin-top: 5px; margin-bottom: 15px;">This has several advantages, such as better uniformity, readability, and consistency.</p> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">Promoting stateless transactions. This helps make the services more scalable, as they won’t have the hard coupling constraints of keeping state between client and server communications.</li> 
     <li style="padding-bottom: 8px;">Easier navigation within the entire set of resources without prior knowledge of the internal URI scheme with the help of HATEOAS. It enhances the response model of each resource by providing a set of relevant links so that it is easier to interact with the API, without looking up a specification or other metadata service. One good format of HATEOAS is the&nbsp;<a style="background: transparent; color: #0288d1;" href="https://en.wikipedia.org/wiki/Hypertext_Application_Language" rel="nofollow" target="_blank">HAL</a>&nbsp;specification. For example, here is a HAL response to a specific article resource, exposing the relevant links for the reporters:</li> 
    </ul> 
    <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; color: black; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
     <div class="CodeMirror-scroll" style=""> 
      <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
       <div style=""> 
        <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
         <div style=""> 
          <div class="CodeMirror-code" style=""> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">{</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">  <span class="cm-property" style="">“_links”</span>: {</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">    <span class="cm-property" style="">“Self”</span>: {</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">        <span class="cm-property" style="">“href”</span>: <span class="cm-variable" style="">“</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">api</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">v1</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">articles</span><span class="cm-operator" style="">/</span><span class="cm-number" style="color: #116644;">1</span><span class="cm-variable" style="">”</span></span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">    },</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">    <span class="cm-property" style="">“</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">rels</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">reporters”</span>: [</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">      {</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">        <span class="cm-variable" style="">“href”</span>: <span class="cm-variable" style="">“</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">api</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">v1</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">reporters</span><span class="cm-operator" style="">/</span><span class="cm-number" style="color: #116644;">1121</span><span class="cm-variable" style="">”</span></span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">        <span class="cm-variable" style="">“fullName”</span>: <span class="cm-variable" style="">“John</span> <span class="cm-variable" style="">Doe”</span></span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">      },</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">      {</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">        <span class="cm-variable" style="">“href”</span>: <span class="cm-variable" style="">“</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">api</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">v1</span><span class="cm-operator" style="">/</span><span class="cm-variable" style="">reporters</span><span class="cm-operator" style="">/</span><span class="cm-number" style="color: #116644;">192</span><span class="cm-variable" style="">”</span></span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">        <span class="cm-variable" style="">“fullName”</span>: <span class="cm-variable" style="">“Alice</span> <span class="cm-variable" style="">Jansen”</span></span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">      }</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">    ]</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">  }</span></pre> 
           </div> 
           <div style=""> 
            <div class="CodeMirror-gutter-wrapper" style="">
             &nbsp;
            </div> 
            <pre><span style="padding-right: 29px;">}</span></pre> 
           </div> 
          </div> 
         </div> 
        </div> 
       </div> 
      </div> 
      <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 314px;">
       &nbsp;
      </div> 
     </div> 
    </div> 
    <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 40px; color: inherit; margin-bottom: 5px; font-size: 24px; clear: both;">6. Secure Your Endpoints</h2> 
    <p style="margin-top: 5px; margin-bottom: 15px;">You should not neglect security. Any breach can have catastrophic consequences and lead to serious legal issues. Security controls need to be established early in the development process, and, ideally, your API needs to be assessed by an external vendor. The&nbsp;C.I.A. triad of security applies with the following:</p> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;"> <strong style="">C</strong>onfidentiality is achieved by adding proper&nbsp;<strong style="">authentication</strong>&nbsp;controls that provide a means for your system to know who is accessing information or sites.&nbsp;<a style="background: transparent; color: #0288d1;" href="https://en.wikipedia.org/wiki/OAuth" rel="nofollow" target="_blank">OAuth2</a>&nbsp;and&nbsp;<a style="background: transparent; color: #0288d1;" href="https://en.wikipedia.org/wiki/JSON_Web_Token" rel="nofollow" target="_blank">JWT</a>offer a practical and secure means of authenticating controls.&nbsp;<strong style="">HTTPS</strong>&nbsp;must be used at all public endpoints to ensure secure communications.</li> 
     <li style="padding-bottom: 8px;"> <strong style="">I</strong>ntegrity is achieved by using&nbsp;<strong style="">access controls</strong>&nbsp;and&nbsp;<strong style="">authorization</strong>&nbsp;strategies to prevent the tampering of data from unauthorized users.&nbsp;<a style="background: transparent; color: #0288d1;" href="https://en.wikipedia.org/wiki/Role-based_access_control" rel="nofollow" target="_blank">Role-Based Authorization</a>&nbsp;provides a good option.</li> 
     <li style="padding-bottom: 8px;"> <strong style="">A</strong>vailability is achieved by establishing&nbsp;<strong style="">rate limits, partial responses and caching,&nbsp;</strong>in order to prevent extensive usage of API resources or even servers taken down by infinite loops.</li> 
    </ul> 
    <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 40px; color: inherit; margin-bottom: 5px; font-size: 24px; clear: both;">7. Use Monitoring and Reporting</h2> 
    <p style="margin-top: 5px; margin-bottom: 15px;">While developing and testing your API plays a big part in the process, the real work does not end here. You need to continue providing support, even before the code is deployed to production. If something goes wrong, the right people need to be notified with actionable information, in order to respond by any means necessary. This constitutes a proactive approach when developing your API. If you keep things at bay, when endpoint issues emerge, you can prevent any catastrophic failures. API monitoring tools like&nbsp;<a style="background: transparent; color: #0288d1;" href="https://www.runscope.com/" rel="nofollow" target="_blank">Runscope</a>&nbsp;can also help you with that.</p> 
   </div> 
  </div> 
  <div class="article-bumper article-bumper-bottom ng-binding ng-scope" style="color: #808285; padding: 10px 0px; line-height: 1.45; display: inline-block; margin: 25px 0px 0px; font-size: 16px; width: 853px; border-top: 1px solid #d9dcdd; border-bottom: 1px solid #d9dcdd;">
   &nbsp;
  </div> 
 </div> 
 <p>&nbsp;</p> 
</div>