#Spring REST Service Exception Handling
###发表时间：2019-04-02
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2439662" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2439662</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">spring提供Controller Advice (@ControllerAdvice)来统一处理各个Controller的异常信息。</p> 
 <p style="font-size: 14px;">示例代码如下：</p> 
 <pre name="code" class="java">import lombok.extern.slf4j.Slf4j;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import static org.springframework.http.HttpStatus.INTERNAL_SERVER_ERROR;
import static org.springframework.http.HttpStatus.NOT_FOUND;
@ControllerAdvice
@Slf4j
public class DogsServiceErrorAdvice {
    @ExceptionHandler({RuntimeException.class})
    public ResponseEntity&lt;String&gt; handleRunTimeException(RuntimeException e) {
        return error(INTERNAL_SERVER_ERROR, e);
    }
    @ExceptionHandler({DogsNotFoundException.class})
    public ResponseEntity&lt;String&gt; handleNotFoundException(DogsNotFoundException e) {
        return error(NOT_FOUND, e);
    }
    @ExceptionHandler({DogsServiceException.class})
    public ResponseEntity&lt;String&gt; handleDogsServiceException(DogsServiceException e){
        return error(INTERNAL_SERVER_ERROR, e);
    }
    private ResponseEntity&lt;String&gt; error(HttpStatus status, Exception e) {
        log.error("Exception : ", e);
        return ResponseEntity.status(status).body(e.getMessage());
    }
}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">参考资料地址：&nbsp;<a href="https://dzone.com/articles/spring-rest-service-exception-handling-1?fromrel=true">https://dzone.com/articles/spring-rest-service-exception-handling-1?fromrel=true</a></p> 
 <p style="font-size: 14px;">参考资料的具体内容：</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">This tutorial talks about Spring Rest Service Exception Handling. In our previous article, we created our very first&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.amitph.com/spring-boot-rest-service/" rel="nofollow">Spring Boot REST Web Service</a>. In this tutorial, let’s concentrate on how to handle an exception in Spring applications. While there always is an option to handle them manually and set a particular&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">ResponseStatus</code>, however, Spring provides an abstraction over the entire exception handling and just asks you to put a few annotations — it takes care of everything else. In this article, we will demonstrate these concepts with code examples.</p> 
 <h2>How to Manually Handle Exceptions</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">In the&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.amitph.com/spring-boot-rest-service/" rel="nofollow">Spring Boot Rest Service</a>&nbsp;tutorials, we had created a Dogs Service to understand the concepts. In this post, let's extend the same Dogs Service to handle exceptions.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">DogsController</code>&nbsp;returns a&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">ResponseEntity</code>&nbsp;instance, which has a response body along with &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">HttpStatus</code>.</p> 
 <ul style="margin-bottom: 10px; color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <li style="padding-bottom: 8px;">If no exception is thrown, the following endpoint returns &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">List&lt;Dog&gt;</code><span style="font-style: italic;">&nbsp;</span>&nbsp;as response body and 200 as status.</li> 
  <li style="padding-bottom: 8px;">For &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">DogsNotFoundException</code>, it returns empty body and status 404.</li> 
  <li style="padding-bottom: 8px;">For&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">DogsServiceException</code>, it returns 500 and empty body.</li> 
 </ul> 
 <span style="color: #222635; font-family: Cambria, serif;"><span style="color: #222635; font-family: Cambria, serif;"><span style="font-size: 19px;"></span></span></span> 
 <pre name="code" class="java">package com.amitph.spring.dogs.web;
import com.amitph.spring.dogs.model.DogDto;
import com.amitph.spring.dogs.repo.Dog;
import com.amitph.spring.dogs.service.DogsService;
import lombok.RequiredArgsConstructor;
import lombok.Setter;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import java.util.List;
@RestController
@RequestMapping("/dogs")
@RequiredArgsConstructor
@Setter
public class DogsController {
    @Autowired private final DogsService service;
    @GetMapping
    public ResponseEntity&lt;List&lt;Dog&gt;&gt; getDogs() {
        List&lt;Dog&gt; dogs;
        try {
            dogs = service.getDogs();
        } catch (DogsServiceException ex) {
            return new ResponseEntity&lt;&gt;(null, null, HttpStatus.INTERNAL_SERVER_ERROR);
        } catch (DogsNotFoundException ex) {
            return new ResponseEntity&lt;&gt;(null, null, HttpStatus.NOT_FOUND);
        }
        return new ResponseEntity&lt;&gt;(dogs, HttpStatus.OK);
    }
}</pre> 
 <span style="color: #222635; font-family: Cambria, serif;"><span style="font-size: 19px;">&nbsp;<br></span></span> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The problem with this approach is&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">Duplication</code>. The catch blocks are generic and will be needed in other endpoints as well (e.g. DELETE, POST, etc).</p> 
 <h2>Controller Advice (<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@ControllerAdvice</code>)</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Spring provides a better way of handling exceptions, which is Controller Advice. This is a centralized place to handle all the application level exceptions.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Our Dogs Controller now looks clean and is free for any sort of handling exceptions.</p> 
 <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Handle and Set Response Status</h3> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Below is our&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@ControllerAdvice</code>&nbsp;class where we are handling all the exceptions.</p> 
 <pre name="code" class="java">package com.amitph.spring.dogs.web;
