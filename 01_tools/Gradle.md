# Gradle

Gradle是一个基于Apache Ant和Apache  Maven概念的项目自动化构建开源工具。它使用一种基于Groovy的特定领域语言(DSL)来声明项目设置，目前也增加了基于Kotlin语言的kotlin-based DSL，抛弃了基于XML的各种繁琐配置。

官网地址： https://gradle.org/

**功能**

gradle对多工程的构建支持很出色，工程依赖是gradle的第一功能。

gradle支持局部构建，支持多方式依赖管理：包括从[maven](https://baike.baidu.com/item/maven)远程仓库、[nexus](https://baike.baidu.com/item/nexus)私服、ivy仓库以及本地文件系统的jars或者dirs

gradle是第一个构建集成工具，与ant、maven、ivy有良好的相容相关性。

轻松迁移：gradle适用于任何结构的工程，你可以在同一个开发平台平行构建原工程和gradle工程。通常要求写相关测试，以保证开发的插件的相似性，这种迁移可以减少破坏性，尽可能的可靠。这也是重构的最佳实践。

gradle的整体设计是以作为一种语言为导向的，而非成为一个严格死板的框架。

免费开源

　

**gradle提供了什么**

一种可切换的，像maven一样的基于约定的构建框架，却又从不锁住你（约定优于配置）

强大的支持多工程的构建

强大的依赖管理（基于Apache Ivy），提供最大的便利去构建你的工程

全力支持已有的Maven或者Ivy仓库基础建设

支持传递性依赖管理，在不需要远程仓库和pom.xml和ivy配置文件的前提下

基于groovy脚本构建，其build脚本使用[groovy](https://baike.baidu.com/item/groovy)语言编写

具有广泛的领域模型支持你的构建



##### Gradle优势：

1. 一款最新的，功能最强大的构建工具，用它逼格更高
2. 使用程序代替传统的XML配置，项目构建更灵活
3. 丰富的第三方插件，让你随心所欲使用
4. Maven、Ant能做的，Gradle都能做，但是Gradle能做的，Maven、Ant不一定能做。

##### DSL介绍：

全称domain specific language，即特定领域语言

有哪些常见的DSL语言：
 xml、html

DSL与通用编程语言的区别：
 求专不求全，解决特定问题

##### Groovy介绍：

1. 一种基于JVM的敏捷开发语言
2. 结合了Python、Ruby和Smalltalk的许多强大的特性
3. Groovy可以与Java完美结合，而且可以使用Java所有的库

##### Groovy特性：

1. 语法上支持动态类型、闭包等新一代语言特性
2. 无缝集成所有已经存在的Java类库
    3.既支持面向对象编程也支持面向过程编程

##### Groovy优势：

1. 一种更加敏捷的编程语言
2. 入门非常的容易，且功能非常的强大
3. 既可以作为编程语言也可以作为脚本语言



学习网址w3cschool：

https://www.w3cschool.cn/gradle/

Gradle安装使用以及基本操作

https://www.cnblogs.com/linkstar/p/7899191.html

idea+Gradle使用教程

https://blog.csdn.net/pzq915981048/article/details/82852309

