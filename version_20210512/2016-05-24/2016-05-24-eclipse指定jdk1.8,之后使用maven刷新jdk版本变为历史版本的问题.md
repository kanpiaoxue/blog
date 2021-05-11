#eclipse指定jdk1.8,之后使用maven刷新jdk版本变为历史版本的问题
###发表时间：2016-05-24
###分类：eclipse,maven
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2300656" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2300656</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>今天要将一个项目的jdk由1.6的版本变更为1.8的版本。</p> 
 <p>我将eclipse的Preference -&gt; Java -&gt; Instanled JREs 里面的jdk改为jdk1.8，将<span style="line-height: 1.5;">Preference -&gt; Java -&gt; Compiler 里面的1.6改为1.8.</span></p> 
 <p><span style="line-height: 1.5;">为了让项目在eclipse里面刷新，我使用快捷键“ALT + F5”刷新了项目。结果，我发现eclipse的</span><span style="line-height: 1.5;">Instanled JREs</span><span style="line-height: 1.5;">&nbsp;和</span><span style="line-height: 1.5;">Compiler</span><span style="line-height: 1.5;">&nbsp;有变更为jdk1.6 。我以为eclipse有啥问题呢，重复尝试了好几次，发现还是这个样子。</span></p> 
 <p><span style="line-height: 1.5;">于是乎我就去万能的Google搜索了一下。发现了有人和我遇到了同样的问题。</span></p> 
 <p><span style="line-height: 1.5;">地址如下：</span></p> 
 <p><a href="http://stackoverflow.com/questions/9926798/eclipse-jre-system-library-j2se-1-5">http://stackoverflow.com/questions/9926798/eclipse-jre-system-library-j2se-1-5</a></p> 
 <p>&nbsp;</p> 
 <p>内容如下：</p> 
 <p>------------------------------------------------------------------------------------------------------------------------------</p> 
 <div id="question-header" style="margin-top: 0px; margin-right: 0px; margin-left: 0px; padding: 5px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #e4e6e8; font-size: 13px; clear: both; color: #242729; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; line-height: 16.9px;"> 
  <h1 style="border: 0px; font-size: 22px; line-height: 1.3;"><a class="question-hyperlink" style="margin: 0px 0px 0.5em; padding: 0px; border: 0px; font-size: 24px; color: #242729; cursor: pointer; font-weight: normal; line-height: 1.35;" href="http://stackoverflow.com/questions/9926798/eclipse-jre-system-library-j2se-1-5">Eclipse JRE System Library [J2SE-1.5]</a></h1> 
 </div> 
 <div id="mainbar" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; float: left; width: 728px; color: #242729; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; line-height: 16.9px;"> 
  <div id="question" class="question" style="margin: 0px; padding: 0px; border: 0px; clear: both;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-spacing: 0px; border-collapse: collapse;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This question shows research effort; it is useful and clear">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #6a737c;">30</span>
        <a class="vote-down-off" style="" title="This question does not show any research effort; it is unclear or not useful">down vote</a>
        <a class="star-off" style="" href="http://stackoverflow.com/questions/9926798/eclipse-jre-system-library-j2se-1-5">favorite</a> 
        <div class="favoritecount" style="margin: 0px; padding: 0px; border: 0px;">
         <span style="margin: 0px; padding: 0px; border: 0px; color: #6a737c;">9</span>
        </div> 
       </div> </td> 
      <td class="postcell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div style="margin: 0px; padding: 0px; border: 0px;"> 
        <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
         <p style="margin-bottom: 1em; border: 0px; clear: both;">I'm using Eclipse EE 3.7 with m2e plugin installed. I have JDK7 set in eclipse. When I import maven projects, the JRE is set to&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-size: 13px; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; white-space: pre-wrap; background-color: #eff0f1;">JRE System Library [J2SE-1.5]</code>, So i have compilation issues with java 6 related stuff. Instead I want the JRE in eclipse to be by default set to JRE&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-size: 13px; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; white-space: pre-wrap; background-color: #eff0f1;">System Library [J2SE-1.6]</code></p> 
         <p style="margin-bottom: 1em; border: 0px; clear: both;">When i try to open a new project in eclipse File -&gt; new -&gt; Java project on the first screen i have an option to choose JRE and the third option is&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-size: 13px; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; white-space: pre-wrap; background-color: #eff0f1;">Use default JRE (currently 'jdk1.7.0_03')</code></p> 
         <p style="margin-bottom: 1em; border: 0px; clear: both;">From this i can see that the default JRE in Eclipse is 1.7, but when i import new Maven projects, the JRE is set to 1.5 by default.</p> 
         <p style="margin-bottom: 1em; border: 0px; clear: both;">Any help, how can i do this?</p> 
        </div> 
        <div class="post-taglist" style="margin: 0px 0px 10px; padding: 0px; border: 0px; clear: both;"> 
         <a class="post-tag js-gps-track" style="margin: 2px 2px 2px 0px; padding: 0.4em 0.5em; border: 1px solid transparent; font-size: 12px; color: #39739d; cursor: pointer; display: inline-block; line-height: 1; white-space: nowrap; text-align: center; border-radius: 0px; background-color: #e1ecf4;" title="show questions tagged 'java'" href="http://stackoverflow.com/questions/tagged/java" rel="tag">java</a>&nbsp;
         <a class="post-tag js-gps-track" style="margin: 2px 2px 2px 0px; padding: 0.4em 0.5em; border: 1px solid transparent; font-size: 12px; color: #39739d; cursor: pointer; display: inline-block; line-height: 1; white-space: nowrap; text-align: center; border-radius: 0px; background-color: #e1ecf4;" title="show questions tagged 'eclipse'" href="http://stackoverflow.com/questions/tagged/eclipse" rel="tag">eclipse</a>&nbsp;
         <a class="post-tag js-gps-track" style="margin: 2px 2px 2px 0px; padding: 0.4em 0.5em; border: 1px solid transparent; font-size: 12px; color: #39739d; cursor: pointer; display: inline-block; line-height: 1; white-space: nowrap; text-align: center; border-radius: 0px; background-color: #e1ecf4;" title="show questions tagged 'm2eclipse'" href="http://stackoverflow.com/questions/tagged/m2eclipse" rel="tag">m2eclipse</a>&nbsp;
         <a class="post-tag js-gps-track" style="margin: 2px 2px 2px 0px; padding: 0.4em 0.5em; border: 1px solid transparent; font-size: 12px; color: #39739d; cursor: pointer; display: inline-block; line-height: 1; white-space: nowrap; text-align: center; border-radius: 0px; background-color: #e1ecf4;" title="show questions tagged 'm2e'" href="http://stackoverflow.com/questions/tagged/m2e" rel="tag">m2e</a> 
        </div> 
        <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-spacing: 0px; border-collapse: collapse; width: 660px;">
         <tbody style="margin: 0px; padding: 0px; border: 0px;">
          <tr style="margin: 0px; padding: 0px; border: 0px;"> 
           <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
            <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
             <a id="link-post-9926798" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; color: #848d95; cursor: pointer; display: inline-block;" title="short permalink to this question" href="http://stackoverflow.com/q/9926798">share</a>
             <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; color: #848d95; cursor: pointer; display: inline-block;" title="" href="http://stackoverflow.com/posts/9926798/edit">improve this question</a> 
            </div> </td> 
           <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
            <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #6a737c;"> 
             <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
              <a style="margin: 0px; padding: 0px; border: 0px; color: #0077cc; cursor: pointer;" title="show all edits to this post" href="http://stackoverflow.com/posts/9926798/revisions">edited&nbsp;<span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2012-03-29 14:09:21Z">Mar 29 '12 at 14:09</span></a>
             </div> 
             <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;">
              &nbsp;
             </div> 
             <div class="user-details" style="">
              &nbsp;
             </div> 
            </div> </td> 
           <td class="post-signature owner" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px; background-color: #e0eaf1;"> 
            <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #6a737c;"> 
             <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
              asked&nbsp;
              <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2012-03-29 13:53:36Z">Mar 29 '12 at 13:53</span> 
             </div> 
             <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
              <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; overflow: hidden; width: 32px; height: 32px;">
               <img style="margin: 0px auto; padding: 0px; width: 32px; height: 32px; border-radius: 1px;" src="https://i.stack.imgur.com/XVtno.jpg?s=32&amp;g=1" alt="" width="32" height="32">
              </div> 
             </div> 
             <div class="user-details" style=""> 
              <a style="margin: 0px; padding: 0px; border: 0px; color: #0077cc; cursor: pointer;" href="http://stackoverflow.com/users/1042999/sinisa229-mihajlovski">sinisa229 mihajlovski</a> 
              <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
               <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">1,191</span>
               <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="1 gold badge"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px;">1</span></span>
               <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="11 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px;">11</span></span>
               <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="19 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px;">19</span></span> 
              </div> 
             </div> 
            </div> </td> 
          </tr>
         </tbody>
        </table> 
       </div> </td> 
     </tr> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;">&nbsp;</td> 
      <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;"> 
       <div id="comments-9926798" class="comments " style=""> 
        <table style="margin: 0px; padding: 0px; border: 0px; border-spacing: 0px; border-collapse: collapse; width: 660px;">
         <tbody style="margin: 0px; padding: 0px; border: 0px;">
          <tr id="comment-55899521" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #eff0f1; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-spacing: 0px; border-collapse: collapse;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #eff0f1; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">I am experiencing a similary problem. Whatever the JRE System Library is set to, performing a Project&gt;Maven&gt;Update Project... resets the JRE System Library to J2SE-1.5.</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; color: #0077cc; cursor: pointer; white-space: nowrap;" title="366 reputation" href="http://stackoverflow.com/users/3102471/mbmast">mbmast</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #9199a1;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #005999; cursor: pointer;" href="http://stackoverflow.com/questions/9926798/eclipse-jre-system-library-j2se-1-5#comment55899521_9926798">Dec 3 '15 at 18:14</a></span> 
            </div> </td> 
          </tr>
         </tbody>
        </table> 
       </div> 
       <div id="comments-link-9926798" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; color: #848d95; cursor: pointer;" title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <div id="answers" style="margin: 0px; padding: 10px 0px 0px; border: 0px; clear: both; width: 728px;"> 
   <a style="margin: 0px; padding: 0px; border: 0px; color: #0077cc; cursor: pointer;" name="tab-top"></a> 
   <div id="answers-header" style="margin: 10px 0px 0px; padding: 0px; border: 0px; width: 728px;"> 
    <div class="subheader answers-subheader" style="margin: 0px 0px 10px; padding: 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #e4e6e8; clear: both; height: 40px;"> 
     <h2 style="margin-bottom: 0px; border: 0px; font-size: 18px; line-height: 1.3; float: left; font-weight: 400; color: #3b4045;">2 Answers</h2> 
     <div style="margin: 0px; padding: 0px; border: 0px;"> 
      <div id="tabs" style="margin: 0px; padding: 0px; border: 0px; float: right;"> 
       <a style="margin: 0px 8px 0px 0px; padding: 13px 10px; border: 1px solid transparent; font-size: 12px; color: #848d95; cursor: pointer; float: left; line-height: 1;" title="Answers with the latest activity first" href="http://stackoverflow.com/questions/9926798/eclipse-jre-system-library-j2se-1-5?answertab=active#tab-top">active</a>
       <a style="margin: 0px 8px 0px 0px; padding: 13px 10px; border: 1px solid transparent; font-size: 12px; color: #848d95; cursor: pointer; float: left; line-height: 1;" title="Answers in the order they were provided" href="http://stackoverflow.com/questions/9926798/eclipse-jre-system-library-j2se-1-5?answertab=oldest#tab-top">oldest</a>
       <a class="youarehere" style="margin: 0px; padding: 13px 10px 14px; border-width: 1px; border-style: solid; border-color: #e4e6e8 #e4e6e8 transparent; font-size: 12px; color: #242729; cursor: pointer; float: left; line-height: 1;" title="Answers with the highest score first" href="http://stackoverflow.com/questions/9926798/eclipse-jre-system-library-j2se-1-5?answertab=votes#tab-top">votes</a> 
      </div> 
     </div> 
    </div> 
   </div> 
   <a style="margin: 0px; padding: 0px; border: 0px; color: #0077cc; cursor: pointer;" name="9927172"></a> 
   <div id="answer-9927172" class="answer accepted-answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #e4e6e8; width: 728px;"> 
    <table style="margin: 0px; padding: 0px; border: 0px; border-spacing: 0px; border-collapse: collapse;">
     <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
      <tr style="margin: 0px; padding: 0px; border: 0px;"> 
       <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
        <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
         <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
         <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #6a737c;">61</span>
         <a class="vote-down-off" style="" title="This answer is not useful">down vote</a>
         <span class="vote-accepted-on load-accepted-answer-date" style="" title="loading when this answer was accepted...">accepted</span> 
        </div> </td> 
       <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
        <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
         <p style="margin-bottom: 1em; border: 0px; clear: both;">The problem is not with Eclipse, but with the projects you're importing. m2e will set the project's JRE to match the maven project. The POM specifies the JRE version, and this is defaulted to 1.5 if not present. You need this in the POM:</p> 
         <pre class="lang-java prettyprint prettyprinted"><code style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; white-space: inherit;"><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">build</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">plugins</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">plugin</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">groupId</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">org</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">.</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">apache</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">.</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">maven</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">.</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">plugins</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">groupId</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">artifactId</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">maven</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">-</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">compiler</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">-</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">plugin</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">artifactId</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">version</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="lit" style="margin: 0px; padding: 0px; border: 0px; color: #7d2727;">3.0</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">version</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">configuration</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">source</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="lit" style="margin: 0px; padding: 0px; border: 0px; color: #7d2727;">1.7</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">source</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">target</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="lit" style="margin: 0px; padding: 0px; border: 0px; color: #7d2727;">1.7</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">target</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">configuration</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">plugin</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">plugins</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">build</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span></code></pre> 
        </div> 
        <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-spacing: 0px; border-collapse: collapse; width: 660px;">
         <tbody style="margin: 0px; padding: 0px; border: 0px;">
          <tr style="margin: 0px; padding: 0px; border: 0px;"> 
           <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
            <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
             <a id="link-post-9927172" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; color: #848d95; cursor: pointer; display: inline-block;" title="short permalink to this answer" href="http://stackoverflow.com/a/9927172">share</a>
             <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; color: #848d95; cursor: pointer; display: inline-block;" title="" href="http://stackoverflow.com/posts/9927172/edit">improve this answer</a> 
            </div> </td> 
           <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
            <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #6a737c;"> 
             <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
              <a style="margin: 0px; padding: 0px; border: 0px; color: #0077cc; cursor: pointer;" title="show all edits to this post" href="http://stackoverflow.com/posts/9927172/revisions">edited&nbsp;<span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2015-07-22 08:38:12Z">Jul 22 '15 at 8:38</span></a>
             </div> 
             <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;">
              &nbsp;
             </div> 
             <div class="user-details" style="">
              &nbsp;
             </div> 
            </div> </td> 
           <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
            <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #6a737c;"> 
             <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
              answered&nbsp;
              <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2012-03-29 14:14:25Z">Mar 29 '12 at 14:14</span> 
             </div> 
             <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
              <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; overflow: hidden; width: 32px; height: 32px;">
               <img style="margin: 0px auto; padding: 0px; width: 32px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/98038439a9f244f4a92bed860ad28fd0?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
              </div> 
             </div> 
             <div class="user-details" style=""> 
              <a style="margin: 0px; padding: 0px; border: 0px; color: #0077cc; cursor: pointer;" href="http://stackoverflow.com/users/116509/artbristol">artbristol</a> 
              <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
               <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score 22,938" dir="ltr">22.9k</span>
               <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="4 gold badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px;">4</span></span>
               <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="37 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px;">37</span></span>
               <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="65 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px;">65</span></span> 
              </div> 
             </div> 
            </div> </td> 
          </tr>
         </tbody>
        </table> </td> 
      </tr> 
      <tr style="margin: 0px; padding: 0px; border: 0px;"> 
       <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;">&nbsp;</td> 
       <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;"> 
        <div id="comments-9927172" class="comments " style=""> 
         <table style="margin: 0px; padding: 0px; border: 0px; border-spacing: 0px; border-collapse: collapse; width: 660px;">
          <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
           <tr id="comment-12672877" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
            <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #eff0f1; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
             <table style="margin: 0px; padding: 0px; border: 0px; border-spacing: 0px; border-collapse: collapse;">
              <tbody style="margin: 0px; padding: 0px; border: 0px;">
               <tr style="margin: 0px; padding: 0px; border: 0px;"> 
                <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
                <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
               </tr>
              </tbody>
             </table> </td> 
            <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #eff0f1; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
             <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">It works, thanks</span>&nbsp;–&nbsp;
              <a class="comment-user owner" style="margin: 0px; padding: 1px 5px; border: 0px; color: #0077cc; cursor: pointer; white-space: nowrap; background-color: #e0eaf1;" title="1,191 reputation" href="http://stackoverflow.com/users/1042999/sinisa229-mihajlovski">sinisa229 mihajlovski</a>&nbsp;
              <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #9199a1;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #005999; cursor: pointer;" href="http://stackoverflow.com/questions/9926798/eclipse-jre-system-library-j2se-1-5#comment12672877_9927172">Mar 29 '12 at 15:11</a></span> 
             </div> </td> 
           </tr> 
           <tr id="comment-29732184" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
            <td class="comment-actions" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #eff0f1; font-size: 13px; width: 15px; vertical-align: top; line-height: 1.3;"> 
             <table style="margin: 0px; padding: 0px; border: 0px; border-spacing: 0px; border-collapse: collapse;">
              <tbody style="margin: 0px; padding: 0px; border: 0px;">
               <tr style="margin: 0px; padding: 0px; border: 0px;"> 
                <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;"><span class="cool" style="margin: 0px; padding: 0px 4px 0px 0px; border: 0px; color: #9199a1;" title="number of 'useful comment' votes received">1</span></td> 
                <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
               </tr>
              </tbody>
             </table> </td> 
            <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #eff0f1; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
             <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;"><a style="margin: 0px; padding: 0px; border: 0px; color: #005999; cursor: pointer;" href="http://maven.apache.org/plugins/maven-compiler-plugin/examples/compile-using-different-jdk.html" rel="nofollow">Here</a>&nbsp;is some more info from Maven site</span>&nbsp;–&nbsp;
              <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; color: #0077cc; cursor: pointer; white-space: nowrap;" title="790 reputation" href="http://stackoverflow.com/users/1594823/saik0">Saik0</a>&nbsp;
              <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #9199a1;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #005999; cursor: pointer;" href="http://stackoverflow.com/questions/9926798/eclipse-jre-system-library-j2se-1-5#comment29732184_9927172">Nov 14 '13 at 8:59</a></span> 
             </div> </td> 
           </tr> 
           <tr id="comment-34523048" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
            <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #eff0f1; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
             <table style="margin: 0px; padding: 0px; border: 0px; border-spacing: 0px; border-collapse: collapse;">
              <tbody style="margin: 0px; padding: 0px; border: 0px;">
               <tr style="margin: 0px; padding: 0px; border: 0px;"> 
                <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
                <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
               </tr>
              </tbody>
             </table> </td> 
            <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #eff0f1; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
             <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">for people who have more than one project this question could also be of interest<a style="margin: 0px; padding: 0px; border: 0px; color: #005999; cursor: pointer;" title="default maven compiler setting" href="https://stackoverflow.com/questions/2531650/default-maven-compiler-setting">stackoverflow.com/questions/2531650/…</a></span>&nbsp;–&nbsp;
              <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; color: #0077cc; cursor: pointer; white-space: nowrap;" title="599 reputation" href="http://stackoverflow.com/users/649923/xtroce">Xtroce</a>&nbsp;
              <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #9199a1;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #005999; cursor: pointer;" href="http://stackoverflow.com/questions/9926798/eclipse-jre-system-library-j2se-1-5#comment34523048_9927172">Mar 26 '14 at 14:37</a></span> 
             </div> </td> 
           </tr> 
           <tr id="comment-50723802" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
            <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #eff0f1; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
             <table style="margin: 0px; padding: 0px; border: 0px; border-spacing: 0px; border-collapse: collapse;">
              <tbody style="margin: 0px; padding: 0px; border: 0px;">
               <tr style="margin: 0px; padding: 0px; border: 0px;"> 
                <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
                <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
               </tr>
              </tbody>
             </table> </td> 
            <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #eff0f1; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
             <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">I put it in &lt;build&gt;&lt;plugins&gt;&lt;/plugins&gt;&lt;/build&gt; of pom file. It works, thanks!</span>&nbsp;–&nbsp;
              <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; color: #0077cc; cursor: pointer; white-space: nowrap;" title="299 reputation" href="http://stackoverflow.com/users/1929092/jugal-panchal">Jugal Panchal</a>&nbsp;
              <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #9199a1;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #005999; cursor: pointer;" href="http://stackoverflow.com/questions/9926798/eclipse-jre-system-library-j2se-1-5#comment50723802_9927172">Jul 12 '15 at 20:39</a></span> 
             </div> </td> 
           </tr> 
          </tbody>
         </table> 
        </div> 
        <div id="comments-link-9927172" style="margin: 0px; padding: 0px; border: 0px;">
         <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; color: #848d95; cursor: pointer;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
        </div> </td> 
      </tr> 
     </tbody>
    </table> 
   </div> 
   <div id="adzerk1476115548" class="everyonelovesstackoverflow" style="margin: 0px 0px 10px; padding: 0px; border: 0px;">
    &nbsp;
   </div> 
   <a style="margin: 0px; padding: 0px; border: 0px; color: #0077cc; cursor: pointer;" name="35307278"></a> 
   <div id="answer-35307278" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #e4e6e8; width: 728px;"> 
    <table style="margin: 0px; padding: 0px; border: 0px; border-spacing: 0px; border-collapse: collapse;">
     <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
      <tr style="margin: 0px; padding: 0px; border: 0px;"> 
       <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
        <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
         <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
         <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #6a737c;">0</span>
         <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
        </div> </td> 
       <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
        <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
         <p style="margin-bottom: 1em; border: 0px; clear: both;">artbristol gave the correct answer (and I upvoted him).</p> 
         <p style="margin-bottom: 1em; border: 0px; clear: both;">That was in 2012. Here is an update more appropriate for today (2016, Java 8, Spring 4.x/Servlet 3.x):</p> 
         <pre class="lang-java prettyprint prettyprinted"><code style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; white-space: inherit;"><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">plugin</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">groupId</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">org</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">.</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">apache</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">.</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">maven</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">.</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">plugins</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">groupId</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">artifactId</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">maven</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">-</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">compiler</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">-</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">plugin</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">artifactId</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">version</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="lit" style="margin: 0px; padding: 0px; border: 0px; color: #7d2727;">3.0</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">version</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">configuration</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">source</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="lit" style="margin: 0px; padding: 0px; border: 0px; color: #7d2727;">1.7</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">source</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">target</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="lit" style="margin: 0px; padding: 0px; border: 0px; color: #7d2727;">1.7</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">target</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">configuration</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&lt;/</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">plugin</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #303336;">&gt;</span></code></pre> 
        </div> 
        <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-spacing: 0px; border-collapse: collapse; width: 660px;">
         <tbody style="margin: 0px; padding: 0px; border: 0px;">
          <tr style="margin: 0px; padding: 0px; border: 0px;"> 
           <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
            <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
             <a id="link-post-35307278" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; color: #848d95; cursor: pointer; display: inline-block;" title="short permalink to this answer" href="http://stackoverflow.com/a/35307278">share</a>
             <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; color: #848d95; cursor: pointer; display: inline-block;" title="" href="http://stackoverflow.com/posts/35307278/edit">improve this answer</a> 
            </div> </td> 
           <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
            <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #6a737c;"> 
             <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
              answered&nbsp;
              <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2016-02-10 05:10:19Z">Feb 10 at 5:10</span> 
             </div> 
             <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
              <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; overflow: hidden; width: 32px; height: 32px;">
               <img style="margin: 0px auto; padding: 0px; width: 32px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/9a9793fdeb3b94e185c8c99c0238372f?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
              </div> 
             </div> 
             <div class="user-details" style=""> 
              <a style="margin: 0px; padding: 0px; border: 0px; color: #0077cc; cursor: pointer;" href="http://stackoverflow.com/users/421195/paulsm4">paulsm4</a> 
              <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
               <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score 54,228" dir="ltr">54.2k</span>
               <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="6 gold badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px;">6</span></span>
               <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="64 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px;">64</span></span>
               <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="89 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px;">89</span></span> 
              </div> 
             </div> 
            </div> </td> 
          </tr>
         </tbody>
        </table> </td> 
      </tr> 
      <tr style="margin: 0px; padding: 0px; border: 0px;"> 
       <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;">&nbsp;</td> 
       <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;"> 
        <div id="comments-link-35307278" style="margin: 0px; padding: 0px; border: 0px;">
         <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; color: #848d95; cursor: pointer;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
        </div> </td> 
      </tr> 
     </tbody>
    </table> 
   </div> 
  </div> 
 </div> 
 <p>------------------------------------------------------------------------------------------------------------------------------</p> 
 <p>&nbsp;</p> 
 <p>按照上面的提示，我将项目的pom.xml的</p> 
 <p>&lt;plugin&gt;</p> 
 <p>&nbsp; &nbsp; &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;</p> 
 <p>&nbsp; &nbsp; &lt;artifactId&gt;maven-compiler-plugin&lt;/artifactId&gt;</p> 
 <p>&nbsp; &nbsp; &lt;version&gt;${maven-compiler-plugin.version}&lt;/version&gt;</p> 
 <p>&nbsp; &nbsp; &lt;configuration&gt;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;source&gt;1.6&lt;/source&gt;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;target&gt;1.6&lt;/target&gt;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;encoding&gt;UTF-8&lt;/encoding&gt;</p> 
 <p>&nbsp; &nbsp; &lt;/configuration&gt;</p> 
 <p>&lt;/plugin&gt;</p> 
 <p>修改一下就好了。如下：</p> 
 <p>&lt;plugin&gt;</p> 
 <p>&nbsp; &nbsp; &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;</p> 
 <p>&nbsp; &nbsp; &lt;artifactId&gt;maven-compiler-plugin&lt;/artifactId&gt;</p> 
 <p>&nbsp; &nbsp; &lt;version&gt;${maven-compiler-plugin.version}&lt;/version&gt;</p> 
 <p>&nbsp; &nbsp; &lt;configuration&gt;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;source&gt;1.8&lt;/source&gt;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;target&gt;1.8&lt;/target&gt;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;encoding&gt;UTF-8&lt;/encoding&gt;</p> 
 <p>&nbsp; &nbsp; &lt;/configuration&gt;</p> 
 <p>&lt;/plugin&gt;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>