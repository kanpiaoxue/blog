#SpringMVC上传文件、下载文件
###发表时间：2018-02-02
###分类：java,Spring,文件处理
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2410061" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2410061</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <pre name="code" class="上传文件的easyui的HTML">&lt;form id="uploadForm" enctype="multipart/form-data"&gt;
    &lt;span style="margin-right: 65px;"&gt;词典名称:&lt;/span&gt;
    &lt;select class="easyui-combobox" style="width: 180px;" id="batchAddPanelDictConditionSelect" name="dictId"&gt;
    &lt;/select&gt;    
    &lt;div style="margin-bottom: 20px"&gt;
        &lt;input class="easyui-filebox" label="Excel文件:" name="excelFile" id="excelFileId" labelPosition="left"
            data-options="prompt:'Choose a excel file...'" style="width: 100%"&gt;
    &lt;/div&gt;
&lt;/form&gt;</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="js">function commit() {

    var dictId = $('#batchAddPanelDictConditionSelect').combobox('getValue');
    if (dictId == '') {
        showWarningMessage('请选择词典！');
        return;
    }
    var excelFile = $('#excelFileId').textbox('getValue');
    if (excelFile == '') {
        showWarningMessage('请选择需要上传的excel！');
        return;
    }
    var regex = /^.+?(\.xlsx)|(\.xls)$/;
    if (!regex.test(excelFile)) {
        showWarningMessage('上传的文件必须是excel！');
        return;
    }

    var formData = new FormData($('#uploadForm')[0]);

    var options = {
        url: 'entry/batchAddEntries',
        type: 'POST',
        dataType: 'json',
        data: formData,
        // 告诉jQuery不要去处理发送的数据
        processData: false,
        // 告诉jQuery不要去设置Content-Type请求头
        contentType: false,
        beforeSend: function () {
            console.log("正在进行，请稍候");
        },
        success: function (rs) {
        },
        error: function (rs) {
        }
    };
    $.ajax(options);
};</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@RestController
@RequestMapping(value = { "/entry" })
public class EntryController  {
    private static final Logger LOGGER = LoggerFactory.getLogger(EntryController.class);
    /**
     * excel文件后缀形式1
     */
    private static final String EXCEL_SUFFIX_01 = ".xls";
    /**
     * excel文件后缀形式2
     */
    private static final String EXCEL_SUFFIX_02 = ".xlsx";

    @RequestMapping(value = { "/batchAddEntries" }, method = { RequestMethod.POST })
        public Result&lt;Void&gt; batchAddEntries(@RequestParam("dictId") Integer dictId,
                @RequestParam("excelFile") MultipartFile excelFile) {
            LOGGER.debug("start to batchAddEntries. dictId:{},excelFile:{}", dictId, excelFile);
            checkNotNull(dictId, "dictId is null");
            checkNotNull(excelFile, "excelFile is null");
            String lowcaseName = excelFile.getName().toLowerCase();
            checkArgument(lowcaseName.endsWith(EXCEL_SUFFIX_01) || lowcaseName.endsWith(EXCEL_SUFFIX_02),
                    "upload file is not a excel file");

            // TODO upload excel
            return null;
        }


    @RequestMapping(value = { "/download" }, method = { RequestMethod.GET })
    public ResponseEntity&lt;byte[]&gt; download(HttpServletRequest request,
            @RequestParam("fileName") String fileName) throws Exception {
        // 下载文件路径
        String path = request.getServletContext().getRealPath("/static/template/");
        File file = new File(path + File.separator + fileName);
        HttpHeaders headers = new HttpHeaders();
        // 通知浏览器以attachment（下载方式）打开图片
        headers.setContentDispositionFormData("attachment", fileName);
        // application/octet-stream ： 二进制流数据（最常见的文件下载）。
        headers.setContentType(MediaType.APPLICATION_OCTET_STREAM);
        return new ResponseEntity&lt;byte[]&gt;(FileUtils.readFileToByteArray(file), headers, HttpStatus.CREATED);
    }
    
}</pre> 
 <p>&nbsp;&nbsp;</p> 
 <p>&nbsp;参考地址：<a href="http://blog.csdn.net/qian_ch/article/details/69258465">&nbsp;http://blog.csdn.net/qian_ch/article/details/69258465</a></p> 
 <p>&nbsp;</p> 
 <p>参考代码：单文件上传、多文件上传</p> 
 <p><a href="https://github.com/eugenp/tutorials/blob/master/spring-rest/src/main/java/com/baeldung/web/upload/controller/FileServerResource.java">https://github.com/eugenp/tutorials/blob/master/spring-rest/src/main/java/com/baeldung/web/upload/controller/FileServerResource.java</a></p> 
 <pre name="code" class="java">import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.multipart.MultipartFile;

import java.io.IOException;
import java.util.List;

@RestController
@RequestMapping("/fileserver")
public class FileServerResource {

    @RequestMapping(path = "/singlefileupload/", method = RequestMethod.POST)
    public ResponseEntity&lt;String&gt; processFile(@RequestParam("file") MultipartFile file) throws IOException {

        byte[] bytes = file.getBytes();

        System.out.println("File Name: " + file.getOriginalFilename());
        System.out.println("File Content Type: " + file.getContentType());
        System.out.println("File Content:\n" + new String(bytes));

        return (new ResponseEntity&lt;&gt;("Successful", null, HttpStatus.OK));
    }

    @RequestMapping(path = "/multiplefileupload/", method = RequestMethod.POST)
    public ResponseEntity&lt;String&gt; processFile(@RequestParam("files") List&lt;MultipartFile&gt; files) throws IOException {

        for (MultipartFile file : files) {
            byte[] bytes = file.getBytes();

            System.out.println("File Name: " + file.getOriginalFilename());
            System.out.println("File Content Type: " + file.getContentType());
            System.out.println("File Content:\n" + new String(bytes));
        }

        return (new ResponseEntity&lt;&gt;("Successful", null, HttpStatus.OK));
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>