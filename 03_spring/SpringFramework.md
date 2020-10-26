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



> **Spring源码学习的好处：**
>
> 培养代码架构思维，深入理解Spring框架，写出优雅的代码，装逼
>
> **Spring源码学习的原则：**
>
> 定焦原则：定目标，抓主线
>
> 宏观原则：站在上帝视角，关注源码结构和流程（淡化某行代码的编写细节）
>
> **Spring源码学习的技巧：**
>
> 断点：debug模式  观察调用栈
>
> 反调：Find Usages
>
> 经验：Spring框架中doXXX是具体干活的方法
>
> **Spring源码学习的构建：**
>
> 下载源码（GitHub）5.1.2 
>
> https://github.com/spring-projects/spring-framework/
>
> 安装gradle 版本5.6.3   idea 2019.2  JDK 11.0.5 
>
> 
>
> 导入 需要耗费一定的时间
>
> 编译工程 （顺序  core -> oxm -> content -> beans -> aspects -> aop）工程 -> tasks -> other -> compileTestJava



### 第一节 Spring IOC 容器初始化主流程

#### 1.1 Spring IOC容器的继承体系

IoC容器是Spring的核心模块，是抽象了对象管理、依赖关系管理的框架解决方案。Spring提供了很多的容器，其中BeanFactory是顶层容器（根容器），不能被实例化，它定义了所有IoC容器必须遵从的一套原则，具体的容器实现可以增加额外的功能，比如我们常用到的ApplicationContext， 其下更具体的实现如ClassPathXmlApplication 则是包含了解析xml等一系列的内容，AnnotationConfigApplicationContext 则是包含了注解解析等一系列的内容。Spring IoC容器继承体系非常聪明，需要使用哪个层次用哪个层次即可，不必使用功能大而全的。



BeanFactory顶层接口方法栈如下：

![image-20201024153501863](SpringFramework.assets/image-20201024153501863.png)

BeanFactory 容器继承体系

选择 ClassPathXmlApplicationContext 查询继承关系， 快捷键Ctrl + Alt + u

![image-20201024160432670](SpringFramework.assets/image-20201024160432670.png)



> 参考：spring的beanFactory继承体系
>
> https://www.cnblogs.com/sunrainlyb/p/11668490.html
>
> 参考：Spring IOC-BeanFactory的继承体系结构
>
> https://blog.csdn.net/chenzitaojay/article/details/46716071

通过其接口设计，我们可以看到我们一贯使用的ApplicationContext除了继承BeanFactory的子接口，还继承了ResourceLoader、MessageSource等接口，因此其提供的功能也就更丰富了。

下面我们以ClasspathXmlApplicationContext为例，深入源码说明IoC容器的初始化流程。



#### 1.2 Bean生命周期关键时机点

**思路：** 创建一个类DemoBean, 让其实现几个特殊的接口，并分别在接口实现的构造器、接口方法中断点，观察线程调用栈，分析出Bean对象创建和管理关键点的触发时机。

DemoBean类

```java
import org.springframework.beans.BeansException;
import org.springframework.beans.factory.InitializingBean;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ApplicationContextAware;

public class DemoBean implements InitializingBean, ApplicationContextAware {

	private ItBean itBean;

	public void setItBean(ItBean itBean) {
		this.itBean = itBean;
	}

	/**
	 * 构造函数
	 */
	public LagouBean(){
		System.out.println("LagouBean 构造器...");
	}


	/**
	 * InitializingBean 接口实现
	 */
	public void afterPropertiesSet() throws Exception {
		System.out.println("LagouBean afterPropertiesSet...");
	}

	public void print() {
		System.out.println("print方法业务逻辑执行");
	}

	@Override
	public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
		System.out.println("setApplicationContext....");
	}
}
```

BeanPostProcessor 接口实现类

```java
import org.springframework.beans.BeansException;
import org.springframework.beans.factory.config.BeanPostProcessor;
import org.springframework.stereotype.Component;

/**
 * @Author 应癫
 * @create 2019/12/3 16:59
 */
public class MyBeanPostProcessor implements BeanPostProcessor {

	public MyBeanPostProcessor() {
		System.out.println("BeanPostProcessor 实现类构造函数...");
	}

	@Override
	public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
		if("lagouBean".equals(beanName)) {
			System.out.println("BeanPostProcessor 实现类 postProcessBeforeInitialization 方法被调用中......");
		}
		return bean;
	}

	@Override
	public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
		if("lagouBean".equals(beanName)) {
			System.out.println("BeanPostProcessor 实现类 postProcessAfterInitialization 方法被调用中......");
		}
		return bean;
	}
}
```

BeanFactoryPostProcessor 接口实现类

```java

import org.springframework.beans.BeansException;
import org.springframework.beans.factory.config.BeanFactoryPostProcessor;
import org.springframework.beans.factory.config.ConfigurableListableBeanFactory;
import org.springframework.stereotype.Component;

/**
 * @Author 应癫
 * @create 2019/12/3 16:56
 */
public class MyBeanFactoryPostProcessor implements BeanFactoryPostProcessor {

	public MyBeanFactoryPostProcessor() {
		System.out.println("BeanFactoryPostProcessor的实现类构造函数...");
	}

	@Override
	public void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory) throws BeansException {
		System.out.println("BeanFactoryPostProcessor的实现方法调用中......");
	}
}
```

ApplicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	   xmlns:aop="http://www.springframework.org/schema/aop"
	   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	   xsi:schemaLocation="
	    http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd
