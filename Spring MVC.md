#Spring MVC

01 框架原理和入门配置

02 非注解的处理器映射器和适配器

03 注解的处理器映射器和适配器

04 前端控制器

05 入门程序小结

06 springmvc整合mybatis(IDEA中通过maven构建)

07 springmvc整合mybatis之mapper

08 springmvc整合mybatis之service

09 springmvc整合mybatis之controller

10 springmvc注解开发之商品修改功能

11 springmvc注解开发之简单参数绑定

12 springmvc注解开发之包装类型参数绑定

13 springmvc注解开发之集合类型参数绑定

14 springmvc校验

15 数据回显

16 异常处理器

17 上传图片

18 json数据交互

19 RESTful支持

20 拦截器

21 springmvc整合mybatis遇到的问题及解决小结

22 springmvc开发小结

###什么是springMVC？

springmvc是spring框架的一个模块，springmvc和spring无需通过中间整合层进行整合。（struts2与Spring整合的时候需要借助单独的jar包）

springmvc是一个基于mvc的web框架。

### MVC在b/s系统 下的应用
mvc是一个设计模式，mvc在b/s系统下的应用：
![](https://i.imgur.com/eZulATF.png)


###SpringMVC框架原理
![](https://i.imgur.com/tHRuUYM.png)

**步骤**

1. 发起请求到前端控制器 (DispatcherServlet)
2. 前端控制器请求处理器映射器 (HandlerMapping) 查找 Handler (可根据 xml 配置、注解进行查找)
3. 处理器映射器 (HandlerMapping) 向前端控制器返回 Handler
4. 前端控制器调用处理器适配器 (HandlerAdapter) 执行 Handler
5. 处理器适配器 (HandlerAdapter) 去执行 Handler
6. Handler 执行完，给适配器返回 ModelAndView (SpringMVC 框架的一个底层对象)
7. 处理器适配器 (HandlerAdapter) 向前端控制器返回 ModelAndView
8. 前端控制器 (DispatcherServlet) 请求视图解析器 (ViewResolver) 进行视图解析，根据逻辑视图名解析成真正的视图 (jsp)
9. 视图解析器 (ViewResolver) 向前端控制器 (DispatcherServlet) 返回 View
10. 前端控制器进行视图渲染，即将模型数据 (在 ModelAndView 对象中)填充到 request 域
11. 前端控制器向用户响应结果

**组件及其作用**

1. 前端控制器 (DispatcherServlet)

接收请求，响应结果，相当于转发器，中央处理器。

有了DispatcherServlet减少了其他组件之间的耦合度

2. 处理器映射器 (HandlerMapping)

作用：根据请求的 url 查找 Handler

3. 处理器 (Handler)

注意：编写Handler时按照HandlerAdapter的要求去做，这样适配器才可以去正确执行Handler

4. 处理器适配器 (HandlerAdapter)

作用：按照特定规则（HandlerAdapter要求的规则）执行Handler。

5. 视图解析器 (ViewResolver)

作用：进行视图解析，根据逻辑视图解析成真正的视图 (View)

6. 视图 (View)

View 是一个接口实现类支持不同的 View 类型（jsp,pdf等等）
**注意：只需要程序员开发，处理器和视图。**

### springMVC入门程序

环境搭建

new => project => maven 选择maven-archetype-webapp并 勾中create from archtype
如果不勾上，则需要手动建webapp的目录

在src/main下新建文件夹webapp

pom.xml文件：
    //添加依赖
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.1.0.RELEASE</version>
    </dependency>


* 配置前端控制器

配置文件web.xml
**在web.xml配置前端控制器，让Spring MVC拦截并处理所有的请求。DispatcherServlet是前端控制器，所有来自客户端的请求，都会交由它去处理。**

    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/cache http://www.springframework.org/schema/cache/spring-cache.xsd http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!--启用注解扫描-->
    <context:component-scan base-package="com.XXX.项目名.controller"/>

    <!--启用 mvc 的常用注解-->    
    <mvc:annotation-driven validator="myValidator" conversion-service="conversionService" >
        <mvc:message-converters>
            <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
                <property name="objectMapper">
                    <bean class="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean">
                        <property name="failOnEmptyBeans" value="false" />
                    </bean>
                </property>
            </bean>
        </mvc:message-converters>

    </mvc:annotation-driven>

Spring MVC 在启动的时候会初始化容器，所以需要通过 xml 配置其容器的初始化。创建一个Spring-Mvc.xml:

* 配置Handler
 
将编写Handler在spring容器加载
    <!-- 配置Handler -->
    <bean name="/queryItems.action" class="com.iot.ssm.controller.ItemsController"/>


* 配置处理器映射器
在classpath下的springmvc.xml中配置处理器映射器

    <!-- 处理器映射器
    将bean的name作为url进行查找，需要在配置Handler时指定beanname(就是url)
    -->
    <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
* 配置处理器适配器
所有处理器适配器都实现了HandlerAdapter接口

    <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter">

demo:

    public boolean supports(Object handler) {
            return handler instanceof Controller;
    }


此适配器能执行实现Controller接口的Handler

配置视图解析器
需要配置解析jsp的视图解析器

 <!-- 视图解析器
    解析jsp,默认使用jstl,classpath下要有jstl的包
    -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"/>



在springmvc.xml中视图解析器配置前缀和后缀：

    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <!-- 配置jsp路径的前缀 -->
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <!-- 配置jsp路径的后缀 -->
        <property name="suffix" value=".jsp"/>
    </bean>

程序中不用指定前缀和后缀：

    //指定视图
    //下边的路径，如果在视图解析器中配置jsp的路径前缀和后缀，修改为items/itemsList
    //modelAndView.setViewName("/WEB-INF/jsp/items/itemsList.jsp");
    
    //下边的路径配置就可以不在程序中指定jsp路径的前缀和后缀
    modelAndView.setViewName("items/itemsList");