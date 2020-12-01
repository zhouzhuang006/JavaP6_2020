# Spring MVC 框架高级进阶

Spring MVC 是Spring 给我们提供的一个用于简化Web开发的框架

## 主要课程内容

- Spring MVC 应用（常规使用）
- Spring MVC 高级技术（拦截器、异常处理器等）
- 手写MVC 框架（自定义MVC框架。难点、重点）
- Spring MVC 源码深度剖析（难点、重点）
- SSM整合

## 第一部分 Spring MVC 应用

### 第1节 Spring MVC 简介

#### 1.1 MVC 体系结构

三层架构

我们的开发架构一般都是基于两种形式，一种是C/S架构，也就是客户端/服务端；另一种是B/S架构，也就是浏览器/服务器。在JavaEE开发中，几乎全部都是基于B/S架构的开发。那么在B/S架构中，系统标准的三层架构包括：表现层、业务层、持久层。三层架构在我们的实际开发中使用的非常多，所以我们的课程中的案例也都是基于三层架构设计的。

三层架构中， 每一层各司其职，接下来我们说说每层都是负责哪些方面：

- 表现层：

  也就是我们常说的web层。它负责客户端请求，向客户端响应结果，通常客户端使用http协议请求web层，web需要接收http请求，完成http响应。

  表现层包括展示层和控制层：控制层负责接收请求，展示层负责结果的展示。

  表现层依赖业务层，接收到客户端请求一般会调用业务层进行业务处理，并将处理结果响应给客户端。

  表现层的设计一般都是使用MVC模型，（MVC是表现层的设计模型，和其他层没有关系）

- 业务层：

  也就是我们常说的service层。它负责业务逻辑处理，和我们开发项目的需求息息相关。web层依赖业务层，但是业务层不依赖web层。
  
  业务层在业务处理时可能会依赖持久层，如果要对数据持久化需要保证事务一致性。（也就是我们说的，事务应该放到业务层来控制）
  
- 持久层：

  也就是我们是常说的dao层。负责数据持久化，包括数据层即数据库和数据访问层，数据库是对数据进行持久化的载体，数据访问层是业务层和持久层交互的接口，业务层需要通过数据访问层将数据持久化到数据库中，通俗的讲，持久层就是和数据库交互，对数据库表进行增删改查的。

MVC 设计模式

MVC全名是Model View Controller, 是模型（model）- 视图（view）- 控制器（controller）的缩写， 是一种用于设计创建web应用程序表现层的模式。MVC中每个部分各司其职：

- Model(模型)：模型包含业务模型和数据模型，数据模型用于封装数据，业务模型用于处理业务。
- View(视图)：通常指的就是我们的jsp或者html. 作用一般就是展示数据的，通常视图是依据模型数据创建的。
- Controller(控制器)：是应用程序中处理用户交互的部分，作用一般就是处理程序逻辑的。

MVC 提倡：每一层只编写自己的东西，不编写任何其他层的代码；分层是为了解耦，解耦是为了维护方便合分工协作。

#### 1.2 Spring MVC 是什么？

Spring MVC 的全名叫 Spring Web MVC, 是一种基于Java的实现MVC设计模型的请求驱动类型的轻量级Web框架，属于SpringFrameWork的后续产品。

![image-20201124154949119](SpringMVC.assets/image-20201124154949119.png)

SpringMVC 已经成为目前最主流的MVC框架之一，并且随着Spring3.0的发布，全面超越Struts2,成为最优秀的MVC框架。

servlet、struts实现接⼝、springmvc中要让⼀个java类能够处理请求只需要添加注解就ok

它通过⼀套注解，让⼀个简单的 Java 类成为处理请求的控制器，⽽⽆须实现任何接⼝。同时它还⽀持 RESTful 编程⻛格的请求。

总之：Spring MVC和Struts2⼀样，都是 为了解决表现层问题 的web框架，它们都是基于 MVC 设计模 式的。⽽这些表现层框架的主要职责就是处理前端HTTP请求。

Spring MVC 本质可以认为是对servlet的封装，简化了我们serlvet的开发 作⽤：1）接收请求 2）返回响应，跳转⻚⾯

![image-20201124155256369](SpringMVC.assets/image-20201124155256369.png)

第 2 节 Spring Web MVC ⼯作流程

