#Spring RestTemplate文件上传(Uploading MultipartFile with Spring RestTemplate)
###发表时间：2019-04-01
###分类：Spring,RestTemplate,文件处理,REST
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2439615" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2439615</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>文章《Uploading MultipartFile with Spring RestTemplate》</p> 
 <p>地址：<a href="https://www.baeldung.com/spring-rest-template-multipart-upload">https://www.baeldung.com/spring-rest-template-multipart-upload</a></p> 
 <p>代码：<a href="https://github.com/eugenp/tutorials/tree/master/spring-rest/src/main/java/com/baeldung/web/upload">https://github.com/eugenp/tutorials/tree/master/spring-rest/src/main/java/com/baeldung/web/upload</a></p> 
 <p>client：</p> 
 <pre name="code" class="java">mport org.springframework.core.io.FileSystemResource;
import org.springframework.core.io.Resource;
import org.springframework.http.HttpEntity;
import org.springframework.http.HttpHeaders;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.util.LinkedMultiValueMap;
import org.springframework.util.MultiValueMap;
import org.springframework.web.client.RestTemplate;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;

public class MultipartFileUploadClient {

    public static void main(String[] args) throws IOException {
        uploadSingleFile();
        uploadMultipleFile();
    }

    private static void uploadSingleFile() throws IOException {
        HttpHeaders headers = new HttpHeaders();
        headers.setContentType(MediaType.MULTIPART_FORM_DATA);

        MultiValueMap&lt;String, Object&gt; body = new LinkedMultiValueMap&lt;&gt;();
        body.add("file", getTestFile());


        HttpEntity&lt;MultiValueMap&lt;String, Object&gt;&gt; requestEntity = new HttpEntity&lt;&gt;(body, headers);
        String serverUrl = "http://localhost:8082/spring-rest/fileserver/singlefileupload/";
        RestTemplate restTemplate = new RestTemplate();
        ResponseEntity&lt;String&gt; response = restTemplate.postForEntity(serverUrl, requestEntity, String.class);
        System.out.println("Response code: " + response.getStatusCode());
    }

    private static void uploadMultipleFile() throws IOException {
        HttpHeaders headers = new HttpHeaders();
        headers.setContentType(MediaType.MULTIPART_FORM_DATA);

        MultiValueMap&lt;String, Object&gt; body = new LinkedMultiValueMap&lt;&gt;();
        body.add("files", getTestFile());
        body.add("files", getTestFile());
        body.add("files", getTestFile());

        HttpEntity&lt;MultiValueMap&lt;String, Object&gt;&gt; requestEntity = new HttpEntity&lt;&gt;(body, headers);
        String serverUrl = "http://localhost:8082/spring-rest/fileserver/multiplefileupload/";
        RestTemplate restTemplate = new RestTemplate();
        ResponseEntity&lt;String&gt; response = restTemplate.postForEntity(serverUrl, requestEntity, String.class);
        System.out.println("Response code: " + response.getStatusCode());
    }

    public static Resource getTestFile() throws IOException {
        Path testFile = Files.createTempFile("test-file", ".txt");
        System.out.println("Creating and Uploading Test File: " + testFile);
        Files.write(testFile, "Hello World !!, This is a test file.".getBytes());
        return new FileSystemResource(testFile.toFile());
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>server：</p> 
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
</div>