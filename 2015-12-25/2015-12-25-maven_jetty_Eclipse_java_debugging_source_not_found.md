#maven jetty Eclipse java debugging: source not found
###发表时间：2015-12-25
###分类：maven,jetty,eclipse,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2266665" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2266665</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>地址：&nbsp;<a href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found">http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <div id="question" class="question" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; clear: both; color: #222426; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; line-height: 16.8999996185303px;"> 
  <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
   <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
    <tr style="margin: 0px; padding: 0px; border: 0px;"> 
     <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
      <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
       <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">64</span>
       <a class="vote-down-off" style="" title="This question does not show any research effort; it is unclear or not useful">down vote</a>
       <a class="star-off" style="" title="This is a favorite question (click again to undo)" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found">favorite</a> 
       <div class="favoritecount" style="margin: 0px; padding: 0px; border: 0px;">
        <span style="margin: 0px; padding: 0px; border: 0px; color: #777777;">25</span>
       </div> 
      </div> </td> 
     <td class="postcell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
      <div style="margin: 0px; padding: 0px; border: 0px;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">While debugging a java app in eclipse I receive a "<strong style="margin: 0px; padding: 0px; border: 0px;">Source not found</strong>" error in two cases:</p> 
        <ul style="margin-bottom: 1em; margin-left: 30px; border: 0px;"> 
         <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px;">Stepping in to a file in a different project which is already imported</li> 
         <li style="margin-bottom: 0px; margin-left: 0px; border: 0px;">Stepping in to a file in an installed maven repository</li> 
        </ul> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">The files are there, but eclipse won't step into them, instead it shows a button to "<strong style="margin: 0px; padding: 0px; border: 0px;">attach source</strong>"</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">I tried attaching (which opened a dialog to define a variable?!) and eclipse did jump to the file, but the debugger could not inspect any variables there. Also manually attaching the source for each dependency isn't practical, as in my case there are thousands of dependency files.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">I'm new to&nbsp;<em style="margin: 0px; padding: 0px; border: 0px;">eclipse\java</em>&nbsp;so an explanation of why this is happening + how to resolve this would help a lot!</p> 
       </div> 
       <div class="post-taglist" style="margin: 0px 0px 10px; padding: 0px; border: 0px; clear: both;"> 
        <a class="post-tag js-gps-track" style="" title="show questions tagged 'java'" href="http://stackoverflow.com/questions/tagged/java" rel="tag">java</a>&nbsp;
        <a class="post-tag js-gps-track" style="" title="show questions tagged 'eclipse'" href="http://stackoverflow.com/questions/tagged/eclipse" rel="tag">eclipse</a>&nbsp;
        <a class="post-tag js-gps-track" style="" title="show questions tagged 'debugging'" href="http://stackoverflow.com/questions/tagged/debugging" rel="tag">debugging</a> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-6174550" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this question" href="http://stackoverflow.com/q/6174550">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/6174550/edit">improve this question</a> 
           </div> </td> 
          <td class="post-signature owner" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px; background-color: #e0eaf1;"> 
           <div class="user-info user-hover" style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             asked&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2011-05-30 09:36:46Z">May 30 '11 at 9:36</span> 
            </div> 
            <div class="user-gravatar32" style=""> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/8c45eeae6f3bdb3e49b50a0b8241f6d4?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/348545/jonathan">Jonathan</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score 18097" dir="ltr">18.1k</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="42 gold badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">42</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="150 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">150</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="230 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">230</span></span> 
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
      <div id="comments-link-6174550" style="margin: 0px; padding: 0px; border: 0px;">
       <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.">add a comment</a>
      </div> </td> 
    </tr> 
   </tbody>
  </table> 
 </div> 
 <div id="answers" style="margin: 0px; padding: 10px 0px 0px; border: 0px; font-size: 13px; clear: both; width: 728px; color: #222426; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; line-height: 16.8999996185303px;"> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="tab-top"></a> 
  <div id="answers-header" style="margin: 10px 0px 0px; padding: 0px; border: 0px; width: 728px;"> 
   <div class="subheader answers-subheader" style="margin: 0px 0px 15px; padding: 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #eaebec; clear: both; height: 34px;"> 
    <h2 style="margin-bottom: 0px; border: 0px; font-size: 18px; line-height: 1.3; color: #444444; float: left; font-weight: 400;">20 Answers</h2> 
    <div style="margin: 0px; padding: 0px; border: 0px;"> 
     <div id="tabs" style="margin: 0px; padding: 0px; border: 0px; float: right; height: 38px;"> 
      <a style="margin: 0px 8px 0px 0px; padding: 10px; border-width: 2px 1px 1px; border-style: solid; border-color: transparent transparent #eaebec; font-size: 12px; cursor: pointer; color: #767d84; float: left; display: block; line-height: 1;" title="Answers with the latest activity first" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found?answertab=active#tab-top">active</a>
      <a style="margin: 0px 8px 0px 0px; padding: 10px; border-width: 2px 1px 1px; border-style: solid; border-color: transparent transparent #eaebec; font-size: 12px; cursor: pointer; color: #767d84; float: left; display: block; line-height: 1;" title="Answers in the order they were provided" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found?answertab=oldest#tab-top">oldest</a>
      <a class="youarehere" style="margin: 0px; padding: 10px; border-width: 2px 1px 1px; border-style: solid; border-color: #f69c55 #eaebec #ffffff; font-size: 12px; cursor: pointer; color: #222426; float: left; display: block; line-height: 1;" title="Answers with the highest score first" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found?answertab=votes#tab-top">votes</a> 
     </div> 
    </div> 
   </div> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="6179462"></a> 
  <div id="answer-6179462" class="answer accepted-answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">21</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a>
        <span class="vote-accepted-on load-accepted-answer-date" style="" title="loading when this answer was accepted...">accepted</span> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Eclipse debugging works with the class&nbsp;<em style="margin: 0px; padding: 0px; border: 0px;">actually loaded</em>&nbsp;by the program.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">The symptoms you describe sounds like the class in question was not found in the project, but in a distribution jar without debug info found&nbsp;<em style="margin: 0px; padding: 0px; border: 0px;">before</em>&nbsp;the project you are working with.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">This can happen for several reasons but have a look at the location where the classes showing this behaviour is found (look in the navigation pane to identify it). You will most likely need to change the build path of the project to avoid using this jar and have the JVM use the project instead.</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-6179462" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/6179462">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/6179462/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" title="show all edits to this post" href="http://stackoverflow.com/posts/6179462/revisions">edited&nbsp;<span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2011-05-31 01:23:48Z">May 31 '11 at 1:23</span></a>
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;">
             &nbsp;
            </div> 
            <div class="user-details" style="">
             &nbsp;
            </div> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info user-hover" style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2011-05-30 18:08:23Z">May 30 '11 at 18:08</span> 
            </div> 
            <div class="user-gravatar32" style=""> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/2e71c1745ebc5401c8c8dfbf7c9a5d30?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/53897/thorbj%c3%b8rn-ravn-andersen">Thorbjørn Ravn Andersen</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score 45998" dir="ltr">46k</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="14 gold badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">14</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="104 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">104</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="223 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">223</span></span> 
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
       <div id="comments-6179462" class="comments " style=""> 
        <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
         <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
          <tr id="comment-15782245" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">hi thanks for all but i found this answer more usefull (stack over flow link)[<a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #005999;" title="eclipse dont have java doc to show information about class and methods how to a%5d" href="http://stackoverflow.com/questions/5815013/eclipse-dont-have-java-doc-to-show-information-about-class-and-methods-how-to-a%5D">stackoverflow.com/questions/5815013/…</a></span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="2326 reputation" href="http://stackoverflow.com/users/944593/shareef">shareef</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment15782245_6179462">Aug 8 '12 at 12:16</a></span> 
            </div> </td> 
          </tr> 
          <tr id="comment-22712857" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td class="comment-actions" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; width: 15px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;"><span class="warm" style="margin: 0px; padding: 0px 4px 0px 0px; border: 0px; color: #9b764f;" title="number of 'useful comment' votes received">6</span></td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">@shareef that link is about missing javadoc, not missing source.</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="45998 reputation" href="http://stackoverflow.com/users/53897/thorbj%c3%b8rn-ravn-andersen">Thorbjørn Ravn Andersen</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment22712857_6179462">Apr 11 '13 at 4:52</a></span> 
            </div> </td> 
          </tr> 
          <tr id="comment-53127166" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">@ACV Well, yes. Perhaps it is not as elaborate as you would like - could you let me know what you would like to have explained better?</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="45998 reputation" href="http://stackoverflow.com/users/53897/thorbj%c3%b8rn-ravn-andersen">Thorbjørn Ravn Andersen</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment53127166_6179462">Sep 17 at 20:22</a></span> 
            </div> </td> 
          </tr> 
         </tbody>
        </table> 
       </div> 
       <div id="comments-link-6179462" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <div id="adzerk1965102242" class="everyonelovesstackoverflow adzerk-vote" style="margin: 0px 0px 10px; padding: 0px; border: 0px;"> 
   <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" title="" href="http://engine.adzerk.net/r?e=eyJhdiI6NDE0LCJhdCI6NCwiYnQiOjAsImNtIjozMjI1MTQsImNoIjoxMTc4LCJjayI6e30sImNyIjoxMTk1NzgzLCJkaSI6IjJhNjRiMjFjYWZmMjRmMTg4YjE1NjRlYjVmNTFiZGVkIiwiZG0iOjEsImZjIjoxMjY5MTQyLCJmbCI6ODY0MjI1LCJpcCI6IjYxLjEzNS4xNjkuNzMiLCJrdyI6ImphdmEsZWNsaXBzZSxkZWJ1Z2dpbmciLCJudyI6MjIsInBjIjowLCJlYyI6MCwicHIiOjE2MDQsInJ0IjoxLCJyZiI6Imh0dHBzOi8vd3d3Lmdvb2dsZS5jb20uaGsvIiwic3QiOjgyNzcsInVrIjoidWUxLTljNmYxODY2ZDA0MDRmOTQ5NWU2OWY1NTk4YjVkM2VmIiwiem4iOjQ0LCJ0cyI6MTQ1MTAzNzg2NzQ5OCwiYmYiOnRydWUsInBuIjoiYWR6ZXJrMTk2NTEwMjI0MiIsInVyIjoiaHR0cDovL2NhcmVlcnMuc3RhY2tvdmVyZmxvdy5jb20vcHJvZHVjdHM_dXRtX3NvdXJjZT1zdGFja292ZXJmbG93LmNvbSZ1dG1fbWVkaXVtPWFkJnV0bV9jYW1wYWlnbj1lbXBsb3llcnMtc3VwZXJoZXJvZXMmdXRtX2NvbnRlbnQ9bWxiLXN1cGVyaGVyb2VzIn0&amp;s=wkX-g_Qfk3yXEcNp4L7FGBrPBQc" rel="nofollow" target="_blank"><img style="margin: 0px; padding: 0px;" title="" src="http://static.adzerk.net/Advertisers/543b9426d0914a5083cc19318c1ffbc4.png" alt="" width="728" height="90" border="0"></a>
   <img style="margin: 0px; padding: 0px;" src="http://engine.adzerk.net/i.gif?e=eyJhdiI6NDE0LCJhdCI6NCwiYnQiOjAsImNtIjozMjI1MTQsImNoIjoxMTc4LCJjayI6e30sImNyIjoxMTk1NzgzLCJkaSI6IjJhNjRiMjFjYWZmMjRmMTg4YjE1NjRlYjVmNTFiZGVkIiwiZG0iOjEsImZjIjoxMjY5MTQyLCJmbCI6ODY0MjI1LCJpcCI6IjYxLjEzNS4xNjkuNzMiLCJrdyI6ImphdmEsZWNsaXBzZSxkZWJ1Z2dpbmciLCJudyI6MjIsInBjIjowLCJlYyI6MCwicHIiOjE2MDQsInJ0IjoxLCJyZiI6Imh0dHBzOi8vd3d3Lmdvb2dsZS5jb20uaGsvIiwic3QiOjgyNzcsInVrIjoidWUxLTljNmYxODY2ZDA0MDRmOTQ5NWU2OWY1NTk4YjVkM2VmIiwiem4iOjQ0LCJ0cyI6MTQ1MTAzNzg2NzQ5OSwiYmYiOnRydWUsInBuIjoiYWR6ZXJrMTk2NTEwMjI0MiJ9&amp;s=TUschDir6PbFU0BQevqpJ7L2PKU" alt="" width="0px" height="0px" border="0"> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="22934568"></a> 
  <div id="answer-22934568" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">69</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Just 3 steps to configuration Eclipse IDE:</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Edit Source Lookup Select the Edit Source Lookup... command [ Edit Source Lookup ] to open the Source Path Dialog, which allows you to make changes to the source lookup path of the selected debug target.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;"><img style="margin: 0px; padding: 0px; max-width: 630px;" src="http://i.stack.imgur.com/aIYJA.png" alt="enter image description here"></p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;"><img style="margin: 0px; padding: 0px; max-width: 630px;" src="http://i.stack.imgur.com/53p7o.png" alt="enter image description here"></p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;"><img style="margin: 0px; padding: 0px; max-width: 630px;" src="http://i.stack.imgur.com/0aepF.png" alt="enter image description here"></p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">After updating the Source Lookup paths, you'll have to stop and restart your debug session. Otherwise, the file with the missing source will continue to show "missing source".</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-22934568" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/22934568">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/22934568/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info user-hover" style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" title="show all edits to this post" href="http://stackoverflow.com/posts/22934568/revisions">edited&nbsp;<span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2015-10-29 14:56:46Z">Oct 29 at 14:56</span></a>
            </div> 
            <div class="user-gravatar32" style=""> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/b27fe292c68b5b0e482d7104bb1d87cc?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/108146/ashnazg">ashnazg</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">3,807</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="1 gold badge"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">1</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="10 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">10</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="22 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">22</span></span> 
             </div> 
            </div> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info user-hover" style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2014-04-08 10:42:03Z">Apr 8 '14 at 10:42</span> 
            </div> 
            <div class="user-gravatar32" style=""> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/5d8ea9cfa5b6418f2ab584fa22412206?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/1533342/douglas-frari">Douglas Frari</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">1,143</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="1 gold badge"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">1</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="8 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">8</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="16 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">16</span></span> 
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
       <div id="comments-22934568" class="comments " style=""> 
        <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
         <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
          <tr id="comment-35111304" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td class="comment-actions" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; width: 15px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;"><span class="warm" style="margin: 0px; padding: 0px 4px 0px 0px; border: 0px; color: #9b764f;" title="number of 'useful comment' votes received">5</span></td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">Editing the Source Lookup actually worked for me. Thanks Douglas Frari</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="139 reputation" href="http://stackoverflow.com/users/629096/stephen-ebichondo">stephen ebichondo</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment35111304_22934568">Apr 10 '14 at 14:23</a></span> 
            </div> </td> 
          </tr> 
          <tr id="comment-42802953" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td class="comment-actions" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; width: 15px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;"><span class="cool" style="margin: 0px; padding: 0px 4px 0px 0px; border: 0px; color: #999999;" title="number of 'useful comment' votes received">1</span></td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">Works like a charm. Thanks!</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="375 reputation" href="http://stackoverflow.com/users/307133/carlos-a-junior">Carlos A. Junior</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment42802953_22934568">Nov 26 '14 at 16:36</a></span> 
            </div> </td> 
          </tr> 
          <tr id="comment-45614577" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td class="comment-actions" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; width: 15px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;"><span class="cool" style="margin: 0px; padding: 0px 4px 0px 0px; border: 0px; color: #999999;" title="number of 'useful comment' votes received">3</span></td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">and what if even that doesn't work... cause its not working for me</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="310 reputation" href="http://stackoverflow.com/users/3320962/saras-arya">Saras Arya</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment45614577_22934568">Feb 22 at 15:22</a></span> 
            </div> </td> 
          </tr> 
          <tr id="comment-51554699" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">not working for me either</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="77 reputation" href="http://stackoverflow.com/users/3951576/dave">Dave</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment51554699_22934568">Aug 4 at 16:30</a></span> 
            </div> </td> 
          </tr> 
          <tr id="comment-53862958" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td class="comment-actions" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; width: 15px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;"><span class="cool" style="margin: 0px; padding: 0px 4px 0px 0px; border: 0px; color: #999999;" title="number of 'useful comment' votes received">1</span></td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">Important!! Worked well, but only AFTER I stopped the running application and restarted it. Until I did that it seemed as though it still couldn't get the sources.</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="2416 reputation" href="http://stackoverflow.com/users/88252/jeach">Jeach</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment53862958_22934568">Oct 8 at 15:27</a></span> 
            </div> </td> 
          </tr> 
         </tbody>
        </table> 
       </div> 
       <div id="comments-link-22934568" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="6181216"></a> 
  <div id="answer-6181216" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">29</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">The symptoms perfectly describes the case when the found class doesn't have associated (or assigned) source.</p> 
        <ul style="margin-bottom: 1em; margin-left: 30px; border: 0px;"> 
         <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px;">You can associate the sources for JDK classes in&nbsp;<strong style="margin: 0px; padding: 0px; border: 0px;">Preferences &gt; Java &gt; Installed JRE</strong>. If JRE (not JDK) is detected as default JRE to be used, then your JDK classes won't have attached sources. Note that, not all of the JDK classes have provided sources, some of them are distributed in binary form only.</li> 
         <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px;">Classes from project's build path, added manually requires that you manually attach the associated source. The source can reside in a zip or jar file, in the workspace or in the filesystem. Eclipse will scan the zip, so your sources doesn't have to be in the root of the archive file, for example.</li> 
         <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px;">Classes, from dependencies coming from another plugins (maven, PDE, etc.). In this case, it is up to the plugin how the source will be provided. 
          <ul style="margin-bottom: 0px; margin-left: 30px; border: 0px;"> 
           <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px;"> <em style="margin: 0px; padding: 0px; border: 0px;">PDE</em>&nbsp;will require that each plugin have corresponding&nbsp;<em style="margin: 0px; padding: 0px; border: 0px;">XXX.source</em>&nbsp;bundle, which contains the source of the plugin. More information can be found&nbsp;<a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #005999;" href="http://aniszczyk.org/2007/12/05/fyi-new-style-source-bundles/">here</a>&nbsp;and&nbsp;<a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #005999;" href="http://wiki.eclipse.org/PDEBuild/Individual_Source_Bundles">here</a>.</li> 
           <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px;"> <em style="margin: 0px; padding: 0px; border: 0px;">m2eclipse</em>&nbsp;can fetch sources and javadocs for Maven dependencies if they are available. This feature should be enabled&nbsp;<em style="margin: 0px; padding: 0px; border: 0px;">m2eclipse</em>&nbsp;preferences (the option was named something like "<em style="margin: 0px; padding: 0px; border: 0px;">Download source and javadocs</em>".</li> 
           <li style="margin-bottom: 0px; margin-left: 0px; border: 0px;">For other plugins, you'll need to consult their documentation</li> 
          </ul> </li> 
         <li style="margin-bottom: 0px; margin-left: 0px; border: 0px;">Classes, which are loaded from your project are automatically matched with the sources from the project.</li> 
        </ul> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;"><em style="margin: 0px; padding: 0px; border: 0px;">But what if Eclipse still suggest that you attach source, even if I correctly set my classes and their sources:</em></p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">This almost always means that Eclipse is finding the class from different place than you expect. Inspect your source lookup path to see where it might get the wrong class. Update the path accordingly to your findings.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;"><em style="margin: 0px; padding: 0px; border: 0px;">Eclipse doesn't find anything at all, when breakpoint is hit:</em></p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">This happens, when you are source lookup path doesn't contain the class, which is currently loaded in the runtime. Even if the class is in the workspace, it can be invisible to the launch configuration, because Eclipse follows the source lookup path strictly and attaches only the dependencies of the project, which is currently debugged.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">An exception is the debugging bundles in&nbsp;<em style="margin: 0px; padding: 0px; border: 0px;">PDE</em>. In this case, because the runtime is composed from multiple projects, which doesn't have to declare dependencies on one another, Eclipse will automatically find the class in the workspace, even if it is not available in the source lookup path.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;"><em style="margin: 0px; padding: 0px; border: 0px;">I cannot see the variables when I hit a breakpoint or it just opens the source, but doesn't select the breakpoint line:</em></p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">This means that in the runtime, either the JVM or the classes themselves doesn't have the necessary debug information. Each time classes are compiled, debug information can be attached. To reduce the storage space of the classes, sometimes this information is omitted, which makes debugging such code a pain. Your only chance is to try and recompile with debug enabled.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;"><em style="margin: 0px; padding: 0px; border: 0px;">Eclipse source viewer shows different lines than those that are actually executed:</em></p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">It sometimes can show that empty space is executed as well. This means that your sources doesn't match your runtime version of the classes. Even if you think that this is not possible, it is, so make sure you setup the correct sources. Or your runtime match your latest changes, depending on what are you trying to do.</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-6181216" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/6181216">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/6181216/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" title="show all edits to this post" href="http://stackoverflow.com/posts/6181216/revisions">May 30 '11 at 22:22</a> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;">
             &nbsp;
            </div> 
            <div class="user-details" style="">
             &nbsp;
            </div> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info" style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-details" style="margin: 0px; padding: 0px; border: 0px; line-height: 17px; float: left; width: 187px;">
             <span class="community-wiki" style="margin: 0px; padding: 0px; border: 0px;" title="This post is community owned as of May 30 '11 at 22:22. Votes do not generate reputation, and it can be edited by users with 100 rep">community wiki</span>
            </div> 
            <br>
            <div class="user-details" style="margin: 0px; padding: 0px; border: 0px; line-height: 17px; float: left; width: 187px;">
             <a id="history-6181216" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" title="show revision history for this post" href="http://stackoverflow.com/posts/6181216/revisions">Danail Nachev</a>
            </div> 
           </div> </td> 
         </tr>
        </tbody>
       </table> </td> 
     </tr> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;">&nbsp;</td> 
      <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;"> 
       <div id="comments-link-6181216" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="14256822"></a> 
  <div id="answer-14256822" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">7</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">From&nbsp;<a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #005999;" href="http://www.coderanch.com/t/587493/vc/Debugging-Eclipse-Source">http://www.coderanch.com/t/587493/vc/Debugging-Eclipse-Source</a></p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">"When running in debug mode, right click on the running thread (in threads tab) and select Edit Source Lookup. At this point, you should be able to add the necessary project/jar which contains your source code."</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">I added my current project in this way, and it solved my problem</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-14256822" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/14256822">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/14256822/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2013-01-10 11:23:54Z">Jan 10 '13 at 11:23</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/dae1d88f6447706460d00687a9aff40f?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/1782309/vering">Vering</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">186</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="2 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">2</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="10 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">10</span></span> 
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
       <div id="comments-14256822" class="comments " style=""> 
        <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
         <tbody style="margin: 0px; padding: 0px; border: 0px;">
          <tr id="comment-53861577" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">I had to do this in the Debug view, there under "Remote Java Application" or "Java HotSpot VM".</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="3980 reputation" href="http://stackoverflow.com/users/923560/abdull">Abdull</a>
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment53861577_14256822">Oct 8 at 14:55</a></span> 
            </div> </td> 
          </tr>
         </tbody>
        </table> 
       </div> 
       <div id="comments-link-14256822" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="13182988"></a> 
  <div id="answer-13182988" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">3</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Remove the existing Debug Configuration and create a new one. That should resolve the problem.</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-13182988" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/13182988">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/13182988/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2012-11-01 18:07:08Z">Nov 1 '12 at 18:07</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/b60ce00a7671da8c7cbeeea9d596d157?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/1792191/rajneesh-sekharmantri">Rajneesh Sekharmantri</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">31</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="1 bronze badge"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">1</span></span> 
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
       <div id="comments-13182988" class="comments " style=""> 
        <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
         <tbody style="margin: 0px; padding: 0px; border: 0px;">
          <tr id="comment-38941479" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">I followed this and it worked. Possibly because I also added the desired java project folder on the new run/debug configuration's 'Source' tab. Maybe just adding the missing source folder/project to the 'Source' tab of the existing run/debug config can work without having to delete it first.</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="140 reputation" href="http://stackoverflow.com/users/315385/xilef">xilef</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment38941479_13182988">Jul 30 '14 at 13:26</a></span> 
            </div> </td> 
          </tr>
         </tbody>
        </table> 
       </div> 
       <div id="comments-link-13182988" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="6174690"></a> 
  <div id="answer-6174690" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">2</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Evidently, Eclipse does not automatically know where the source code for the dependent jars are. It is not clear why debugger could not inspect variables once the source was attached. One possibility is incorrect/incompatible source.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Assuming you have a maven project and the sources of the dependencies are downloaded and available in the local repository, you may want to install&nbsp;<a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #005999;" href="http://m2eclipse.sonatype.org/" rel="nofollow">m2eclipse</a>, the maven eclipse plugin and see if that helps in addressing your issue.</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-6174690" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/6174690">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/6174690/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info user-hover" style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2011-05-30 09:47:24Z">May 30 '11 at 9:47</span> 
            </div> 
            <div class="user-gravatar32" style=""> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/211ea8bb93bbd3df4eca1d59fe2c7e0d?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/254643/raghuram">Raghuram</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score 32737" dir="ltr">32.7k</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="5 gold badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">5</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="58 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">58</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="88 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">88</span></span> 
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
       <div id="comments-link-6174690" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="12832118"></a> 
  <div id="answer-12832118" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">2</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">I had the problem that my Eclipse was not debugging the source code of my project. I was getting a blank page with "Source code node found".</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Please click the Attach source code button. Then delete the "default" folder then click add and go to your project location and attach. This worked for me</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-12832118" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/12832118">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/12832118/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2012-10-11 04:15:14Z">Oct 11 '12 at 4:15</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/d1cbe359c1be3f525c9678a89799b5e8?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/1736867/avase">avase</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">21</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="1 bronze badge"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">1</span></span> 
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
       <div id="comments-12832118" class="comments " style=""> 
        <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
         <tbody style="margin: 0px; padding: 0px; border: 0px;">
          <tr id="comment-17361672" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">that was a simple and good reply.</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="787 reputation" href="http://stackoverflow.com/users/1547779/gapchoos">Gapchoos</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment17361672_12832118">Oct 11 '12 at 5:45</a></span> 
            </div> </td> 
          </tr>
         </tbody>
        </table> 
       </div> 
       <div id="comments-link-12832118" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="23289043"></a> 
  <div id="answer-23289043" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">2</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">I had similar problem with my eclipse maven project. I fought with this issue quite a long time then I tried to rebuild projet with</p> 
        <pre class="lang-java prettyprint prettyprinted"><code style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; white-space: inherit;"><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #000000;">mvn clean eclipse</span><span class="pun" style="margin: 0px; padding: 0px; border: 0px; color: #000000;">:</span><span class="pln" style="margin: 0px; padding: 0px; border: 0px; color: #000000;">eclipse</span></code></pre> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">and it helped.</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-23289043" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/23289043">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/23289043/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2014-04-25 09:20:34Z">Apr 25 '14 at 9:20</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/83e503371c60ba6ccbeb7fc0f59bba5b?s=32&amp;d=identicon&amp;r=PG&amp;f=1" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/2750931/krzysiek-ste">krzysiek.ste</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">721</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="9 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">9</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="17 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">17</span></span> 
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
       <div id="comments-23289043" class="comments " style=""> 
        <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
         <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
          <tr id="comment-39614726" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">Only this solution worked for me, thanks!</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="847 reputation" href="http://stackoverflow.com/users/169534/yasin-okumus">Yasin Okumus</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment39614726_23289043">Aug 20 '14 at 7:14</a></span>&nbsp;
            </div> </td> 
          </tr> 
          <tr id="comment-42318563" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">Only this works for me too!&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-size: 13px; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; white-space: normal; background-color: #eeeeee;">mvn eclipse:eclipse</code>&nbsp;add project dependency to java build path, so it works. Besides, the m2eclipse plugin will add the project dependency only in "Maven Dependencies" which in Libraries tab, and the debugger cannot find.</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="91 reputation" href="http://stackoverflow.com/users/1083021/naive">naive</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment42318563_23289043">Nov 12 '14 at 7:20</a></span>&nbsp;
            </div> </td> 
          </tr> 
          <tr id="comment-50077020" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">Work for me too!</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="60 reputation" href="http://stackoverflow.com/users/287566/hlex">Hlex</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment50077020_23289043">Jun 24 at 12:13</a></span> 
            </div> </td> 
          </tr> 
         </tbody>
        </table> 
       </div> 
       <div id="comments-link-23289043" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="11452337"></a> 
  <div id="answer-11452337" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">1</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">You might have source code of a dependency accessible to Eclipse. But Eclipse does not know for source code for code that is dynamically loaded. E.g. through Maven.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">In case of Maven, I recommend that you use run-jetty-run plugin:</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;"><a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #005999;" href="http://code.google.com/p/run-jetty-run/" rel="nofollow">http://code.google.com/p/run-jetty-run/</a></p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">As a workaround you can also connect to a running JVM with the debugger and you will see the code. Alternatively you can use Dynamic Source Lookup plugin for Eclipse from here:</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;"><a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #005999;" href="https://github.com/ifedorenko/com.ifedorenko.m2e.sourcelookup" rel="nofollow">https://github.com/ifedorenko/com.ifedorenko.m2e.sourcelookup</a></p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Unfortunately it didn't helped me as it has issues with Windows paths with spaces.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">I have filled an enhancement request on Eclipse Bugzilla and if you agree this issue "Source not found" should vanish forever, please vote for it here:</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;"><a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #005999;" href="https://bugs.eclipse.org/bugs/show_bug.cgi?id=384065" rel="nofollow">https://bugs.eclipse.org/bugs/show_bug.cgi?id=384065</a></p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Thanks!</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Sasa</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-11452337" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/11452337">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/11452337/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" title="show all edits to this post" href="http://stackoverflow.com/posts/11452337/revisions">edited&nbsp;<span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2012-11-27 15:52:24Z">Nov 27 '12 at 15:52</span></a>
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;">
             &nbsp;
            </div> 
            <div class="user-details" style="">
             &nbsp;
            </div> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2012-07-12 12:56:04Z">Jul 12 '12 at 12:56</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/bcbd71c65741493ab7778a21080a90d8?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/695116/ssasa">ssasa</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">895</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="9 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">9</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="19 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">19</span></span> 
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
       <div id="comments-11452337" class="comments " style=""> 
        <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
         <tbody style="margin: 0px; padding: 0px; border: 0px;">
          <tr id="comment-16619911" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
           <td style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; line-height: 1.3; vertical-align: top;"> 
            <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
             <tbody style="margin: 0px; padding: 0px; border: 0px;">
              <tr style="margin: 0px; padding: 0px; border: 0px;"> 
               <td class=" comment-score" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;&nbsp;</td> 
               <td style="margin: 0px; padding: 0px; border: 0px; font-size: 13px;">&nbsp;</td> 
              </tr>
             </tbody>
            </table> </td> 
           <td class="comment-text" style="margin: 0px; padding: 6px 6px 6px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; font-size: 13px; vertical-align: top; line-height: 1.3;"> 
            <div class="comment-body" style="margin: 0px; padding: 0px; border: 0px;"> 
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">You now have my support on this bug!</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="3980 reputation" href="http://stackoverflow.com/users/923560/abdull">Abdull</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; color: #999999;" dir="ltr"><a class="comment-link" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/6174550/eclipse-java-debugging-source-not-found#comment16619911_11452337">Sep 11 '12 at 15:48</a></span> 
            </div> </td> 
          </tr>
         </tbody>
        </table> 
       </div> 
       <div id="comments-link-11452337" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="9118257"></a> 
  <div id="answer-9118257" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">0</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">I had the very same problem. In my case, I've disabled Window-Preferences-Java-Debug [Suspend execution on uncaught exceptions]. Then, the console showed me the correct error: my MySql user hadn't privileges to access the database.&nbsp;<a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #005999;" href="http://stackoverflow.com/questions/1960158/eclipse-debugging-source-not-found">According to this topic.</a></p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-9118257" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/9118257">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/9118257/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info user-hover" style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2012-02-02 18:59:18Z">Feb 2 '12 at 18:59</span> 
            </div> 
            <div class="user-gravatar32" style=""> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/68fa74ee335b803e26e737aa84322e4e?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/312808/alex">Alex</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">1,353</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="4 gold badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">4</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="23 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">23</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="52 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">52</span></span> 
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
       <div id="comments-link-9118257" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="14874937"></a> 
  <div id="answer-14874937" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">0</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Info: This is a possible solution, when you use maven (pom.xml) with couple of projects.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">If you are working with maven, make sure what version you are taking inside the according pom.xml (e. g. 1.0.1-SNAPSHOT ). It might be possible that your code is up-to-date, but your pom.xml dependencies are still taking the old JAR's/Snapshots (with the old code).</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Finding the problem:</p> 
        <ul style="margin-bottom: 1em; margin-left: 30px; border: 0px;"> 
         <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px;">Try to debug the according file.</li> 
         <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px;">Therefore, set a breakpoint in the relevant code area.</li> 
         <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px;">When&nbsp;<strong style="margin: 0px; padding: 0px; border: 0px;">"source not found"</strong>&nbsp;appears, make sure to bind in the right project (where the .java file can be found).</li> 
         <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px;">The compile .class file opens up in the IDE editor.</li> 
         <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px;">Click "Link with Editor" to find the according JAR/Snapshot.</li> 
         <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px;">Now make sure that this JAR is the most recent one. Possibly there is a newer one. In that case, write the most recent version number in the pom.xml.</li> 
         <li style="margin-bottom: 0px; margin-left: 0px; border: 0px;">Then do a maven update and build (e. g. "mvn clean install -U") in the right project directory.</li> 
        </ul> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-14874937" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/14874937">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/14874937/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2013-02-14 12:31:05Z">Feb 14 '13 at 12:31</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/6c90850931f6dd016119af6c24473ded?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/1854667/user1854667">user1854667</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">316</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="3 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">3</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="7 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">7</span></span> 
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
       <div id="comments-link-14874937" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="16893377"></a> 
  <div id="answer-16893377" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">0</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">If you are on eclipse or STS please install and Use GC(GrepCode Plugin) ,some time you don't need to attach the source .zip file into your project path so GrepCode works fine for you.</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-16893377" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/16893377">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/16893377/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info user-hover" style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2013-06-03 09:11:08Z">Jun 3 '13 at 9:11</span> 
            </div> 
            <div class="user-gravatar32" style=""> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://i.stack.imgur.com/I6efM.jpg?s=32&amp;g=1" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/2281472/danielad">danielad</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">2,458</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="1 gold badge"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">1</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="14 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">14</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="40 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">40</span></span> 
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
       <div id="comments-link-16893377" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="20214187"></a> 
  <div id="answer-20214187" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">0</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">I've had a related issue in connection with Glassfish server debugging in Eclipse. This was brought about by loading the source code from a different repository (changing from SVN to GitHub). In the process, the wrong compiled classes were used by the Glassfish server and hence, the source and run time would be out of sync with break points appearing on empty lines.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">To solve this, rename or delete the top folder of the classes directory and Glassfish will recreate the whole class directory tree including updating the class files with the correctly compiled version.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">The classes directory is located in: /workspace/glassfish3122eclipsedefaultdomain/eclipseApps/&lt; your Web Application&gt;/WEB-INF/classes</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-20214187" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/20214187">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/20214187/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2013-11-26 10:18:35Z">Nov 26 '13 at 10:18</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://graph.facebook.com/100001270177906/picture?type=large" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/3035873/user3035873">user3035873</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;">
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">1</span>
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
       <div id="comments-link-20214187" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="24139350"></a> 
  <div id="answer-24139350" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">0</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">In my case with tomcat projects I have checked project here: Window - Preferences - Tomcat - Source Path - Add java projects to source path</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-24139350" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/24139350">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/24139350/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2014-06-10 11:02:03Z">Jun 10 '14 at 11:02</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/45e06b1f0412fceec99bc311f8f94588?s=32&amp;d=identicon&amp;r=PG&amp;f=1" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/3132194/user3132194">user3132194</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">411</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="2 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">2</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="7 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">7</span></span> 
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
       <div id="comments-link-24139350" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="25919034"></a> 
  <div id="answer-25919034" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">0</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">In my case the Maven version of the other referenced project didn't match the version of the test project. Once they were the same, the problem disappeared.</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-25919034" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/25919034">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/25919034/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2014-09-18 17:36:33Z">Sep 18 '14 at 17:36</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/a5421e55c3b5c75f8c6acbff1e7e5a37?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/571150/maarten">maarten</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">131</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="5 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">5</span></span> 
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
       <div id="comments-link-25919034" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="28707334"></a> 
  <div id="answer-28707334" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">0</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">When running in debug mode, click Edit Source Lookup after suspended from thread. At this point, we should be able to add the necessary project/jar which contains your source code. After I added my current project in this way, and it solved my problem. Thanks</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-28707334" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/28707334">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/28707334/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2015-02-24 22:10:07Z">Feb 24 at 22:10</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/5a3ca96a9fa69c138ff4c50c8546633b?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/4603250/yoga">Yoga</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;">
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">1</span>
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
       <div id="comments-link-28707334" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="29159498"></a> 
  <div id="answer-29159498" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">0</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">If you want to attach source code to any JAR by auto-downloading, try using this Eclipse plugin&nbsp;<a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #005999;" href="http://marketplace.eclipse.org/content/java-source-attacher" rel="nofollow">Java Source Attacher</a></p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;"><img style="margin: 0px; padding: 0px; max-width: 630px;" src="http://i.stack.imgur.com/NGLiz.png" alt="enter image description here"></p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-29159498" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/29159498">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/29159498/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" title="show all edits to this post" href="http://stackoverflow.com/posts/29159498/revisions">edited&nbsp;<span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2015-03-20 05:05:21Z">Mar 20 at 5:05</span></a>
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;">
             &nbsp;
            </div> 
            <div class="user-details" style="">
             &nbsp;
            </div> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2015-03-20 04:35:06Z">Mar 20 at 4:35</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://i.stack.imgur.com/7ALzV.jpg?s=32&amp;g=1" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/248847/krishprabakar">KrishPrabakar</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">841</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="1 gold badge"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">1</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="12 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">12</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="30 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">30</span></span> 
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
       <div id="comments-link-29159498" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="29906151"></a> 
  <div id="answer-29906151" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">0</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">I had this problem while working on java code to do process on a excel file containing a data set, then convert it to .csv file, i tried answers to this post, but they did not work. the problem was the jar files themselves. after downloading needed jar files one by one(older releases) and add them to my project, "source not found" error vanished. maybe you can check your jar files. hope this would help.</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-29906151" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/29906151">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/29906151/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2015-04-27 21:21:20Z">Apr 27 at 21:21</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/e7c29ffbdf819cbf8061309438bc77d3?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/1952431/simin">simin</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">11</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="1 bronze badge"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">1</span></span> 
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
       <div id="comments-link-29906151" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="31651344"></a> 
  <div id="answer-31651344" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">0</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">this worked for me</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">right click on project -&gt; Properties -&gt; Deployment Assembly -&gt; add your jar</p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-31651344" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/31651344">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/31651344/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2015-07-27 10:59:51Z">Jul 27 at 10:59</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/992d9c87b51b2874472b99a0d8fe11a8?s=32&amp;d=identicon&amp;r=PG&amp;f=1" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/3580519/tajnosagentos">TajnosAgentos</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">49</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="7 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">7</span></span> 
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
       <div id="comments-link-31651344" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="19995823"></a> 
  <div id="answer-19995823" class="answer downvoted-answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" style="" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="">-3</span>
        <a class="vote-down-off" style="" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style=""> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">In my case problem was resolved by clicking&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-size: 13px; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; white-space: pre-wrap; background-color: #eeeeee;">Remove All Breakpoints</code></p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-19995823" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/19995823">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/19995823/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="" align="right"> 
           <div class="user-info user-hover" style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" title="show all edits to this post" href="http://stackoverflow.com/posts/19995823/revisions">edited&nbsp;<span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2013-11-15 07:54:15Z">Nov 15 '13 at 7:54</span></a>
            </div> 
            <div class="user-gravatar32" style=""> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://i.stack.imgur.com/BA7wy.jpg?s=32&amp;g=1" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/628006/ruffp">ruffp</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">2,097</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="10 gold badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">10</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="30 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">30</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="69 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">69</span></span> 
             </div> 
            </div> 
           </div> </td> 
          <td class="post-signature" style="" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2013-11-15 07:35:13Z">Nov 15 '13 at 7:35</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/bd43f1e9c9b3cddfc0ceba8d9df8ad23?s=32&amp;d=identicon&amp;r=PG&amp;f=1" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details" style=""> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/2995311/user2995311">user2995311</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;">
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">11</span>
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
       <div id="comments-link-19995823" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
  <div class="question-status" style=""> 
   <h2 style="margin-bottom: 10px; border: 0px; font-size: 15px; line-height: 18px; font-weight: 400;"> <strong style="margin: 0px; padding: 0px; border: 0px;">protected</strong>&nbsp;by&nbsp;<a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/-1/community">Community</a><span class="mod-flair" style="margin: 0px 0px 0px 3px; padding: 0px; border: 0px; color: #0077cc; font-weight: bold; line-height: 1;" title="moderator">♦</span>&nbsp;<span style="margin: 0px; padding: 0px; border: 0px;" dir="ltr"><span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2015-03-28 09:23:37Z">Mar 28 at 9:23</span></span> </h2> 
   <p style="margin-bottom: 1em; border: 0px; clear: both;">Thank you for your interest in this question. Because it has attracted low-quality or spam answers that had to be removed, posting an answer now requires 10&nbsp;<a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/help/whats-reputation">reputation</a>&nbsp;on this site.&nbsp;<br><br>Would you like to answer one of these&nbsp;<a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/unanswered?fromProtectedNotice=true">unanswered questions</a>&nbsp;instead?</p> 
  </div> 
  <h2 class="bottom-notice" style="margin-top: 15px; margin-bottom: 1em; padding-right: 10px; border: 0px; font-size: 16px; line-height: 1.4; font-weight: 400;">Not the answer you're looking for? Browse other questions tagged&nbsp;<a class="post-tag" style="" title="show questions tagged 'java'" href="http://stackoverflow.com/questions/tagged/java" rel="tag">java</a>&nbsp;<a class="post-tag" style="" title="" href="http://stackoverflow.com/questions/tagged/eclipse" rel="tag">eclipse</a>&nbsp;<a class="post-tag" style="" title="show questions tagged 'debugging'" href="http://stackoverflow.com/questions/tagged/debugging" rel="tag">debugging</a>&nbsp;or&nbsp;<a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/questions/ask">ask your own question</a>.</h2> 
 </div> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>