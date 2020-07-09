# Maven

Maven 是 Apache 下的一个纯 Java 开发的开源项目。基于项目对象模型（缩写：POM）概念，Maven利用一个中央信息片断能管理一个项目的构建、报告和文档等步骤。

Maven 是一个项目管理工具，可以对 Java 项目进行构建、依赖管理。

Maven 也可被用于构建和管理各种项目，例如 C#，Ruby，Scala 和其他语言编写的项目。Maven 曾是 Jakarta 项目的子项目，现为由 Apache 软件基金会主持的独立 Apache 项目。

阅读本章之前，您需要有以下基础：`Java 基础`



## 1. 初见

1. 认识Maven

   项目构建工具

2. Maven 功能

   ```
   - 构建
   - 文档生成
   - 报告
   - 依赖
   - SCMs
   - 发布
   - 分发
   - 邮件列表
   ```

3. 优势

   ```
   - 约定优于配置
   - 使用简单
   - 测试支持
   - 构建简单
   - 持续集成 CI  http://maven.apache.org/ci-management.html
   - 插件丰富
   ```

4. 下载 

- https://maven.apache.org/download.cgi

- 解压安装

- maven-model-builder-3.3.9.jar/org/apache/maven/model

- 配置 MVM_HOME
  * Windows path
  * Linux .bash_profile 
  * MAVEN_OPTS
  * 配置setting.xml

```xml
<mirrors>
    <mirror>
        <id>alimaven</id>
        <name>aliyun maven</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
    <mirror>
        <id>ui</id>
        <mirrorOf>central</mirrorOf>
        <name>Human Readable Name for this Mirror.</name>
        <url>http://uk.maven.org/maven2/</url>
    </mirror>
    <mirror>
        <id>osc</id>
        <mirrorOf>central</mirrorOf>
        <url>http://maven.oschina.net/content/groups/public/</url>
    </mirror>
    <mirror>
        <id>osc_thirdparty</id>
        <mirrorOf>thirdparty</mirrorOf>
        <url>http://maven.oschina.net/content/repositories/thirdparty/</url>
    </mirror>
</mirrors>
```

5. 新建一个Maven项目

- 项目结构

 ```
src
  -main
      –java java源代码文件
      –resources 资源库，会自动复制到classes目录里
  -test
      –java 单元测试java源代码文件
target
pom.xml

工程根目录下就只有src和target两个目录
target是有存放项目构建后的文件和目录，jar包、war包、编译的class文件等。
target里的所有内容都是maven构建的时候生成的

my-app
|-- pom.xml
|-- src
    |-- main
    |   `-- java
    |       `-- com
    |           `-- mycompany
    |               `-- app
    |                   `-- App.java
    `-- test
        `-- java
            `-- com
                `-- mycompany
                    `-- app
                        `-- AppTest.java
 ```

6. pom.xml

```
groupId  com.free
artfactId 功能命名
version 版本号
packaging  打包方式 默认是jar
```



## 2. 相遇

### pom.xml 文件解析

#### dependencyManagement

1. 只能出现在父pom
2. 统一版本号
3. 声明 (子POM里用到再引)

####  Dependency

1. Type 默认jar

2. scope

- compile 编译  例如spring-core

- test 测试

- provided编译 例如 servlet

- runtime运行时 例如JDBC驱动实现

- system 本地一些jar  例如短信jar

#### 依赖传递

第一列表示直接依赖的scope，第一行表示间接依赖的scope

|          | compile  | test | provided | runtime  |
| -------- | -------- | ---- | -------- | -------- |
| compile  | compile  | -    | -        | runtime  |
| test     | test     | -    | -        | test     |
| provided | provided | -    | provided | provided |
| runtime  | runtime  | -    | -        | runtime  |

#### 依赖仲裁

- 最短路径原则

- 加载先后原则

#### exclusions

    排除包

#### 生命周期 lifecycle/phase/goal

1. A Build Lifecycle is Made Up of Phases

2. A Build Phase is Made Up of Plugin Goals

 


版本管理

- 1.0-SNAPSHOT

  i. repository 删除

  ii. mvn clean package -U (强制拉一次)

- 主版本号.次版本号.增量版本号-<里程碑版本>

  1.0.0-RELAESE

 

## 常用命令

compile

clean  删除target/

test    test case junit/testNG

package 打包

install  把项目install到local repo

deploy  发本地jar发布到remote

 

## 插件

1. 常用插件

  i. https://maven.apache.org/plugins/ 

  ii. http://www.mojohaus.org/plugins.html 

  iii. findbugs 静态代码检查

  iv. versions 统一升级版本号

1. mvn versions:set -DnewVersion=1.1

  v. source 打包源代码

  vi. assembly 打包zip、war

  vii. tomcat7

2. 自定义插件 
   https://maven.apache.org/guides/plugin/guide-java-plugin-development.html

a)  <packaging>maven-plugin</packaging>

b)  extends AbstractMojo

c)   

d)  mvn install

e)  参数传递

- Profile

a)  使用场景 dev/test/pro

b)  setting.xml 家和公司两套

## 仓库

a)  下载

b)  安装 解压

c)  使用http://books.sonatype.com/nexus-book/reference3/index.html 

i.     http://192.168.1.6:8081/nexus

ii.     admin/admin123

d)  发布

i.     pom.xml 配置 

1.   

2.   

e)  下载jar配置

i.配置mirror

ii.Profile

11.archetype  模版化

a)  生成一个archetype

i.mvn archetype:create-from-project

ii.cd /target/generated-sources/archetype

iii.mvn install

b)  从archetype创建项目 mvn archetype:generate -DarchetypeCatalog=local





### 参考文档：

maven 官网

http://maven.apache.org

菜鸟教程

https://www.runoob.com/maven/maven-tutorial.html

易百教程

https://www.yiibai.com/maven/

