---
layout: post
title: "2018.10.15 — @Autowired"
subtitle: "How does @Autowired annotation work in Spring"
author: "Yiru"
tags: 
    - 每日修行
    - Java
    - Spring
---


(https://stackoverflow.com/questions/3153546/how-does-autowiring-work-in-spring)

First and most important - ALL Spring Beans are managed. they "live" inside a container, called - "Application Context".

Second, each application has an entry point to that context. Web applications have a servlet, JSF uses a el-resolver, etc. Also, there is a place where the application context is boostrapped and all beans - autowired. In web application, this can be a startup listener.

Autowireing happens by placing an instance of one bean into the desired field in an instance of another bean. Both classes should be beans, and they should be defined to live in the application context.


@Autowired

private IUserService userService;

public void func(){

    userService.foo();

}


"living" in the application context, means that the ** Context ** instantiates the objects, not u by new operation -- the container finds each injection point and sets an instance there.

When sees @Autowired, Spring will look for a class that matches the property in the ApplicationContext, and inject in automatically. 


@Autowired makes a **constructor, field, setter method or config method ** as to be autowired by Spring's dependency injection facilities.


1. @Autowired on constructor. @Autowired is necessary when several constructors are available, and at least one must be annotated to teach the container which one it has to use.

public class UserService{
    
    @Autowired
    public UserService(){

    }

}

2. @Autowired on setter method

public class UserService{
    private User user;

    @Autowired
    public void setUser(User user){
        this.user = user;
    }
}

3. @Autowired on Field
public class UserService{

    @Autowired
    private User user;

    @Autowired
    public void setUser(User user){
        this.user = user;
    }
}

4. etc

