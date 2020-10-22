# Spring Framework



## Spring相关教程/资料

### 官网相关

- [Spring官网](https://spring.io/)、[Spring系列主要项目](https://spring.io/projects)、[Spring官网指南](https://spring.io/guides)、[官方文档](https://spring.io/docs/reference)

## 系统学习教程

### 文档

-  [极客学院Spring Wiki](http://wiki.jikexueyuan.com/project/spring/)
-  [Spring W3Cschool教程 ](https://www.w3cschool.cn/wkspring/f6pk1ic8.html)

### 视频

- [网易云课堂—精通java教程Spring框架开发](http://study.163.com/course/courseMain.htm?courseId=1004475015#/courseDetail?tab=1&35)
- [慕课网相关视频](https://www.imooc.com/)



## 面试必备知识点

### SpringAOP,IOC实现原理

AOP实现原理、动态代理和静态代理、Spring IOC的初始化过程、IOC原理、自己实现怎么实现一个IOC容器？这些东西都是经常会被问到的。

推荐阅读：

- [自己动手实现的 Spring IOC 和 AOP - 上篇](http://www.coolblog.xyz/2018/01/18/自己动手实现的-Spring-IOC-和-AOP-上篇/)

- [自己动手实现的 Spring IOC 和 AOP - 下篇](http://www.coolblog.xyz/2018/01/18/自己动手实现的-Spring-IOC-和-AOP-下篇/)

### AOP

AOP思想的实现一般都是基于 **代理模式** ，在JAVA中一般采用JDK动态代理模式，但是我们都知道，**JDK动态代理模式只能代理接口而不能代理类**。因此，Spring AOP 会这样子来进行切换，因为Spring AOP 同时支持 CGLIB、ASPECTJ、JDK动态代理。

- 如果目标对象的实现类实现了接口，Spring AOP 将会采用 JDK 动态代理来生成 AOP 代理类；
- 如果目标对象的实现类没有实现接口，Spring AOP 将会采用 CGLIB 来生成 AOP 代理类——不过这个选择过程对开发者完全透明、开发者也无需关心。

推荐阅读：

- [静态代理、JDK动态代理、CGLIB动态代理讲解](http://www.cnblogs.com/puyangsky/p/6218925.html) ：我们知道AOP思想的实现一般都是基于 **代理模式** ，所以在看下面的文章之前建议先了解一下静态代理以及JDK动态代理、CGLIB动态代理的实现方式。
- [Spring AOP 入门](https://juejin.im/post/5aa7818af265da23844040c6) ：带你入门的一篇文章。这篇文章主要介绍了AOP中的基本概念：5种类型的通知（Before，After，After-returning，After-throwing，Around）；Spring中对AOP的支持：AOP思想的实现一般都是基于代理模式，在Java中一般采用JDK动态代理模式，Spring AOP 同时支持 CGLIB、ASPECTJ、JDK动态代理，
- [Spring AOP 基于AspectJ注解如何实现AOP](https://juejin.im/post/5a55af9e518825734d14813f) ： **AspectJ是一个AOP框架，它能够对java代码进行AOP编译（一般在编译期进行），让java代码具有AspectJ的AOP功能（当然需要特殊的编译器）**，可以这样说AspectJ是目前实现AOP框架中最成熟，功能最丰富的语言，更幸运的是，AspectJ与java程序完全兼容，几乎是无缝关联，因此对于有java编程基础的工程师，上手和使用都非常容易。Spring注意到AspectJ在AOP的实现方式上依赖于特殊编译器(ajc编译器)，因此Spring很机智回避了这点，转向采用动态代理技术的实现原理来构建Spring AOP的内部机制（动态织入），这是与AspectJ（静态织入）最根本的区别。**Spring 只是使用了与 AspectJ 5 一样的注解，但仍然没有使用 AspectJ 的编译器，底层依是动态代理技术的实现，因此并不依赖于 AspectJ 的编译器**。 Spring AOP虽然是使用了那一套注解，其实实现AOP的底层是使用了动态代理(JDK或者CGLib)来动态植入。至于AspectJ的静态植入，不是本文重点，所以只提一提。
- [探秘Spring AOP（慕课网视频，很不错）](https://www.imooc.com/learn/869):慕课网视频，讲解的很不错，详细且深入
- [spring源码剖析（六）AOP实现原理剖析](https://blog.csdn.net/fighterandknight/article/details/51209822) :通过源码分析Spring AOP的原理

### IOC

- [[Spring框架]Spring IOC的原理及详解](https://www.cnblogs.com/wang-meng/p/5597490.html)
- [Spring IOC核心源码学习](https://yikun.github.io/2015/05/29/Spring-IOC核心源码学习/) :比较简短，推荐阅读。
- [Spring IOC 容器源码分析](https://javadoop.com/post/spring-ioc) :强烈推荐，内容详尽，而且便于阅读。
- [Bean初始化过程](https://www.qzztf.com/2019/08/21/Bean%E5%88%9D%E5%A7%8B%E5%8C%96/#Bean-%E5%AE%9E%E4%BE%8B%E5%8C%96)


## Spring事务管理

- [可能是最漂亮的Spring事务管理详解](https://juejin.im/post/5b00c52ef265da0b95276091)
- [Spring编程式和声明式事务实例讲解](https://juejin.im/post/5b010f27518825426539ba38)

### Spring单例与线程安全

- [Spring框架中的单例模式（源码解读）](http://www.cnblogs.com/chengxuyuanzhilu/p/6404991.html):单例模式是一种常用的软件设计模式。通过单例模式可以保证系统中一个类只有一个实例。spring依赖注入时，使用了 多重判断加锁 的单例模式。

### Spring源码阅读

阅读源码不仅可以加深我们对Spring设计思想的理解，提高自己的编码水平，还可以让自己在面试中如鱼得水。下面的是Github上的一个开源的Spring源码阅读，大家有时间可以看一下，当然你如果有时间也可以自己慢慢研究源码。

 - [spring-core](https://github.com/seaswalker/Spring/blob/master/note/Spring.md)
- [spring-aop](https://github.com/seaswalker/Spring/blob/master/note/spring-aop.md)
- [spring-context](https://github.com/seaswalker/Spring/blob/master/note/spring-context.md)
- [spring-task](https://github.com/seaswalker/Spring/blob/master/note/spring-task.md)
- [spring-transaction](https://github.com/seaswalker/Spring/blob/master/note/spring-transaction.md)
- [spring-mvc](https://github.com/seaswalker/Spring/blob/master/note/spring-mvc.md)
- [guava-cache](https://github.com/seaswalker/Spring/blob/master/note/guava-cache.md)



# Spring 高级框架



## 第一部分 Spring概述

第1节 Spring 简介

> 百度：Spring是于2003 年兴起的一个轻量级的Java 开发框架，由Rod Johnson创建。简单来说，Spring是一个分层的JavaSE/EE full-stack(一站式) 轻量级开源框架。

> Spring官网：Spring makes Java simple. modern. productive. reactive. cloud-read.





第2节 Spring发展历程

1997年 IBM 提出了EJB的思想； 1998年，SUN 制定开发标准规范EJB1.0； 1999年，EJB 1.1发

布； 2001年，EJB 2.0发布； 2003年，EJB 2.1发布； 2006年，EJB 3.0发布；

Rod Johnson（spring之⽗）Expert One-to-One J2EE Design and Development(2002) 阐述了J2EE使⽤EJB开发设计的优

点及解决⽅案

Expert One-to-One J2EE Development without EJB(2004) 阐述了J2EE开发不使⽤EJB的解决

⽅式（Spring雏形）

2017 年 9 ⽉份发布了 Spring 的最新版本 Spring 5.0 通⽤版（GA）

第3节 Spring的优势



第4节 Spring的核心结构

#### 1）Core Container核心容器

core部分包含4个模块：
 1、spring-core：依赖注入IoC与DI的最基本实现
 2、spring-beans：Bean工厂与bean的装配
 3、spring-context：spring的context上下文即IoC容器
 4、spring-expression：spring表达式语言

#### 2）数据访问/集成

数据访问/集成层包括 JDBC，ORM，OXM，JMS 和事务处理模块（简）

#### 3）Web

Web 层由 Web，Web-MVC，Web-Socket 和 Web-Portlet 组成 （简）

#### 4）AOP

AOP：提供了面向切面编程的实现，让你可以定义方法拦截器和切点，从而将逻辑代码分开，降低代码间的耦合性。
 Aspects：提供了对AspectJ的集成支持，这是一个功能强大且成熟的面向方面编程（AOP）框架。
 WebSocket：提供了一个在Web应用中高效、双向的通信工具。
 Instrumentation：提供了在特定的应用服务器中使用类工具的支持和类加载器实现。

#### 5）Test

支持使用JUnit和TestNG对Spring组件进行测试。



第5节 Spring框架版本



## 第二部分 核心思想





## 第三部分 手写实现IOC和AOP





## 第四部分 Spring IOC应用





## 第五部分 Spring IOC源码深度剖析





## 第六部分 Spring AOP应用





## 第七部分 Spring AOP源码深度剖析





