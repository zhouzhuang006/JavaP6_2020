# Spring Boot 高级



## 1. SpringBoot 基础回顾

### 1.1 约定优于配置

```
Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".
We take an opinionated view of the Spring platform and third-party libraries so you can get started with minimum fuss. Most Spring Boot applications need minimal Spring configuration.
```

约定优于配置（Convention over Configuration）, 又称按约定编程，是一种软件设计范式。

本质上说，系统，类库或者框架应该假定合理的默认值，而非要求提供不必要的配置，比如说模型中有一个名为User的类，那么数据库中对应的表就会默认命名为user。只有再偏离这一个约定的时候，例如想要将该表命名为person，才需要写有关这个名字的配置。

比如平时架构师搭建项目就是限制软件开发随便写代码，制定出一套规范，让开发人员按统一的要求进行开发编码测试之类的，这样就加强了开发效率与审查代码效率。所以说写代码的时候就需要按要求命名，这样统一规范的代码就有良好的可读性与维护性了

约定优于配置简单来理解，就是遵循约定



### 1.2 SpringBoot概念

#### 1.2.1 Spring 优缺点分析

优点：

spring 是Java企业版（Java Enterprise Eduition, J2EE）的轻量级代替品。无需开发重量级的Enterprise JavaBean (EJB) , Spring 为企业级Java开发提供了一种相对简单的方法，通过依赖注入和面向切面编程，用简单的Java对象（Plain Old Java Object, POJO）实现了EJB的功能

缺点：

虽然Spring的组件代码是轻量级的，但是他的配置却是重量级的，一开始，Spring用XML配置，而且是很多XML配置。Spring2.5引入了基于注解的组件扫描，这消除了大量针对应用程序自身组件的显式XML配置。Spring3.0引入了基于Java的配置，这是一种类型安全的可重构配置方式，可以代替XML。

所有这些配置都代表了开发时的损耗。因为在思考Spring特性配置和解决业务问题之间需要进行思维切换，所以编写配置挤占了编写应用程序逻辑的时间。和所有框架一样，Spring实用，但与此同时它要求的回报也不少。

除此之外，项目的依赖管理也是一件耗时耗力的事情。在环境搭建时，需要分析要导入哪些库的坐标，而且还需要分析导入与之有依赖关系的其他库的坐标，一旦选错了依赖的版本，随之而来的不兼容问题就会严重阻碍项目的开发进度

#### 1.2.2 SpringBoot 解决上述Spring问题

SpringBoot对上述Spring的缺点进行的改善和优化，基于约定优于配置的思想，可以让开发人员不必在配置与逻辑业务之间进行思维的切换，全身心的投入到业务逻辑的代码编写中，从而大大提高了开发的效率，一定程度上缩短了项目周期

起步依赖

起步依赖本质上是一个Maven项目对象模型（Project Object Model, POM）， 定义了对其他库的传递依赖，这些东西加起来在一起即支持某项功能。

简单的说，起步依赖就是具备某种功能的坐标打包到一起，并提供一些默认的功能。

自动配置

SpringBoot的自动配置，指的是SpringBoot会自动将一些配置类的bean注册进ioc容器，我们可以需要的地方使用@Autowired 或者@Resource等注解来使用它。

“自动”



### 1.3 SpringBoot案例实现



### 1.4单元测试与热部署



### 1.5全局配置文件



### 1.6配置文件属性值的注入



### 1.7自定义配置



### 1.8随机数设置及参数间引用



## 2. SpringBoot原理深入及源码剖析

### 2.1 依赖管理

问题：（1）为什么导入dependency时不需要指定版本？



#### 1.Spring-boot-starter-parent依赖

查看spring-boot-dependencies

```xml

```

继续查看spring-boot-dependencies底层源文件

```xml

```

可以看出 Spring对依赖文件进行了统一版本号管理，例如 activemq/spring/tomcat等



问题：（2）spring-boot-start-parent父依赖启动器的主要作用是进行版本统一管理，那么项目运行依赖的JAR包是从何而来的？

#### 2.Spring-boot-starter-web依赖

查看spring-boot-starter-web依赖文件源码，核心代码具体如下

```xml


```

从上述代码可以发现，spring-boot-starter-web依赖启动器时，就可以实现Web场景开发，而不需要额外导入Tomcat服务器以及其他web依赖文件



### 2.2 自动配置（启动流程）

问题：Spring Boot到底是如何进行自动配置的，都吧哪些组件进行了自动配置？



Spring Boot 应用的启动入口是@SpringBootApplaiction注解标注类中的main()方法



#### 1.@SpringBootConfiguartion注解





#### 2.@EnableAutoConfiguration注解

（1）@AutoConfigurationPackage注解



（2）@Import({AutoConfigurationImportSelector.class})



深入研究loadMatadata方法



深入 getCandidateConfigurations方法



总结

SpringBoot底层实现自动配置的步骤是：

1.springBoot应用启动；

2.@SpringBootApplication起作用；

3.@EnableAutoConfiguration;

4.@AutoConfigurationPackage，这个组合注解主要是