import lombok.extern.slf4j.Slf4j;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import static org.springframework.http.HttpStatus.INTERNAL_SERVER_ERROR;
import static org.springframework.http.HttpStatus.NOT_FOUND;
@ControllerAdvice
@Slf4j
public class DogsServiceErrorAdvice {
    @ExceptionHandler({RuntimeException.class})
    public ResponseEntity&lt;String&gt; handleRunTimeException(RuntimeException e) {
        return error(INTERNAL_SERVER_ERROR, e);
    }
    @ExceptionHandler({DogsNotFoundException.class})
    public ResponseEntity&lt;String&gt; handleNotFoundException(DogsNotFoundException e) {
        return error(NOT_FOUND, e);
    }
    @ExceptionHandler({DogsServiceException.class})
    public ResponseEntity&lt;String&gt; handleDogsServiceException(DogsServiceException e){
        return error(INTERNAL_SERVER_ERROR, e);
    }
    private ResponseEntity&lt;String&gt; error(HttpStatus status, Exception e) {
        log.error("Exception : ", e);
        return ResponseEntity.status(status).body(e.getMessage());
    }
}</pre> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">See what is happening here:</p> 
 <ul style="margin-bottom: 10px; color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <li style="padding-bottom: 8px;"> <strong>handleRunTimeException</strong>: This method handles all the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">RuntimeException</code>&nbsp;and returns the status of&nbsp;<em>INTERNAL_SERVER_ERROR.</em> </li> 
  <li style="padding-bottom: 8px;"> <strong>handleNotFoundException:</strong>&nbsp;This method handles&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">DogsNotFoundException</code>&nbsp;and returns&nbsp;<em>NOT_FOUND</em>.</li> 
  <li style="padding-bottom: 8px;"> <strong>handleDogsServiceException:</strong>&nbsp;This method handles&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">DogsServiceException</code>&nbsp;and returns&nbsp;<em>INTERNAL_SERVER_ERROR.</em> </li> 
 </ul> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The key is to catch the checked exceptions in the application and throw&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">RuntimeExceptions</code>. Let these exceptions be thrown out of the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">Controller</code>&nbsp;class, and then, Spring applies the&nbsp;&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">ControllerAdvice</code>&nbsp;to it.</p> 
 <pre name="code" class="java">try {
    //
    // Lines of code
    //
} catch (SQLException sqle) {
    throw new DogsServiceException(sqle.getMessage());
}</pre> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;">Use&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@ResponseStatus</code>&nbsp;to Map the Exception to the ResponseStatus</h3> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Another short way to do achieve this is to use &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@ResponseStatus</code>. It looks simpler and more readable.</p> 
 <pre name="code" class="java">package com.amitph.spring.dogs.web;
import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.ResponseStatus;
@ControllerAdvice
public class DogsServiceErrorAdvice {
    @ResponseStatus(HttpStatus.NOT_FOUND)
    @ExceptionHandler({DogsNotFoundException.class})
    public void handle(DogsNotFoundException e) {}
    @ResponseStatus(HttpStatus.INTERNAL_SERVER_ERROR)
    @ExceptionHandler({DogsServiceException.class, SQLException.class, NullPointerException.class})
    public void handle() {}
    @ResponseStatus(HttpStatus.BAD_REQUEST)
    @ExceptionHandler({DogsServiceValidationException.class})
    public void handle(DogsServiceValidationException e) {}
}</pre> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Have a look at the second handler. We can group multiple similar exceptions and map a common Response Code for them.</p> 
 <h2>Use @ResponseStatus With a Custom Exception</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Spring also does an abstraction for the&nbsp;&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@ControllerAdvice</code><span id="_tmp_pre_13">,&nbsp;</span>and we can even skip writing one.<br>The trick is to define your own&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">RunTimeException</code><span id="_tmp_pre_14">&nbsp;</span>&nbsp;and annotate it with a specific&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@ResponseStatus</code>. When the particular exception is thrown out of a&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">Controller</code>, the&nbsp;Spring abstraction returns the specific Response Status.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Here is a custom&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">RunTimeException</code>&nbsp;class.</p> 
 <pre name="code" class="java">package com.amitph.spring.dogs.service;
import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.ResponseStatus;
@ResponseStatus(HttpStatus.NOT_FOUND)
public class DogsNotFoundException extends RuntimeException {
    public DogsNotFoundException(String message) {
        super(message);
    }
}</pre> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Let’s throw it from anywhere in the code. For example, I am throwing it from a Service method here:</p> 
 <pre name="code" class="java">public List&lt;Dog&gt; getDogs() {
    throw new DogsNotFoundException("No Dog Found Here..");
}</pre> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">I made a call to the respective Controller endpoint, and I received 404 with the following body.</p> 
 <pre name="code" class="java">{
    "timestamp": "2018-11-28T05:06:28.460+0000",
    "status": 404,
    "error": "Not Found",
    "message": "No Dog Found Here..",
    "path": "/dogs"
}</pre> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">What is interesting here is my exception message, which is correctly propagated in the response body.</p> 
 <h2>Summary</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">So, in this Spring Rest Service Exception Handling tutorial, we have seen how to handle an&nbsp;exception with a Spring web application. Spring’s exception abstraction frees you from writing those bulky catch blocks and improve the readability of your code with the help of annotations.</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>