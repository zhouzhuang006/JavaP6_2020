# generator-code代码生成



​     easycode 就不解释了， 大家都是码农。 我一直想做的是一个生成代码的工具，每天的CURD不仅让程序员苦不堪言，更不能解放我们的双手创造更有价值的东西。作为一名资深码农， 当然要解决这些问题。当前市面上有许多代码生成的插件， 确实是很好， 我也从中受到启发，既然代码生成如此重要，又有成熟的框架，为什么不能精益求精更上一层楼呢！或许它将成为我现实自我价值的方向！

> 目前主流的代码生成的原理非常简单，就是查询数据库的信息，然后通过模板引擎渲染出来

## 当前流行的代码生成工具

### 1. renren-generator 定制的代码生成器

https://gitee.com/junjun888/code-generator

### 2. Mybatis Generator

http://mybatis.org/generator/

### 3.SpringBoot_v2

https://gitee.com/bdj/SpringBoot_v2



https://gitee.com/explore/code-generator?lang=Java

排行

缺点：

而且基本都是mysql  数据库， 特别依赖数据库， 而且只能支持数据库定义的字段上取值， 扩展有限； 如果我是mongodb 怎么办！其他的数据源呢？





## 模板引擎

FreeMarker VS Velocity(freemarker模板引擎和velocity模板引擎比较)

```
// velocity
//===========================================
```

如果你对velocity不是很清楚，你可以去官网：http://velocity.apache.org/ 了解更多的信息

当然你也可以到：

[apache的开源项目-模板引擎(Velocity)_学习了两天就上手啦_源码下载](http://www.cnblogs.com/hongten/archive/2013/03/09/hongten_apache_velocity.html)

[利用Velocity自动生成自定义代码_java版_源码下载](http://www.cnblogs.com/hongten/archive/2013/03/10/hongten_velocity_automatic_code_generation.html)

[Velocity基本常用语法](https://www.cnblogs.com/xiohao/p/5788932.html)





```
// freemarker 
//===========================================
```

如果你对freemarker不是很清楚，你可以去官网：http://freemarker.org/ 了解更多信息

同样，你可以可以到：[FreeMarker_模板引擎_代码自动生成器_源码下载](http://www.cnblogs.com/hongten/archive/2013/04/05/hongten_freemarker.html) 了解freemarker的工作情况。

```
//velocity VS freemarker
//===========================================
```







祝愿天下码农早日脱离996！







# 参考文档：

Java之利用Freemarker模板引擎实现代码生成器，提高效率

https://blog.csdn.net/huangwenyi1010/article/details/71249258