@Import(AutoConfigurationPackages.Registrar.class)，它通过将Registrar类导入到容器中，而Registrar类作用是扫描配置类同级目录以及子包，并将相应的组件导入到springboot创建管理的容器中；

5.@Import(AutoConfigurationImportSelector.class)，它通过将AutoConfigurationImportSelector类导入到容器中，AutoConfigurationImportSelector类作用是通过selectImports方法执行的过程中，会使用内部工具类SpringFactoriesLoader，查找classpath上所有jar包中的META-INF/spring.factories进行加载，实现将配置类信息交给SpringFactory加载器进行一系列的容器创建过程

#### 3.@ComponentScan注解



### 2.3自定义Stater



#### SpringBoot starter机制



#### 为什么要自定义starter



#### 自定义starter的命名规则





### 2.4 执行原理

每个Spring Boot项目都有一个主程序启动类，在主程序启动类中有一个启动项目的main()方法，在该方法中通过执行SpringApplication.run()即可以启动整个Spring Boot程序。

问题：那么SpringApplication.run() 到底是如何做到启动 Spring Boot项目的呢？

下面我们查询run方法的内部源码，核心代码具体如下：

```java
@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

```java
public static ConfigurableApplicationContext run(Class<?> primarySource, String... args) {
    return run(new Class[]{primarySource}, args);
}

public static ConfigurableApplicationContext run(Class<?>[] primarySources, String[] args) {
    return (new SpringApplication(primarySources)).run(args);
}
```

从上述源码可以看出， SpringApplication.run()方法内部执行了两个操作，分别是SpringApplication实例化的创建和调用run()启动项目， 这两个阶段的实现说明具体如下：

#### 1.SpringApplication实例的初始化创建

查看SpringApplication 实例化对象初始化创建的源码信息， 核心代码如下：

```java
public SpringApplication(ResourceLoader resourceLoader, Class<?>... primarySources) {
    this.sources = new LinkedHashSet();
    this.bannerMode = Mode.CONSOLE;
    this.logStartupInfo = true;
    this.addCommandLineProperties = true;
    this.addConversionService = true;
    this.headless = true;
    this.registerShutdownHook = true;
    this.additionalProfiles = Collections.emptySet();
    this.isCustomEnvironment = false;
    this.lazyInitialization = false;
    this.applicationContextFactory = ApplicationContextFactory.DEFAULT;
    this.applicationStartup = ApplicationStartup.DEFAULT;
    this.resourceLoader = resourceLoader;
    Assert.notNull(primarySources, "PrimarySources must not be null");
    this.primarySources = new LinkedHashSet(Arrays.asList(primarySources));
    this.webApplicationType = WebApplicationType.deduceFromClasspath();
    this.bootstrappers = new ArrayList(this.getSpringFactoriesInstances(Bootstrapper.class));
    this.setInitializers(this.getSpringFactoriesInstances(ApplicationContextInitializer.class));
    this.setListeners(this.getSpringFactoriesInstances(ApplicationListener.class));
    this.mainApplicationClass = this.deduceMainApplicationClass();
}
```

从上述代码可以看出， SpringApplication 的初始化过程主要包括4部分，具体说明如下：

（1）this.webApplicationType = WebApplication.deduceFromClasspath() 用于判断当前webApplicationType应用的类型。deduceFromClasspath()方法用于查看Classpath类路径下是否存在某个特征类，从而判断当前webApplicationType类型是SERVLET应用







#### 2.项目的初始化启动





## 3.SpringBoot 数据访问

SpringData是Spring提供的一个用户简化数据库访问、支持云服务的开源框架。它是一个伞形项目，包含了大量关系型数据库及非关系型的数据库访问解决方案，其设计目的是使我们可以快速且简单第使用各种数据访问技术。SpringBoot默认采用整合SpringData的方式统一处理数据访问层，通过添加大量自动配置，引入各种数据访问模板xxxTemplate以及统一的Repository接口，从而达到简化数据访问层的操作。



### 3.1Spring Boot整合MyBatis

MyBatis 是一款优秀的持久层框架，Spring Boot官方虽然没有对MyBatis进行整合，但是MyBatis团队自行适配了对应的启动器，进一步简化了使用MyBatis进行数据的操作

因为Spring Boot框架开发的便利性，所以实现Spring Boot 和数据库访问层框架的整合非常简单，主要是映入对应的依赖启动器，并进行数据库参数相关设置即可

基础环境搭建：

1.数据准备

在MySQL中，先创建了一个数据库SPringBootData, 然后创建了两个表t_article和t_comment并向表中插入数据。其中评论表t_comment的a_id与文章表t_article的主键id相关联

```sql
# 创建数据库

```

2.创建项目，引入相应的启动器



3.编写与数据库表t_comment和t_article对应的实体类Comment和Article



4.编写配置文件



注解方式整合MyBatis



### 3.2Spring Boot整合JPA





### 3.3 Spring Boot整合Redis





## 4.SpringBoot视图技术



### 4.1 支持的视图技术



### 4.2 Thymeleaf



## 5.SpringBoot缓存管理



### 5.1 默认缓存管理



### 5.2 整合Redis缓存实现



### 5.3 自定义Redis缓存序列化机制