需求：前端浏览器请求url：http://localhost:8080/demo/handle01，前端⻚⾯显示后台服务器的时间 开发过程

 1）配置DispatcherServlet前端控制器

 2）开发处理具体业务逻辑的Handler（@Controller、@RequestMapping）

 3）xml配置⽂件配置controller扫描，配置springmvc三⼤件 

4）将xml⽂件路径告诉springmvc（DispatcherServlet）

2.1 Spring MVC 请求处理流程

![image-20201124155344538](SpringMVC.assets/image-20201124155344538.png)

流程说明 

第⼀步：⽤户发送请求⾄前端控制器DispatcherServlet 

第⼆步：DispatcherServlet收到请求调⽤HandlerMapping处理器映射器 

第三步：处理器映射器根据请求Url找到具体的Handler（后端控制器），⽣成处理器对象及处理器拦截 器(如果 有则⽣成)⼀并返回DispatcherServlet 

第四步：DispatcherServlet调⽤HandlerAdapter处理器适配器去调⽤Handler

第五步：处理器适配器执⾏Handler 

第六步：Handler执⾏完成给处理器适配器返回ModelAndView 

第七步：处理器适配器向前端控制器返回 ModelAndView，ModelAndView 是SpringMVC 框架的⼀个 底层对 象，包括 Model 和 View 

第⼋步：前端控制器请求视图解析器去进⾏视图解析，根据逻辑视图名来解析真正的视图。 

第九步：视图解析器向前端控制器返回View 

第⼗步：前端控制器进⾏视图渲染，就是将模型数据（在 ModelAndView 对象中）填充到 request 域 

第⼗⼀步：前端控制器向⽤户响应结果

#### 2.2 Spring MVC 九⼤组件

- HandlerMapping（处理器映射器）

  HandlerMapping 是⽤来查找 Handler 的，也就是处理器，具体的表现形式可以是类，也可以是 ⽅法。⽐如，标注了@RequestMapping的每个⽅法都可以看成是⼀个Handler。Handler负责具 体实际的请求处理，在请求到达后，HandlerMapping 的作⽤便是找到请求相应的处理器 Handler 和 Interceptor.

- HandlerAdapter（处理器适配器）

  HandlerAdapter 是⼀个适配器。因为 Spring MVC 中 Handler 可以是任意形式的，只要能处理请 求即可。但是把请求交给 Servlet 的时候，由于 Servlet 的⽅法结构都是 doService(HttpServletRequest req,HttpServletResponse resp)形式的，要让固定的 Servlet 处理 ⽅法调⽤ Handler 来进⾏处理，便是 HandlerAdapter 的职责。

- HandlerExceptionResolver

  HandlerExceptionResolver ⽤于处理 Handler 产⽣的异常情况。它的作⽤是根据异常设置 ModelAndView，之后交给渲染⽅法进⾏渲染，渲染⽅法会将 ModelAndView 渲染成⻚⾯。

- ViewResolver

  ViewResolver即视图解析器，⽤于将String类型的视图名和Locale解析为View类型的视图，只有⼀ 个resolveViewName()⽅法。从⽅法的定义可以看出，Controller层返回的String类型视图名 viewName 最终会在这⾥被解析成为View。View是⽤来渲染⻚⾯的，也就是说，它会将程序返回 的参数和数据填⼊模板中，⽣成html⽂件。ViewResolver 在这个过程主要完成两件事情： ViewResolver 找到渲染所⽤的模板（第⼀件⼤事）和所⽤的技术（第⼆件⼤事，其实也就是找到 视图的类型，如JSP）并填⼊参数。默认情况下，Spring MVC会⾃动为我们配置⼀个 InternalResourceViewResolver,是针对 JSP 类型视图的。

- RequestToViewNameTranslator

  RequestToViewNameTranslator 组件的作⽤是从请求中获取 ViewName.因为 ViewResolver 根据 ViewName 查找 View，但有的 Handler 处理完成之后,没有设置 View，也没有设置 ViewName， 便要通过这个组件从请求中查找 ViewName。

- LocaleResolver

  ViewResolver 组件的 resolveViewName ⽅法需要两个参数，⼀个是视图名，⼀个是 Locale。 LocaleResolver ⽤于从请求中解析出 Locale，⽐如中国 Locale 是 zh-CN，⽤来表示⼀个区域。这 个组件也是 i18n 的基础。

