# Jenkins详细教程



最近花了一段时间研究jenkins这个工具。所以写下这篇文章，算是当做记录吧！

# 一、jenkins是什么？

​    Jenkins是一个开源的、提供友好操作界面的持续集成(CI)工具，起源于Hudson（Hudson是商用的），主要用于持续、自动的构建/测试软件项目、监控外部任务的运行（这个比较抽象，暂且写上，不做解释）。Jenkins用Java语言编写，可在Tomcat等流行的servlet容器中运行，也可独立运行。通常与版本管理工具(SCM)、构建工具结合使用。常用的版本控制工具有SVN、GIT，构建工具有Maven、Ant、Gradle。



# 二、CI/CD是什么？

​     CI(Continuous integration，中文意思是持续集成)是一种软件开发时间。持续集成强调开发人员提交了新代码之后，立刻进行构建、（单元）测试。根据测试结果，我们可以确定新代码和原有代码能否正确地集成在一起。借用网络图片对CI加以理解。



![img](https:////upload-images.jianshu.io/upload_images/6464255-1b6e3bfdbece1492.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/1000/format/webp)

<center>CI</center>

​    CD(Continuous Delivery， 中文意思持续交付)是在持续集成的基础上，将集成后的代码部署到更贴近真实运行环境(类生产环境)中。比如，我们完成单元测试后，可以把代码部署到连接数据库的Staging环境中更多的测试。如果代码没有问题，可以继续手动部署到生产环境。下图反应的是CI/CD 的大概工作模式。



![img](https:////upload-images.jianshu.io/upload_images/6464255-ba088ec7257062c0.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/1000/format/webp)

CI/CD



# 三、使用Jenkins测试、打包

​    Jenkins是一个强大的CI工具，虽然本身使用Java开发，但也能用来做其他语言开发的项目CI。下面讲解如何使用Jenkins创建一个构建任务。

 登录Jenkins， 点击左侧的新建，创建新的构建任务。



![img](https:////upload-images.jianshu.io/upload_images/6464255-22b3c49af599565d.png?imageMogr2/auto-orient/strip|imageView2/2/w/374/format/webp)

跳转到如下界面。任务名称可以自行设定，但需要全局唯一。输入名称后选择构建一个自由风格的软件项目(其他选项不作介绍)。并点击下方的确定按钮即创建了一个构建任务。之后会自动跳转到该job的配置页面。



![img](https:////upload-images.jianshu.io/upload_images/6464255-0febc0bc4ca3cadd.png?imageMogr2/auto-orient/strip|imageView2/2/w/1044/format/webp)

新建自由风格的软件项目



下图是构建任务设置界面，可以看到上方的几个选项**"General", "源码管理"， "构建触发器"，"构建环境"， "构建"， "构建后操作"**。下面逐一介绍。

##  

![img](https:////upload-images.jianshu.io/upload_images/6464255-77998a3e6a70b83f.png?imageMogr2/auto-orient/strip|imageView2/2/w/1032/format/webp)

## 1.General

General是构建任务的一些基本配置。名称，描述之类的。



![img](https:////upload-images.jianshu.io/upload_images/6464255-60c69c788cdaf271.png?imageMogr2/auto-orient/strip|imageView2/2/w/983/format/webp)

General

**项目名称:** 是刚才创建构建任务步骤设置的，当然在这里也可以更改。

**描述:** 对构建任务的描述。 

**丢弃旧的构建：** 服务器资源是有限的，有时候保存了太多的历史构建，会导致Jenkins速度变慢，并且服务器硬盘资源也会被占满。当然下方的"保持构建天数" 和 保持构建的最大个数是可以自定义的，需要根据实际情况确定一个合理的值。

其他几个选项在这里不做介绍，有兴趣的可以查看Jenkins"帮助信息"， 会有一个大概的介绍。不过这些"帮助信息"都是英文的。



![img](https:////upload-images.jianshu.io/upload_images/6464255-7e84819c41bf22a5.png?imageMogr2/auto-orient/strip|imageView2/2/w/994/format/webp)

点击右方的这些"问号"查看"帮助信息"



## 2.源码管理

源码管理就是配置你代码的存放位置。



![img](https:////upload-images.jianshu.io/upload_images/6464255-0d7722861c56901e.png?imageMogr2/auto-orient/strip|imageView2/2/w/978/format/webp)

源码管理

 **Git:** 支持主流的github 和gitlab代码仓库。因我们的研发团队使用的是gitlab，所以下面我只会对该项进行介绍。

**Repository URL**：仓库地址

**Credentials**：凭证。可以使用HTTP方式的用户名密码，也可以是RSA文件。 但要通过后面的"ADD"按钮添加凭证。

**Branches to build**：构建的分支。*/master表示master分支，也可以设置为其他分支。

**源码浏览器**：你所使用的代码仓库管理工具，如github, gitlab. 

**URL**：填入上方的仓库地址即可。

**Version: 8.7**  这个是我们gitlab服务器的版本。

**Subversion：**就是SVN，这里不作介绍。

**
**

## **3.构建触发器**

构建触发器，顾名思义，就是构建任务的触发器。

![img](https:////upload-images.jianshu.io/upload_images/6464255-f1c8d9414165328f.png?imageMogr2/auto-orient/strip|imageView2/2/w/972/format/webp)

**触发远程构建(例如，使用脚本):** 该选项会提供一个接口，可以用来在代码层面触发构建。这里不做介绍，后期可能会用到。

**Build after other projects are built：** 该选项意思是"在其他projects构建后构建"。这里不作介绍，后期可能会用到该选项。

**Build periodically：** 周期性的构建。很好理解，就是每隔一段时间进行构建。日程表类似    linux crontab书写格式。如下图的设置，表示每隔30分钟进行一次构建。

![img](https:////upload-images.jianshu.io/upload_images/6464255-e7b1a18569d25dd9.png?imageMogr2/auto-orient/strip|imageView2/2/w/931/format/webp)

周期构建



**Build when a change is pushed to GitLab：**当有更改push到gitlab代码仓库，即触发构建。后面会有一个触发构建的地址，一般被称为webhooks。需要将这个地址配置到gitlab中，webhooks如何配置后面介绍。这个是常用的构建触发器。

**Poll SCM：**该选项是配合上面这个选项使用的。当代码仓库发生改动，jenkins并不知道。需要配置这个选项，周期性的去检查代码仓库是否发生改动。



![img](https:////upload-images.jianshu.io/upload_images/6464255-10b8f531e0fb09fa.png?imageMogr2/auto-orient/strip|imageView2/2/w/959/format/webp)

十分钟检查一次



# 4.构建环境

构建环境就是构建之前的一些准备工作，如指定构建工具(在这里我使用ant)。

![img](https:////upload-images.jianshu.io/upload_images/6464255-62b5cda6cd2dc333.png?imageMogr2/auto-orient/strip|imageView2/2/w/979/format/webp)

构建环境中的构建工具



**With Ant：**选择这个工具，并指定ant版本和jdk版本。这两个工具的版本我都事先在服务器上安装，并且在jenkins全局工具中配置好了。

其他选项不作介绍，同样可以查看"帮助信息" 获得使用帮助。



# 5.构建

​    选择下方的增加构建步骤。



![img](https:////upload-images.jianshu.io/upload_images/6464255-998ed8e7820364d2.png?imageMogr2/auto-orient/strip|imageView2/2/w/474/format/webp)

增加构建步骤

可以选择的项很多。这里就介绍"Invoke Ant" 和"Execute shell".

**Eexcute shell**： 执行shell命令，该工具是针对linux环境的，windows环境也有对应的工      具"Execute Windows batch command"。 在构建之前，可能我们需要执行一些命令，比如压缩包的解压之类的。为了演示，我就简单的执行 "echo $RANDOM" 这样的linux shell下生产随机数命令。

**Invoke Ant**：Ant是一款java项目构建工具，当然也能用来构建php。





![img](https:////upload-images.jianshu.io/upload_images/6464255-77b5f4427ce22bef.png?imageMogr2/auto-orient/strip|imageView2/2/w/905/format/webp)



**Ant Version**： 选择Ant版本。这个ant版本是安装在jenkins服务器上的版本，并且需要在jenkins"系统工具"中设置好。

**Targets**：要执行的操作，一行一个操作任务。以上图为例，build是构建，tar是打包。

**Build File:** 是Ant构建的配置文件，如果不指定，则是在项目路径下的workspace目录中的build.xml。build.xml文件具体怎么配置，后面再细讲。

**properties:** 设定一些变量，这些变量可以在build.xml 中被引用。

**Send files or execute commands over SSH：**发送文件到远程主机或执行命令(脚本)



![img](https:////upload-images.jianshu.io/upload_images/6464255-b2ffd97252eca6eb.png?imageMogr2/auto-orient/strip|imageView2/2/w/886/format/webp)

**Name**: SSH Server的名称。SSH Server可以在jenkins-系统设置中配置。

**source files**: 需要发送给远程主机的源文件。

**Remove prefix:** 移除前面的路径。如果不设置这个参数，则远程主机会自动创建构建源 source files 包含的那个路径。

**Remote directory**: 远程主机目录。

**Exec command**：在远程主机上执行的命令，或者执行的脚本。





# **6.构建后操作**

​    构建后操作，就是对project构建完成后的一些后续操作，比如生成相应的代码测试报告。



![img](https:////upload-images.jianshu.io/upload_images/6464255-c3797c5affc64e41.png?imageMogr2/auto-orient/strip|imageView2/2/w/1059/format/webp)

**
**

![img](https:////upload-images.jianshu.io/upload_images/6464255-03fdd8935afecc88.png?imageMogr2/auto-orient/strip|imageView2/2/w/1009/format/webp)

邮件通知

**Publish Clover PHP Coverage Report：**发布代码覆盖率xml格式的文件报告。路径会在"build.xml"文件中定义

**Publish HTML reports**：发布代码覆盖率的HTML报告。 

**Report Crap:** 发布crap报告**。**

**E-mail Notification:** 邮件通知，构建完成后发邮件到指定的邮箱。

**以上配置完成后，点击保存。**

# **7.其他相关配置**

 **SSH Server配置**

登录jenkins -- 系统管理 -- 系统设置

配置请看下图



![img](https:////upload-images.jianshu.io/upload_images/6464255-15476f9e273daa58.png?imageMogr2/auto-orient/strip|imageView2/2/w/1108/format/webp)

SSH SERVER

**SSH Servers:** 由于jenkins服务器公钥文件我已经配置好，所以之后新增SSH Servers 只需要配置这一项即可。 

**Name：** 自定义，需要全局唯一。

**HostName:** 主机名，直接用ip地址即可。

**Username:** 新增Server的用户名，这里配置的是root。

**Remote Directory:** 远程目录。jenkins服务器发送文件给新增的server默认是在这个目录。



### Ant 配置文件 "build.xml"

接下来讲解Ant 构建配置文件"build.xml"。 之所以是build.xml 这是因为官方惯例。就好比任何编程语言的入门都会是打印"Hello world". 你也可以用其他名称代替"build.xml" .

下面针对配置文件"build.xml" 关键配置进行说明。

![img](https:////upload-images.jianshu.io/upload_images/6464255-5748077e695741ed.png?imageMogr2/auto-orient/strip|imageView2/2/w/1144/format/webp)

project name就是项目名称，和jenkins所创建的对应。

target name="build" 就是构建的名称，和jenkins构建步骤 那里的targets对应。depends指明构建需要进行的一些操作。

property 用来设置变量。

fileset 这一行指明了一个文件夹，用include来指明需要包含的文件，exclude指明不包含的文件，"tar"即是打包这个文件夹中匹配到的文件。

下面的这些target都是一些实际的操作步骤，比如make_runtime这个"target" 就是创建了一些目录。phpcs就是利用PHP_CodeSniffer这个工具 对PHP代码规范与质量检查工具。



![img](https:////upload-images.jianshu.io/upload_images/6464255-46af5e32428ad102.png?imageMogr2/auto-orient/strip|imageView2/2/w/968/format/webp)



![img](https:////upload-images.jianshu.io/upload_images/6464255-1f70f8f88ad59d66.png?imageMogr2/auto-orient/strip|imageView2/2/w/966/format/webp)

最后这个target "tar" 就是打包文件。因为上面的build 并没有包含这个target，所以默认情况下，执行build是不会打包文件的，所以在jenkins project配置界面，Ant构建那一步的targets，我们才会有"build" 和 "tar" 这两个targets。如果build.xml 中 "build"这个target depends中已经包含"tar" , 就不需要在jenkins中增加"tar"了。

其他一些target 都是利用一些工具对php代码的操作，比如phpunit是进行php单元测试。这一些方面我没有深入的研究，只是进行了一些简单的配置，毕竟不是这方面的专业人士。



### 配置 Gitlab webhooks

在gitlab的project页面 打开**settings**，再打开 **web hooks** 。点击**"ADD WEB HOOK"** 添加webhook。把之前jenkins配置中的那个url 添加到这里，添加完成后，点击**"TEST HOOK"**进行测试，如果显示SUCCESS 则表示添加成功。



![img](https:////upload-images.jianshu.io/upload_images/6464255-9f8d04a1400556f9.png?imageMogr2/auto-orient/strip|imageView2/2/w/246/format/webp)



![img](https:////upload-images.jianshu.io/upload_images/6464255-154a62db330c819b.png?imageMogr2/auto-orient/strip|imageView2/2/w/240/format/webp)

#  



![img](https:////upload-images.jianshu.io/upload_images/6464255-e4d1ea1e1dbde812.png?imageMogr2/auto-orient/strip|imageView2/2/w/1036/format/webp)



![img](https:////upload-images.jianshu.io/upload_images/6464255-c7a687207b2c26fc.png?imageMogr2/auto-orient/strip|imageView2/2/w/1106/format/webp)



![img](https:////upload-images.jianshu.io/upload_images/6464255-ce8ae810bc2cb0d4.png?imageMogr2/auto-orient/strip|imageView2/2/w/1154/format/webp)

配置phpunit.xml

phpunit.xml是phpunit这个工具用来单元测试所需要的配置文件。这个文件的名称同样也是可以自定义的，但是要在"build.xml"中配置好名字就行。默认情况下，用"phpunit.xml", 则不需要在"build.xml"中配置文件名。



![img](https:////upload-images.jianshu.io/upload_images/6464255-aa212d3b3eaff548.png?imageMogr2/auto-orient/strip|imageView2/2/w/798/format/webp)

build.xml中phpunit配置

fileset dir 指定单元测试文件所在路径，include指定包含哪些文件，支持通配符匹配。当然也可以用exclude关键字指定不包含的文件。





![img](https:////upload-images.jianshu.io/upload_images/6464255-dbc0084f6d50a240.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

# 四、进行jenkins project 构建

第一次配置好jenkins project之后，会自动触发一次构建。此后，每当有commit 提交到master分支（前面设置的是master分支，也可以设置为其他分支），就会触发一次构建。当然也可以在project页面手动触发构建。点击左边的"立即构建" 手动触发构建。



![img](https:////upload-images.jianshu.io/upload_images/6464255-8b36f9e13eaf3fda.png?imageMogr2/auto-orient/strip|imageView2/2/w/968/format/webp)

手动触发构建



# 五、构建结果说明

#### **构建状态**

**Successful蓝色**：构建完成，并且被认为是稳定的。

**Unstable黄色**：构建完成，但被认为是不稳定的。

**Failed红色**：构建失败。

**Disable灰色**：构建已禁用



#### 构建稳定性

构建稳定性用天气表示：**晴、晴转多云、多云、小雨、雷阵雨**。天气越好表示构建越稳定，反之亦然。



#### **构建历史界面**

 **console output：** 输出构建的日志信息

# **六、jenkins权限管理**

由于jenkins默认的权限管理体系不支持用户组或角色的配置，因此需要安装第三发插件来支持角色的配置，本文将使用Role Strategy Plugin。基于这个插件的权限管理设置请参考这篇文章:[http://blog.csdn.net/russ44/article/details/52276222](https://link.jianshu.com?t=http%3A%2F%2Fblog.csdn.net%2Fruss44%2Farticle%2Fdetails%2F52276222)，这里不作详细介绍。



至此，就可以用jenkins周而复始的进行CI了，当然jenkins是一个强大的工具，功能绝不仅仅是以上这些，其他方面要是以后用到，我会更新到这篇文章中。有疑问欢迎在下方留言。

最后，放上一张Jenkins的思维导图

![img](https:////upload-images.jianshu.io/upload_images/6464255-cc56d3af1fdd96df.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)





### 参考文档

Jenkins详细教程

https://www.jianshu.com/p/5f671aca2b5a

jenkins 官网

https://jenkins.io/zh/

https://jenkins.io/zh/doc/