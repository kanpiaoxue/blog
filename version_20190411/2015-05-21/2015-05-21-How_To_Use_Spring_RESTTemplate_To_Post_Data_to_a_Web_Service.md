#How To Use Spring RESTTemplate To Post Data to a Web Service
###发表时间：2015-05-21
###分类：Spring,java,REST,RestTemplate
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2213266" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2213266</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>使用spring的restelplate的post方法，向web程序发起请求，参数用各种变量，包括@RequestBody。</p> 
 <pre name="code" class="java">@Controller
@RequestMapping("/task")
public class TaskWithTokenController extends BaseController {

    @Autowired
    private DataVersionService dataVersionService;
    @Autowired
    private TaskService taskService;
    @Autowired
    private SysService sysService;

    @RequestMapping(value = "/{token}/{userId}/update",
            method = RequestMethod.POST)
    public void update(HttpServletResponse response,
            @RequestBody Task task,
            @PathVariable("token") String token,
            @PathVariable("userId") String userId) {
        LOGGER.debug("update");

        try {
            long taskSysId = checkTokenForTask(task.getTaskId(), token);
            task.setSysId(taskSysId);
            taskService.updateTaskAndAddLog(task, userId);
            processSuccessForResponse(response);
        } catch (Exception e) {
            LOGGER.error(e.getMessage(), e);
            processErrorForResponse(response, e.getMessage());
        }
    }

    private long checkTokenForTask(long taskId, String token) throws Exception {
        Task t = taskService.query(taskId);
        Preconditions.checkNotNull(t, "不存在任务ID是：[%s] 的任务！ ");
        long taskSysId = t.getSysId().longValue();
        List&lt;Sys&gt; syses = sysService.queryAllOnlineSyss();
        String taskToken = null;
        for (Sys sys : syses) {
            if (taskSysId == sys.getSysId().longValue()) {
                taskToken = sys.getToken();
                break;
            }
        }
        String err = String.format("%s 是一个无效的token.", token);
        Preconditions.checkArgument(StringUtils.isNotBlank(taskToken), err);
        Preconditions.checkArgument(token.equals(taskToken), err);
        return taskSysId;

    }

}</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@RequestMapping(value = "/updateTask", method = { RequestMethod.POST })
    @ResponseBody
    public AjaxResult updateTask(@RequestBody Task task,
            @CookieValue(Consts.COOKIE_USER_KEY) String userId) {
        LOGGER.info("user {} start update task {}", userId, task);
        // 检验字段格式
        if ((task.getTaskId() == null) || (task.getTaskId() == -1)) {
            return AjaxResult.errorMessage("taskId is wrong!");
        }

        String url =                 "http://localhost:8080/dmap-apiserver/api/task/{token}/{userId}/update";
        
        try {
            defaultTaskValue(task);
            Map&lt;String, String&gt; uriVariables = Maps.newHashMap();
            uriVariables.put("token", token);
            uriVariables.put("userId", userId);
            ResponseEntity&lt;String&gt; rs = restTemplate.postForEntity(url, task, String.class, uriVariables);
            
            
            String body = rs.getBody();
            AjaxResult ars = JSON.parseObject(body, AjaxResult.class);
            return ars;
        } catch (Exception e) {
            LOGGER.error(e.getMessage(), e);
            return AjaxResult.errorMessage(e.getMessage());
        }

    }</pre> 
 <p>&nbsp;</p> 
 <p>参考：<a href="http://johnathanmarksmith.com/spring/java/javaconfig/programming/spring%20java%20configuration/spring%20mvc/web/rest/resttemplate/2013/06/18/how-to-use-spring-resttemplate-to-post-data-to-a-web-service/">&nbsp;http://johnathanmarksmith.com/spring/java/javaconfig/programming/spring%20java%20configuration/spring%20mvc/web/rest/resttemplate/2013/06/18/how-to-use-spring-resttemplate-to-post-data-to-a-web-service/</a></p> 
</div>