---
layout: post
title: "@RequestBody VS @ResponseBody"
author: "Yiru"
tags: 
    - SpringBoot
    - Java
    - 内功修炼    
---

#@RequestBody VS @ResponseBody

最近犯的比较低级的错误之一: 

在使用RequestBody传递参数的时候, 用GET方法, 而没有去认真看一看, RequestBody 是怎么在SpringBoot内部, 进行参数获取的.

//
@RequestBody annotation indicating a method parameter should be found to the *body* of the web request.

To put it in layman terms, the @RequestBody annoation binds the HTTPRequest body to the domain object.

Spring framework automatically deserializes incoming HTTPRequest to the Java object using *HttpMessageConverter*.

The Body of the request is passed through an HttpMessageConverter to resolve the method argument depending on the content type
of the request. Optionally, automatic validation can be applied by annotating the argument with @Valid.





@ResponseBody

This annotation indicates a method return value should be bound to the web response body. 

To put this in simple words, @ResponseBody tell Spring framework to serialize return object into JSON or XML and send this information back as part of the HTTPResponse.

With Spring 4.x, if we are working on the REST API, we should not use @ResponseBody on method level, but rather use @RestController on class level.

@RestController is a *composed annotation* that is itself meta-annotated with @Controller and @ResponseBody.


{
    @RestController
    public class TestController{
        @Autowired
        private TestService service;

        @PostMapping("/test")
        public ResponseEntity<TestEntity>  test(@RequestBody TestBody testBody){

            return service.test(testBody);
        }
        
    }
}

or 

{
    @Controller
    public class TestController{

        @Autowired
        private TestService service;

        @PostMapping("/test")
        public @ResponseBody TestEntity test(@RequestBody TestBody testBody){

            return service.test(testBody);
        }

    }

}