">

	<!--循环依赖问题-->
	<bean id="lagouBean" class="com.lagou.edu.LagouBean">
		<property name="ItBean" ref="itBean"/>
	</bean>
	<bean id="itBean" class="com.lagou.edu.ItBean">
		<property name="LagouBean" ref="lagouBean"/>
	</bean>


	<!--<bean id="myBeanFactoryPostProcessor" class="com.lagou.edu.MyBeanFactoryPostProcessor"/>
	<bean id="myBeanPostProcessor" class="com.lagou.edu.MyBeanPostProcessor"/>-->


	<!--<bean id="lagouBean" class="com.lagou.edu.LagouBean">
	</bean>-->


	<!--aop配置-->
	<!--横切逻辑-->
	<!--<bean id="logUtils" class="com.lagou.edu.LogUtils">
	</bean>

	<aop:config>
		<aop:aspect ref="logUtils">
			<aop:before method="beforeMethod" pointcut="execution(public void com.lagou.edu.LagouBean.print())"/>
		</aop:aspect>
	</aop:config>-->


</beans>
```

IoC 容器源码分析用例

```java
import com.lagou.edu.LagouBean;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

/**
 * @Author 应癫
 */
public class IocTest {

	/**
	 *  Ioc 容器源码分析基础案例
	 */
	@Test
	public void testIoC() {
		// ApplicationContext是容器的高级接口，BeanFacotry（顶级容器/根容器，规范了/定义了容器的基础行为）
		// Spring应用上下文，官方称之为 IoC容器（错误的认识：容器就是map而已；准确来说，map是ioc容器的一个成员，
		// 叫做单例池, singletonObjects,容器是一组组件和过程的集合，包括BeanFactory、单例池、BeanPostProcessor等以及之间的协作流程）

		/**
		 * Ioc容器创建管理Bean对象的，Spring Bean是有生命周期的
		 * 构造器执行、初始化方法执行、Bean后置处理器的before/after方法、：AbstractApplicationContext#refresh#finishBeanFactoryInitialization
		 * Bean工厂后置处理器初始化、方法执行：AbstractApplicationContext#refresh#invokeBeanFactoryPostProcessors
		 * Bean后置处理器初始化：AbstractApplicationContext#refresh#registerBeanPostProcessors
		 */

		ApplicationContext applicationContext = new ClassPathXmlApplicationContext("classpath:applicationContext.xml");
		LagouBean lagouBean = applicationContext.getBean(LagouBean.class);
		System.out.println(lagouBean);
	}



	/**
	 *  Ioc 容器源码分析基础案例
	 */
	@Test
	public void testAOP() {
		ApplicationContext applicationContext = new ClassPathXmlApplicationContext("classpath:applicationContext.xml");
		LagouBean lagouBean = applicationContext.getBean(LagouBean.class);
		lagouBean.print();
	}
}

```

(1) 分析Bean的创建是在容器初始化时还是在getBean时

![image-20201026203145696](SpringFramework.assets/image-20201026203145696.png)



根据断点调试，我们发现，在未设置延迟加载的前提下，Bean的创建是在容器初始化过程中完成的。

（2） 分析构造函数调用情况



![image-20201026203620503](SpringFramework.assets/image-20201026203620503.png)



![image-20201026203602105](SpringFramework.assets/image-20201026203602105.png)



（3）分析InitializingBean 之 afterPropertiesSet 初始化方法调用情况

![image-20201026204021977](SpringFramework.assets/image-20201026204021977.png)



![image-20201026203949457](SpringFramework.assets/image-20201026203949457.png)

通过如上观察，我们发现InitializingBean 中 afterPropertiesSet方法的调用时机也是在AbstractApplicationContext类refresh方法的finishBeanFactoryInitialization(beanFactory);

(4) 分析BeanFactoryPOstProcessor 初始化和调用情况

分别在构造函数、postProcessBeanFactory 方法处打断点，观察调用栈，发现BeanFactoryPostProcessor 初始化在AbstractApplicationContext类refresh方法的invokeBeanFactoryPostProcessors(beanFactory);

postProcessBeanFactory 调用在AbstractApplicationContext类refresh方法的invokeBeanFactoryPostProcessors(beanFactory);



(5) 分析BeanPostProcessor 初始化和调用情况

分别在构造函数、postProcessBeanFactory 方法处打断点，观察调用栈，发现BeanPostProcessor 初始化在AbstractApplicationContext 类refresh 方法的registerBeanPostProcessors(beanFactory);

postProcessBeforeInitialization 调用在AbstractApplicationContext 类refresh 方法的finishBeanFactoryInitialization（beanFactory）;

postProcessAfterInitialization（beanFactory）;

(6) 总结

根据上面的调试分析， 我们发现Bean对象创建的几个关键时机点代码层级的调用都在AbstractApplicationContext 类的refresh方法中， 可见这个方法对于Spring IoC容器初始化来说相当关键， 汇总如下：

| 关键点                            | 触发代码                                                     |
| --------------------------------- | ------------------------------------------------------------ |
| 构造器                            | refresh#finishBeanFactoryInitialization(beanFactory)(beanFactory) |
| BeanFactoryPostProcessor 初始化   | refresh#invokeBeanFactoryPostProcessors(beanFactory)         |
| BeanFactoryPostProcessor 方法调用 | refresh#invokeBeanFactoryPostProcessors(beanFactory)         |
| BeanPostProcessor 初始化          | registerBeanPostProcessors(beanFactory)                      |
| BeanPostProcessor方法调用         | refresh#finishBeanFactoryInitialization(beanFactory)         |



 











## 第六部分 Spring AOP应用





## 第七部分 Spring AOP源码深度剖析