- ThemeResolver

  ThemeResolver 组件是⽤来解析主题的。主题是样式、图⽚及它们所形成的显示效果的集合。 Spring MVC 中⼀套主题对应⼀个 properties⽂件，⾥⾯存放着与当前主题相关的所有资源，如图 ⽚、CSS样式等。创建主题⾮常简单，只需准备好资源，然后新建⼀个“主题名.properties”并将资 源设置进去，放在classpath下，之后便可以在⻚⾯中使⽤了。SpringMVC中与主题相关的类有 ThemeResolver、ThemeSource和Theme。ThemeResolver负责从请求中解析出主题名， ThemeSource根据主题名找到具体的主题，其抽象也就是Theme，可以通过Theme来获取主题和 具体的资源。

- MultipartResolver

  MultipartResolver ⽤于上传请求，通过将普通的请求包装成 MultipartHttpServletRequest 来实 现。MultipartHttpServletRequest 可以通过 getFile() ⽅法 直接获得⽂件。如果上传多个⽂件，还 可以调⽤ getFileMap()⽅法得到Map这样的结构，MultipartResolver 的作⽤就 是封装普通的请求，使其拥有⽂件上传的功能。

- FlashMapManager

  FlashMap ⽤于重定向时的参数传递，⽐如在处理⽤户订单时候，为了避免重复提交，可以处理完 post请求之后重定向到⼀个get请求，这个get请求可以⽤来显示订单详情之类的信息。这样做虽然 可以规避⽤户重新提交订单的问题，但是在这个⻚⾯上要显示订单的信息，这些数据从哪⾥来获得 呢？因为重定向时么有传递参数这⼀功能的，如果不想把参数写进URL（不推荐），那么就可以通 过FlashMap来传递。只需要在重定向之前将要传递的数据写⼊请求（可以通过ServletRequestAttributes.getRequest()⽅法获得）的属性OUTPUT_FLASH_MAP_ATTRIBUTE 中，这样在重定向之后的Handler中Spring就会⾃动将其设置到Model中，在显示订单信息的⻚⾯ 上就可以直接从Model中获取数据。FlashMapManager 就是⽤来管理 FalshMap 的。



### 第 3 节 请求参数绑定（串讲）

请求参数绑定：说⽩了SpringMVC如何接收请求参数 

http协议（超⽂本传输协议） 

原⽣servlet接收⼀个整型参数： 

1）String ageStr = request.getParameter("age"); 

2) Integer age = Integer.parseInt(ageStr); 

SpringMVC框架对Servlet的封装，简化了servlet的很多操作 

SpringMVC在接收整型参数的时候，直接在Handler⽅法中声明形参即可

```java
@RequestMapping("xxx")
public String handle(Integer age) {
    System.out.println(age);
}
```

参数绑定：取出参数值绑定到handler⽅法的形参上

- 默认⽀持 Servlet API 作为⽅法参数

  当需要使⽤HttpServletRequest、HttpServletResponse、HttpSession等原⽣servlet对象时，直 接在handler⽅法中形参声明使⽤即可。

  ```java
  /**
   *
   * SpringMVC 对原⽣servlet api的⽀持 url：/demo/handle02?id=1
   *
   * 如果要在SpringMVC中使⽤servlet原⽣对象，⽐如
  HttpServletRequest\HttpServletResponse\HttpSession，直接在Handler⽅法形参中声
  明使⽤即可
   *
   */
  @RequestMapping("/handle02")
  public ModelAndView handle02(HttpServletRequest request,
                               HttpServletResponse response,HttpSession session) {
      String id = request.getParameter("id");
      Date date = new Date();
      ModelAndView modelAndView = new ModelAndView();
      modelAndView.addObject("date",date);
      modelAndView.setViewName("success");
      return modelAndView;
  }  
  ```

  

- 绑定简单类型参数

  简单数据类型：⼋种基本数据类型及其包装类型 

  参数类型推荐使⽤包装数据类型，因为基础数据类型不可以为null 整型：Integer、int 字符串：String 单精度：Float、float 双精度：Double、double 布尔型：Boolean、boolean 说明：对于布尔类型的参数，请求的参数值为true或false。或者1或0 注意：绑定简单数据类型参数，只需要直接声明形参即可（形参参数名和传递的参数名要保持⼀ 致，建议 使⽤包装类型，当形参参数名和传递参数名不⼀致时可以使⽤@RequestParam注解进⾏ ⼿动映射）





