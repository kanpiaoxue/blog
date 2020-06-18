#Software Architectur:The 5 Patterns You Need to Know
###发表时间：2018-07-03
###分类：经验,架构,设计模式
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2426046" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2426046</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考地址：&nbsp;https://dzone.com/articles/software-architecture-the-5-patterns-you-need-to-k?edition=383283&amp;utm_source=Daily%20Digest&amp;utm_medium=email&amp;utm_campaign=Daily%20Digest%202018-07-02</p> 
 <p>【注意】附件有该内容的pdf。</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <div class="subhead" style="color: #333333; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;"> 
  <h3 style="font-family: inherit; font-weight: 500; line-height: 1.1; color: #545f68; margin-top: 3px; margin-bottom: 19px; font-size: 21px; clear: both;">Whether you're a software architect or a developer, it always pays to know the patterns used in a given architecture. Here are five of the most important ones.</h3> 
 </div> 
 <div class="publish-meta ng-scope" style=""> 
  <div class="article-author-meta" style="display: inline-block;"> 
   <a style="background: transparent; color: #b6b7ba;" href="https://dzone.com/users/3348179/petermorlion.html"><img class="avatar" style="vertical-align: middle; margin-right: 5px; border-radius: 50%;" src="https://secure.gravatar.com/avatar/61cf7764f1aec30af7bbe4e5aa8e7d9b?d=identicon&amp;r=PG" alt="" width="40">&nbsp;</a>by&nbsp; 
   <div class="author-info" style="display: inline-block;">
    <span class="author-name" style=""><a class="ng-isolate-scope" style="background: transparent; color: #b6b7ba;" href="https://dzone.com/users/3348179/petermorlion.html">Peter Morlion</a></span>
   </div> &nbsp; 
   <div class="mvb-award" style="width: 44px; display: inline-block; cursor: pointer;">
    &nbsp;
   </div> &nbsp; 
   <div class="mvb-partner" style="color: #8468ea; display: inline-block; cursor: pointer;">
    &nbsp;
   </div> &nbsp; 
   <div class="zone-leader" style="">
    &nbsp;
   </div> &nbsp;·
  </div> &nbsp;
  <span class="author-date" style="">Jun. 30, 18</span>&nbsp;·&nbsp;
  <a id="portal-name" style="background: transparent; color: #b6b7ba;" href="https://dzone.com/microservices-news-tutorials-tools">Microservices Zone</a>&nbsp;·&nbsp;Tutorial
 </div> 
 <div class="publish-meta ng-scope" style=""> 
  <div class="ng-scope" style="color: #333333; font-size: 14px; font-weight: 500;"> 
   <div class="content-html" style="margin-top: 30px; color: #222635; font-size: 19px; line-height: 1.45; font-family: Cambria, serif;"> 
    <p style="margin-top: 5px; margin-bottom: 15px;">When I was attending night school to become a programmer, I learned several&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://en.wikipedia.org/wiki/Software_design_pattern" rel="nofollow" target="_blank">design patterns</a>: singleton, repository, factory, builder, decorator, etc. Design patterns give us a proven solution to existing and recurring problems. What I didn’t learn was that a similar mechanism exists on a higher level: software architecture patterns. These are patterns for the overall layout of your application or applications. They all have advantages and disadvantages. And they all address specific issues.</p> 
    <h2 style="">Layered Pattern</h2> 
    <p style="margin-top: 5px; margin-bottom: 15px;">The layered pattern is probably one of the most well-known software architecture patterns. Many developers use it, without really knowing its name. The idea is to split up your code into “layers”, where each layer has a certain responsibility and provides a service to a higher layer.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">There isn’t a predefined number of layers, but these are the ones you see most often:</p> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">Presentation or UI layer</li> 
     <li style="padding-bottom: 8px;">Application layer</li> 
     <li style="padding-bottom: 8px;">Business or domain layer</li> 
     <li style="padding-bottom: 8px;">Persistence or data access layer</li> 
     <li style="padding-bottom: 8px;">Database layer</li> 
    </ul> 
    <p style="margin-top: 5px; margin-bottom: 15px;">The idea is that the user initiates a piece of code in the presentation layer by performing some action (e.g. clicking a button). The presentation layer then calls the underlying layer, i.e. the application layer. Then we go into the business layer and finally, the persistence layer stores everything in the database. So higher layers are dependent upon and make calls to the lower layers.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;"><a style="background: transparent; color: #29a8ff;" href="https://blog.ndepend.com/wp-content/uploads/layered-1.png" rel="nofollow"><img class="fr-fin fr-dib" style="vertical-align: middle; max-width: 100%; height: auto; text-align: center; margin: auto; display: block; float: none !important;" src="https://blog.ndepend.com/wp-content/uploads/layered-1.png" alt="" width="507" height="256"></a></p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">You will see variations of this, depending on the complexity of the applications. Some applications might omit the application layer, while others add a caching layer. It’s even possible to merge two layers into one. For example, the&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://www.martinfowler.com/eaaCatalog/activeRecord.html" rel="nofollow" target="_blank">ActiveRecord</a>&nbsp;pattern combines the business and persistence layers.</p> 
    <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Layer Responsibility</h3> 
    <p style="margin-top: 5px; margin-bottom: 15px;">As mentioned, each layer has its own responsibility. The presentation layer contains the graphical design of the application, as well as any code to handle user interaction. You shouldn’t add logic that is not specific to the user interface in this layer.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">The business layer is where you put the models and logic that is specific to the business problem you are trying to solve.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">The application layer sits between the presentation layer and the business layer. On the one hand, it provides an&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://blog.ndepend.com/plugging-leaky-abstractions/" rel="nofollow" target="_blank">abstraction</a>&nbsp;so that the presentation layer doesn’t need to know the business layer. In theory, you could change the technology stack of the presentation layer without changing anything else in your application (e.g. change from WinForms to WPF). On the other hand, the application layer provides a place to put certain coordination logic that doesn’t fit in the business or presentation layer.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">Finally, the persistence layer contains the code to access the database layer. The database layer is the underlying database technology (e.g. SQL Server, MongoDB). The persistence layer is the set of code to manipulate the database: SQL statements, connection details, etc.</p> 
    <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Advantages</h3> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">Most developers are familiar with this pattern.</li> 
     <li style="padding-bottom: 8px;">It provides an easy way of writing a well-organized and&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://blog.ndepend.com/unit-tests-desirable-codebase-properties/" rel="nofollow" target="_blank">testable application</a>.</li> 
    </ul> 
    <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Disadvantages</h3> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">It tends to lead to monolithic applications that are hard to split up afterward.</li> 
     <li style="padding-bottom: 8px;">Developers often find themselves writing a lot of code to pass through the different layers, without adding any value in these layers. If all you are doing is writing a simple CRUD application, the layered pattern might be overkill for you.</li> 
    </ul> 
    <p style="margin-top: 5px; margin-bottom: 15px;"><strong style="">Ideal for</strong></p> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">Standard line-of-business apps that do more than just CRUD operations</li> 
    </ul> 
    <h2 style="">Microkernel</h2> 
    <p style="margin-top: 5px; margin-bottom: 15px;">The microkernel pattern, or plug-in pattern, is useful when your application has a core set of responsibilities and a collection of interchangeable parts on the side. The microkernel will provide the entry point and the general flow of the application, without really knowing what the different plug-ins are doing.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;"><a style="background: transparent; color: #29a8ff;" href="https://blog.ndepend.com/wp-content/uploads/layered-2.png" rel="nofollow"><img class="fr-fin fr-dib" style="vertical-align: middle; max-width: 100%; height: auto; text-align: center; margin: auto; display: block; float: none !important;" src="https://blog.ndepend.com/wp-content/uploads/layered-2.png" alt="" width="679" height="187"></a></p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">An example is a task scheduler. The microkernel could contain all the logic for scheduling and triggering tasks, while the plug-ins contain specific tasks. As long as the plug-ins adhere to a predefined API, the microkernel can trigger them without needing to know the implementation details.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">Another example is a workflow. The implementation of a workflow contains concepts like the order of the different steps, evaluating the results of steps, deciding what the next step is, etc. The specific implementation of the steps is less important to the core code of the workflow.</p> 
    <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Advantages</h3> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">This pattern provides great flexibility and extensibility.</li> 
     <li style="padding-bottom: 8px;">Some implementations allow for adding plug-ins while the application is running.</li> 
     <li style="padding-bottom: 8px;">Microkernel and plug-ins can be developed by separate teams.</li> 
    </ul> 
    <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Disadvantages</h3> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">It can be difficult to decide what belongs in the microkernel and what doesn’t.</li> 
     <li style="padding-bottom: 8px;">The predefined API might not be a good fit for future plug-ins.</li> 
    </ul> 
    <p style="margin-top: 5px; margin-bottom: 15px;"><strong style="">Ideal for</strong></p> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">Applications that take data from different sources, transform that data and writes it to different destinations</li> 
     <li style="padding-bottom: 8px;">Workflow applications</li> 
     <li style="padding-bottom: 8px;">Task and job scheduling applications</li> 
    </ul> 
    <h2 style="">CQRS</h2> 
    <p style="margin-top: 5px; margin-bottom: 15px;">CQRS is an acronym for&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://blog.ndepend.com/cqrs-understanding-first-principles/" rel="nofollow" target="_blank">Command and Query Responsibility Segregation</a>. The central concept of this pattern is that an application has read operations and write operations that must be totally separated. This also means that the model used for write operations (commands) will differ from the read models (queries). Furthermore, the data will be stored in different locations. In a relational database, this means there will be tables for the command model and tables for the read model. Some implementations even store the different models in totally different databases, e.g. SQL Server for the command model and MongoDB for the read model.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">This pattern is often combined with event sourcing, which we’ll cover below.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">How does it work exactly? When a user performs an action, the application sends a command to the command service. The command service retrieves any data it needs from the command database, makes the necessary manipulations and stores that back in the database. It then notifies the read service so that the read model can be updated. This flow can be seen below.<a style="background: transparent; color: #29a8ff;" href="https://blog.ndepend.com/wp-content/uploads/layered-3.png" rel="nofollow"><img class="fr-fin fr-dib" style="vertical-align: middle; max-width: 100%; height: auto; text-align: center; margin: auto; display: block; float: none !important;" src="https://blog.ndepend.com/wp-content/uploads/layered-3.png" alt="" width="633" height="271"></a></p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">When the application needs to show data to the user, it can retrieve the read model by calling the read service, as shown below.</p> 
    <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;"> <a style="background: transparent; color: #29a8ff;" href="https://blog.ndepend.com/wp-content/uploads/Layered-4.png" rel="nofollow"><img class="fr-fin fr-dib" style="vertical-align: middle; max-width: 100%; height: auto; text-align: center; margin: auto; display: block; float: none !important;" src="https://blog.ndepend.com/wp-content/uploads/Layered-4.png" alt="" width="658" height="269"></a>Advantages</h3> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">Command models can focus on business logic and validation while read models can be tailored to specific scenarios.</li> 
     <li style="padding-bottom: 8px;">You can avoid complex queries (e.g. joins in SQL) which makes the reads more performant.</li> 
    </ul> 
    <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Disadvantages</h3> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">Keeping the command and the read models in sync can become complex.</li> 
    </ul> 
    <p style="margin-top: 5px; margin-bottom: 15px;"><strong style="">Ideal for</strong></p> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">Applications that expect a high amount of reads</li> 
     <li style="padding-bottom: 8px;">Applications with complex domains</li> 
    </ul> 
    <h2 style="">Event Sourcing</h2> 
    <p style="margin-top: 5px; margin-bottom: 15px;">As I mentioned above, CQRS often goes hand in hand with event sourcing. This is a pattern where you don’t store the current state of your model in the database, but rather the events that happened to the model. So when the name of a customer changes, you won’t store the value in a “Name” column. You will store a “NameChanged” event with the new value (and possibly the old one too).</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">When you need to retrieve a model, you retrieve all its stored events and reapply them on a new object. We call this rehydrating an object.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">A real-life analogy of event sourcing is accounting. When you add an expense, you don’t change the value of the total. In accounting, a new line is added with the operation to be performed. If an error was made, you simply add a new line. To make your life easier, you could calculate the total every time you add a line. This total can be regarded as the read model. The example below should make it more clear.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;"><a style="background: transparent; color: #29a8ff;" href="https://blog.ndepend.com/wp-content/uploads/layered-5.png" rel="nofollow"><img class="fr-fin fr-dib" style="vertical-align: middle; max-width: 100%; height: auto; text-align: center; margin: auto; display: block; float: none !important;" src="https://blog.ndepend.com/wp-content/uploads/layered-5.png" alt="" width="512" height="189"></a></p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">You can see that we made an error when adding Invoice 201805. Instead of changing the line, we added two new lines: first, one to cancel the wrong line, then a new and correct line. This is how event sourcing works. You never remove events, because they have undeniably happened in the past. To correct situations, we add new events.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">Also, note how we have a cell with the total value. This is simply a sum of all values in the cells above. In Excel, it automatically updates so you could say it synchronizes with the other cells. It is the read model, providing an easy view for the user.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">Event sourcing is often combined with CQRS because rehydrating an object can have a performance impact, especially when there are a lot of events for the instance. A fast read model can significantly improve the response time of the application.</p> 
    <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Advantages</h3> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">This software architecture pattern can provide an audit log out of the box. Each event represents a manipulation of the data at a certain point in time.</li> 
    </ul> 
    <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Disadvantages</h3> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">It requires some discipline because you can’t just fix wrong data with a simple edit in the database.</li> 
     <li style="padding-bottom: 8px;">It’s not a trivial task to change the structure of an event. For example, if you add a property, the database still contains events without that data. Your code will need to handle this missing data graciously.</li> 
    </ul> 
    <p style="margin-top: 5px; margin-bottom: 15px;"><strong style="">Ideal for applications that</strong></p> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">Need to publish events to external systems</li> 
     <li style="padding-bottom: 8px;">Will be built with CQRS</li> 
     <li style="padding-bottom: 8px;">Have complex domains</li> 
     <li style="padding-bottom: 8px;">Need an audit log of changes to the data</li> 
    </ul> 
    <h2 style="">Microservices</h2> 
    <p style="margin-top: 5px; margin-bottom: 15px;">When you write your application as a set of microservices, you’re actually writing multiple applications that will work together. Each microservice has its own distinct responsibility and teams can develop them independently of other microservices. The only dependency between them is the communication. As microservices communicate with each other, you will have to make sure messages sent between them remain backwards-compatible. This requires some coordination, especially when different teams are responsible for different microservices.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">A diagram can explain.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;"><a style="background: transparent; color: #29a8ff;" href="https://blog.ndepend.com/wp-content/uploads/layered-6.png" rel="nofollow"><img class="fr-fin fr-dib" style="vertical-align: middle; max-width: 100%; height: auto; text-align: center; margin: auto; display: block; float: none !important;" src="https://blog.ndepend.com/wp-content/uploads/layered-6.png" alt="" width="671" height="353"></a>In the above diagram, the application calls a central API that forwards the call to the correct microservice. In this example, there are separate services for the user profile, inventory, orders, and payment. You can imagine this is an application where the user can order something. The separate microservices can call each other too. For example, the payment service may notify the orders service when a payment succeeds. The orders service could then call the inventory service to adjust the stock.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">There is no clear rule of how big a microservice can be. In the previous example, the user profile service may be responsible for data like the username and password of a user, but also the home address, avatar image, favorites, etc. It could also be an option to split all those responsibilities into even smaller microservices.</p> 
    <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Advantages</h3> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">You can write, maintain, and deploy each microservice separately.</li> 
     <li style="padding-bottom: 8px;">A microservices architecture should be easier to scale, as you can scale only the microservices that need to be scaled. There’s no need to scale the less frequently used pieces of the application.</li> 
     <li style="padding-bottom: 8px;">It’s easier to rewrite pieces of the application because they’re smaller and less coupled to other parts.</li> 
    </ul> 
    <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Disadvantages</h3> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">Contrary to what you might expect, it’s actually easier to write a well-structured monolith at first and split it up into microservices later. With microservices, a lot of extra concerns come into play: communication, coordination, backward compatibility, logging, etc. Teams that miss the necessary skill to write a well-structured monolith will probably have a hard time writing a good set of microservices.</li> 
     <li style="padding-bottom: 8px;">A single action of a user can pass through multiple microservices. There are more points of failure, and when something does go wrong, it can take more time to pinpoint the problem.</li> 
    </ul> 
    <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: inherit; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Ideal for:</h3> 
    <ul style="margin-bottom: 10px;"> 
     <li style="padding-bottom: 8px;">Applications where certain parts will be used intensively and need to be scaled</li> 
     <li style="padding-bottom: 8px;">Services that provide functionality to several other applications</li> 
     <li style="padding-bottom: 8px;">Applications that would become very complex if combined into one monolith</li> 
     <li style="padding-bottom: 8px;">Applications where clear&nbsp;<a style="background: transparent; color: #29a8ff;" href="https://martinfowler.com/bliki/BoundedContext.html" rel="nofollow" target="_blank">bounded contexts</a>&nbsp;can be defined</li> 
    </ul> 
    <h2 style="">Combine</h2> 
    <p style="margin-top: 5px; margin-bottom: 15px;">I’ve explained several software architecture patterns, as well as their advantages and disadvantages. But there are more patterns than the ones I’ve laid out here. It is also not uncommon to combine several of these patterns. They aren’t always mutually exclusive. For example, you could have several microservices and have some of them use the layered pattern, while others use CQRS and event sourcing.</p> 
    <p style="margin-top: 5px; margin-bottom: 15px;">The important thing to remember is that there isn’t one solution that works everywhere. When we ask the question of which pattern to use for an application, the age-old answer still applies: “it depends.” You should weigh in on the pros and cons of a solution and make a well-informed decision.</p> 
   </div> 
  </div> 
  <div class="article-bumper article-bumper-bottom ng-binding ng-scope" style="font-weight: 400; color: #808285; padding: 10px 0px; line-height: 1.45; display: inline-block; margin: 25px 0px 0px; width: 1148px; border-top: 1px solid #d9dcdd; border-bottom: 1px solid #d9dcdd;"> 
   <a style="background: transparent; color: #29a8ff;" href="https://dzone.com/go?i=290421&amp;u=https%3A%2F%2Fwww.instana.com%2Ftrial%3Futm_source%3DdZone%26utm_medium%3Dpre_post_article_text_ad%26utm_campaign%3Dinstana_trial%26utm_content%3Dgot_cloud_get_instana" rel="nofollow">Automatically manage containers and microservices</a>&nbsp;with better control and performance using&nbsp;
   <a style="background: transparent; color: #29a8ff;" href="https://dzone.com/go?i=290421&amp;u=https%3A%2F%2Fwww.instana.com%2Ftrial%3Futm_source%3DdZone%26utm_medium%3Dpre_post_article_text_ad%26utm_campaign%3Dinstana_trial%26utm_content%3Dgot_cloud_get_instana" rel="nofollow">Instana&nbsp;APM</a>. Try it for yourself&nbsp;
   <a style="background: transparent; color: #29a8ff;" href="https://dzone.com/go?i=290421&amp;u=https%3A%2F%2Fwww.instana.com%2Ftrial%3Futm_source%3DdZone%26utm_medium%3Dpre_post_article_text_ad%26utm_campaign%3Dinstana_trial%26utm_content%3Dgot_cloud_get_instana" rel="nofollow">today</a>.
  </div> 
  <div class="article-topics" style="margin: 20px 0px; color: #333333; font-size: 14px; font-weight: 500;"> 
   <div class="topic-label" style="width: 50px; display: inline;">
    Topics:
   </div> &nbsp; 
   <div class="topics" style=""> 
    <span class="topics-tag" style="margin-right: 3px; font-size: 12px; color: #737981; display: inline-block;">SOFTWARE ARCHITECTURE ,</span>
    <span class="topics-tag" style="margin-right: 3px; font-size: 12px; color: #737981; display: inline-block;">DESIGN PATTERNS ,</span>
    <span class="topics-tag" style="margin-right: 3px; font-size: 12px; color: #737981; display: inline-block;">MICROSERVICES ,</span>
    <span class="topics-tag" style="margin-right: 3px; font-size: 12px; color: #737981; display: inline-block;">CQRS ,</span>
    <span class="topics-tag" style="margin-right: 3px; font-size: 12px; color: #737981; display: inline-block;">EVENT SOURCING</span> 
   </div> 
   <div class="topics" style="">
    &nbsp;
   </div> 
   <div class="topics" style="">
    &nbsp;
   </div> 
   <div class="topics" style="">
    &nbsp;
   </div> 
  </div> 
 </div> 
</div>