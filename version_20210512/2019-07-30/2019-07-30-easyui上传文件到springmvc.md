#easyui上传文件到springmvc
###发表时间：2019-07-30
###分类：javascript,经验,easyui,jQuery
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2443070" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2443070</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="html">&lt;div class="easyui-panel" title="上传文件" style="width:300%;max-width:400px;padding:30px 60px;"&gt;
            &lt;form id="uploadForm" enctype="multipart/form-data"&gt;
                &lt;div style="margin-bottom:20px"&gt;
                    &lt;input class="easyui-textbox" name="flowId" id="flowId" style="width:100%" data-options="label:'flowId:',required:true"&gt;
                &lt;/div&gt;             
                &lt;div style="margin-bottom:20px"&gt;
                    &lt;input id="file"  name="file" class="f1 easyui-filebox" style="width:100%" data-options="label:'Zip文件:',required:true"/&gt;                    
                &lt;/div&gt;
            &lt;/form&gt;
            &lt;div style="text-align:center;padding:5px 0"&gt;
                &lt;a href="javascript:void(0)" id="submitBtnId" class="easyui-linkbutton" style="width:80px"&gt;上传&lt;/a&gt;
                &lt;a href="javascript:void(0)" id="resetBtnId" class="easyui-linkbutton" style="width:80px"&gt;重置&lt;/a&gt;
            &lt;/div&gt;
        &lt;/div&gt;</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="js">$('#submitBtnId').click(function(){
    var formData = new FormData($('#uploadForm')[0]);
    
    var options = {
            url:  '/zip/upload',
            type : 'POST',
            dataType : 'json',
            data : formData,
            // 告诉jQuery不要去处理发送的数据
            processData : false,
            // 告诉jQuery不要去设置Content-Type请求头
            contentType : false,
            beforeSend : function() {
                $.messager.progress({
                    title : '请稍后，正在导入数据',
                    msg : '数据导入中...'
                });
            },
            complete : function(rs) {
                $.messager.progress('close');
            },
            success : function(rs) {
                if (rs &amp;&amp; rs.status == 0) {
                    showTipMessage(
                            'success',
                            function() {
                                
                            });
                } else {
                    showWarningMessage('失败！'
                            + rs.errorMessage);
                }
            },
            error : function(rs) {
                showWarningMessage('失败！'
                        + rs);
            }
        };
        $.ajax(options);
});</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@RestController
@RequestMapping(value = { "/zip" })
public class GumpZipController {
    private static final Logger LOGGER = LoggerFactory.getLogger(GumpZipController.class);

    @RequestMapping(value = { "/upload" }, method = { RequestMethod.POST })
    public Result&lt;String&gt; upload(HttpServletRequest req, @RequestParam Integer flowId,
            @RequestParam(value = "file") MultipartFile uploadFile) {
        LOGGER.debug("start to upload. flowId:{},uploadFile:{}", flowId, uploadFile);
        return Result.success("hello");
    }
}        </pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>