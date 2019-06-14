#SimpleJdbcInsert异常：InvalidDataAccessApiUsageException: Configuration can't
###发表时间：2015-12-18
###分类：java,Spring
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2265018" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2265018</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>今天使用&nbsp;org.springframework.jdbc.core.simple.SimpleJdbcInsert来进行一些操作，代码如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@Repository("auditLogDao")
public class AuditLogDaoImpl implements AuditLogDao {
    private static final Logger LOGGER = LoggerFactory.getLogger(AuditLogDaoImpl.class);
    @Autowired
    private SimpleJdbcInsert simpleJdbcInsert;

    /*
     * (non-Javadoc)
     */
    @Override
    public void add(EntityOperationAuditLog entityOperationAuditLog) {
        Preconditions.checkNotNull(entityOperationAuditLog);
        if (null == entityOperationAuditLog.getGmtCreate()) {
            entityOperationAuditLog.setGmtCreate(new Date());
        }
        LOGGER.debug("start insert tb_operation_audit_log {} ", entityOperationAuditLog);

        // 表名
        simpleJdbcInsert.withTableName("tb_operation_audit_log");
        SqlParameterSource parameters = new BeanPropertySqlParameterSource(entityOperationAuditLog);
        // 插入db并返回自增主键id
        simpleJdbcInsert.execute(parameters);
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>该代码执行第一次的时候是很好的，可是执行第二次的时候就报错了，如下：</p> 
 <pre name="code" class="java">org.springframework.dao.InvalidDataAccessApiUsageException: Configuration can't be altered once the class has been compiled or used</pre> 
 <p>&nbsp;然后去查了查，发现这个<span style="line-height: 1.5;">SimpleJdbcInsert只能指定一次tableName，不能为同一个</span><span style="line-height: 1.5;">SimpleJdbcInsert的实例多次设置tableName。所以才引起上面的异常信息。</span></p> 
 <p><span style="line-height: 1.5;">改为如下的代码就解决了问题：</span></p> 
 <pre name="code" class="java">@Repository("auditLogDao")
public class AuditLogDaoImpl implements AuditLogDao {
    private static final Logger LOGGER = LoggerFactory.getLogger(AuditLogDaoImpl.class);
    
    private SimpleJdbcInsert simpleJdbcInsert;
    
    
    public AuditLogDaoImpl() {
        super();
    }

    @Autowired
    public AuditLogDaoImpl(SimpleJdbcInsert simpleJdbcInsert) {
        super();
        this.simpleJdbcInsert = simpleJdbcInsert;
        simpleJdbcInsert.withTableName("tb_operation_audit_log");
    }

    /*
     * (non-Javadoc)
     * @see 
     * EntityOperationAuditLog)
     */
    @Override
    public void add(EntityOperationAuditLog entityOperationAuditLog) {
        Preconditions.checkNotNull(entityOperationAuditLog);
        if (null == entityOperationAuditLog.getGmtCreate()) {
            entityOperationAuditLog.setGmtCreate(new Date());
        }
        LOGGER.debug("start insert tb_operation_audit_log {} ", entityOperationAuditLog);

        // 表名
        // simpleJdbcInsert.withTableName("tb_operation_audit_log");
        SqlParameterSource parameters = new BeanPropertySqlParameterSource(entityOperationAuditLog);
        // 插入db并返回自增主键id
        simpleJdbcInsert.execute(parameters);
    }
}</pre> 
 <p><span style="line-height: 1.5;">&nbsp;</span></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p><span style="line-height: 1.5;">参考：&nbsp;</span>http://stackoverflow.com/questions/15606588/org-springframework-dao-invaliddataaccessapiusageexception-configuration-cant</p> 
 <p>&nbsp;</p> 
 <div id="question" class="question" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; clear: both; color: #222426; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; line-height: 16.9px;"> 
  <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
   <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
    <tr style="margin: 0px; padding: 0px; border: 0px;"> 
     <td class="postcell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
      <div style="margin: 0px; padding: 0px; border: 0px;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Iam inserting some data into DB with simpleJdbcInsert in spring , it works fine for first step (i mean for first insertion ) , when i try yo save the data for second time iam getting exception as :org.springframework.dao.InvalidDataAccessApiUsageException: Configuration can't be altered once the class has been compiled or used."</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">Can any one help me out in this.</p> 
       </div> 
       <div class="post-taglist" style="margin: 0px 0px 10px; padding: 0px; border: 0px; clear: both;">
        <a class="post-tag" style="margin: 2px 2px 2px 0px; padding: 0.4em 0.5em; border: 1px solid #e1ecf4; font-size: 12px; cursor: pointer; color: #39739d; border-radius: 0px; text-align: center; line-height: 1; white-space: nowrap; display: inline-block; background: #e1ecf4;" title="show questions tagged 'spring-mvc'" href="http://stackoverflow.com/questions/tagged/spring-mvc" rel="tag">spring-mvc</a>
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-15606588" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this question" href="http://stackoverflow.com/q/15606588">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/15606588/edit">improve this question</a> 
           </div> </td> 
          <td class="post-signature owner" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px; background-color: #e0eaf1;"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             asked&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2013-03-25 02:10:18Z">Mar 25 '13 at 2:10</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/3d0984bf264589142d40c2facfcc38a5?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details"> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/883770/renukeswar">Renukeswar</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">105</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="1 silver badge"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">1</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="8 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">8</span></span> 
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
      <div id="comments-link-15606588" style="margin: 0px; padding: 0px; border: 0px;">
       <a class="js-add-link comments-link disabled-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.">add a comment</a>
      </div> </td> 
    </tr> 
   </tbody>
  </table> 
 </div> 
 <div id="answers" style="margin: 0px; padding: 10px 0px 0px; border: 0px; font-size: 13px; clear: both; width: 728px; color: #222426; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; line-height: 16.9px;"> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="tab-top"></a> 
  <div id="answers-header" style="margin: 10px 0px 0px; padding: 0px; border: 0px; width: 728px;"> 
   <div class="subheader answers-subheader" style="margin: 0px 0px 15px; padding: 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #eaebec; clear: both; height: 34px;"> 
    <h2 style="margin-bottom: 0px; border: 0px; font-size: 18px; line-height: 1.3; color: #444444; float: left; font-weight: 400;">1 Answer</h2> 
    <div style="margin: 0px; padding: 0px; border: 0px;"> 
     <div id="tabs" style="margin: 0px; padding: 0px; border: 0px; float: right; height: 38px;"> 
      <a style="margin: 0px 8px 0px 0px; padding: 10px; border-width: 2px 1px 1px; border-style: solid; border-color: transparent transparent #eaebec; font-size: 12px; cursor: pointer; color: #767d84; float: left; display: block; line-height: 1;" title="Answers with the latest activity first" href="http://stackoverflow.com/questions/15606588/org-springframework-dao-invaliddataaccessapiusageexception-configuration-cant?answertab=active#tab-top">active</a>
      <a style="margin: 0px 8px 0px 0px; padding: 10px; border-width: 2px 1px 1px; border-style: solid; border-color: transparent transparent #eaebec; font-size: 12px; cursor: pointer; color: #767d84; float: left; display: block; line-height: 1;" title="Answers in the order they were provided" href="http://stackoverflow.com/questions/15606588/org-springframework-dao-invaliddataaccessapiusageexception-configuration-cant?answertab=oldest#tab-top">oldest</a>
      <a class="youarehere" style="margin: 0px; padding: 10px; border-width: 2px 1px 1px; border-style: solid; border-color: #f69c55 #eaebec #ffffff; font-size: 12px; cursor: pointer; color: #222426; float: left; display: block; line-height: 1;" title="Answers with the highest score first" href="http://stackoverflow.com/questions/15606588/org-springframework-dao-invaliddataaccessapiusageexception-configuration-cant?answertab=votes#tab-top">votes</a> 
     </div> 
    </div> 
   </div> 
  </div> 
  <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" name="15606749"></a> 
  <div id="answer-15606749" class="answer" style="margin: 0px; padding: 20px 0px; border-width: 0px 0px 1px; border-bottom-style: solid; border-bottom-color: #f0f0f0; width: 728px;"> 
   <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px;">
    <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
     <tr style="margin: 0px; padding: 0px; border: 0px;"> 
      <td class="votecell" style="margin: 0px; padding: 0px 15px 0px 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="vote" style="margin: 0px; padding: 0px; border: 0px; text-align: center; min-width: 46px;"> 
        <a class="vote-up-off" title="This answer is useful">up vote</a>
        <span class="vote-count-post " style="margin: 8px 0px; padding: 0px; border: 0px; font-size: 20px; display: block; color: #777777;">1</span>
        <a class="vote-down-off" title="This answer is not useful">down vote</a> 
       </div> </td> 
      <td class="answercell" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
       <div class="post-text" style="margin: 0px 0px 5px; padding: 0px; border: 0px; font-size: 15px; width: 660px; line-height: 1.3;"> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">This exception usually happens when you try to config(again) a&nbsp;<strong style="margin: 0px; padding: 0px; border: 0px;">compiled</strong>&nbsp;simpleJdbcInsert.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;"><strong style="margin: 0px; padding: 0px; border: 0px;">compiled</strong>&nbsp;means you have instantiated a simpleJdbcInsert instance and set up&nbsp;<strong style="margin: 0px; padding: 0px; border: 0px;">data source</strong>&nbsp;and<strong style="margin: 0px; padding: 0px; border: 0px;">table name</strong>&nbsp;already. Once an simpleJdbcInsert instance is&nbsp;<strong style="margin: 0px; padding: 0px; border: 0px;">compiled</strong>, you should not re-config it again; for instance, set another table name. Create a new simpleJdbcInsert instace if you need to do so.</p> 
        <p style="margin-bottom: 1em; border: 0px; clear: both;">To get a comprehensive understanding about how&nbsp;<strong style="margin: 0px; padding: 0px; border: 0px;">simpleJdbcInsert</strong>&nbsp;works, take a look into source code of&nbsp;<strong style="margin: 0px; padding: 0px; border: 0px;">simpleJdbcInsert</strong>&nbsp;and&nbsp;<strong style="margin: 0px; padding: 0px; border: 0px;">AbstractJdbcInsert</strong>. especially the method&nbsp;<strong style="margin: 0px; padding: 0px; border: 0px;">compile()</strong>&nbsp;in<strong style="margin: 0px; padding: 0px; border: 0px;">AbstractJdbcInsert.java</strong></p> 
       </div> 
       <table class="fw" style="margin: 0px 0px 4px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
        <tbody style="margin: 0px; padding: 0px; border: 0px;">
         <tr style="margin: 0px; padding: 0px; border: 0px;"> 
          <td class="vt" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top;"> 
           <div class="post-menu" style="margin: 0px; padding: 2px 0px 0px; border: 0px;"> 
            <a id="link-post-15606749" class="short-link" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="short permalink to this answer" href="http://stackoverflow.com/a/15606749">share</a>
            <a class="suggest-edit-post" style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #888888;" title="" href="http://stackoverflow.com/posts/15606749/edit">improve this answer</a> 
           </div> </td> 
          <td class="post-signature" style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: top; width: 200px;" align="right"> 
           <div class="user-info " style="margin: 0px; padding: 5px 6px 7px 7px; border: 0px; width: 200px; color: #52575c;"> 
            <div class="user-action-time" style="margin: 1px 0px 4px; padding: 0px; border: 0px; font-size: 12px; white-space: nowrap;">
             answered&nbsp;
             <span class="relativetime" style="margin: 0px; padding: 0px; border: 0px;" title="2013-03-25 02:33:41Z">Mar 25 '13 at 2:33</span> 
            </div> 
            <div class="user-gravatar32" style="margin: 0px; padding: 0px; border: 0px; float: left; width: 32px; height: 32px; border-radius: 1px;"> 
             <div class="gravatar-wrapper-32" style="margin: 0px; padding: 0px; border: 0px; width: 32px; height: 32px; overflow: hidden;">
              <img style="margin: 0px auto; padding: 0px; height: 32px; border-radius: 1px;" src="https://www.gravatar.com/avatar/5d1510d03726199da3896520ee8501c2?s=32&amp;d=identicon&amp;r=PG" alt="" width="32" height="32">
             </div> 
            </div> 
            <div class="user-details"> 
             <a style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc;" href="http://stackoverflow.com/users/2021142/spiritwalker">spiritwalker</a> 
             <div class="-flair" style="margin: 0px; padding: 0px; border: 0px;"> 
              <span class="reputation-score" style="margin: 0px 2px 0px 0px; padding: 0px; border: 0px; font-size: 12px; font-weight: bold;" title="reputation score " dir="ltr">1,535</span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="5 silver badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">5</span></span>
              <span style="margin: 0px 3px 0px 2px; padding: 0px; border: 0px;" title="9 bronze badges"><span class="badgecount" style="margin: 0px; padding: 0px; border: 0px; font-size: 12px; color: #848a91;">9</span></span> 
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
       <div id="comments-15606749" class="comments "> 
        <table style="margin: 0px; padding: 0px; border: 0px; border-collapse: collapse; border-spacing: 0px; width: 660px;">
         <tbody style="margin: 0px; padding: 0px; border: 0px;"> 
          <tr id="comment-22319402" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
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
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">Hi cannot i insert more records being on the same page, on first insertion data is getting inserted , but after navigating and again coming to insertion page , this kind of error iam getting. could u please tell is thier any configureation required to insert more records</span>&nbsp;–&nbsp;
             <a class="comment-user owner" style="margin: 0px; padding: 1px 5px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap; background-color: #e0eaf1;" title="105 reputation" href="http://stackoverflow.com/users/883770/renukeswar">Renukeswar</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #999999;" dir="ltr"><span class="relativetime-clean" style="margin: 0px; padding: 0px; border: 0px;" title="2013-03-30 02:33:57Z">Mar 30 '13 at 2:33</span></span> 
            </div> </td> 
          </tr> 
          <tr id="comment-22319673" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
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
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">are you inserting the the data into same table after page page navigation? Please attache your code to let people reproduce the issue and figure out where goes wrong.</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="1535 reputation" href="http://stackoverflow.com/users/2021142/spiritwalker">spiritwalker</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #999999;" dir="ltr"><span class="relativetime-clean" style="margin: 0px; padding: 0px; border: 0px;" title="2013-03-30 02:57:50Z">Mar 30 '13 at 2:57</span></span> 
            </div> </td> 
          </tr> 
          <tr id="comment-22320807" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
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
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">@Resource(name="dataSource") public void setSimpleJdbcTemplate(DataSource dataSource) { this.simpleJdbcTemplate = new SimpleJdbcTemplate(dataSource); and other paramertes set into Map, simpleJdbcInsert.execute(parameterMap). this.simpleJdbcInsert = new SimpleJdbcInsert(dataSource); } code to insert into DB: this.simpleJdbcInsert.withTableName("MOVIE_INFO"); Map&lt;String,Object&gt; parameterMap = new HashMap&lt;String,Object&gt;(); parameterMap.put("MOVIE_NAME", movie.getMovieName());</span>&nbsp;–&nbsp;
             <a class="comment-user owner" style="margin: 0px; padding: 1px 5px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap; background-color: #e0eaf1;" title="105 reputation" href="http://stackoverflow.com/users/883770/renukeswar">Renukeswar</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #999999;" dir="ltr"><span class="relativetime-clean" style="margin: 0px; padding: 0px; border: 0px;" title="2013-03-30 04:53:08Z">Mar 30 '13 at 4:53</span></span>&nbsp;
            </div> </td> 
          </tr> 
          <tr id="comment-22324834" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
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
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">did any one come across this kind of issue. I saw AbstractJdbcInsert ,in which isCompile method checks for this is compile variable is set true this exception is thrown</span>&nbsp;–&nbsp;
             <a class="comment-user owner" style="margin: 0px; padding: 1px 5px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap; background-color: #e0eaf1;" title="105 reputation" href="http://stackoverflow.com/users/883770/renukeswar">Renukeswar</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #999999;" dir="ltr"><span class="relativetime-clean" style="margin: 0px; padding: 0px; border: 0px;" title="2013-03-30 10:33:43Z">Mar 30 '13 at 10:33</span></span> 
            </div> </td> 
          </tr> 
          <tr id="comment-22326038" class="comment " style="margin: 0px; padding: 0px; border: 0px;"> 
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
             <span class="comment-copy" style="margin: 0px; padding: 0px; border: 0px;">remove ** this.simpleJdbcInsert.withTableName("MOVIE_INFO");**. withTableName does nothing rather than just setting table name. And please refer to my answer, you cannot set table name multiple times to same SimpleJdbcInsert instance.</span>&nbsp;–&nbsp;
             <a class="comment-user" style="margin: 0px; padding: 0px; border: 0px; cursor: pointer; color: #0077cc; white-space: nowrap;" title="1535 reputation" href="http://stackoverflow.com/users/2021142/spiritwalker">spiritwalker</a>&nbsp;
             <span class="comment-date" style="margin: 0px; padding: 0px; border-top-width: 0px; border-right-width: 0px; border-left-width: 0px; border-bottom-style: none; border-color: initial; color: #999999;" dir="ltr"><span class="relativetime-clean" style="margin: 0px; padding: 0px; border: 0px;" title="2013-03-30 11:47:32Z">Mar 30 '13 at 11:47</span></span>&nbsp;
            </div> </td> 
          </tr> 
         </tbody>
        </table> 
       </div> 
       <div id="comments-link-15606749" style="margin: 0px; padding: 0px; border: 0px;">
        <a class="js-show-link comments-link " style="margin: 0px; padding: 0px 3px 2px; border: 0px; cursor: pointer; color: #0077cc;" title="expand to show all comments on this post" href="http://stackoverflow.com/questions/15606588/org-springframework-dao-invaliddataaccessapiusageexception-configuration-cant">show&nbsp;<strong style="margin: 0px; padding: 0px; border: 0px;">4</strong>&nbsp;more comments</a>
       </div> </td> 
     </tr> 
    </tbody>
   </table> 
  </div> 
 </div> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>