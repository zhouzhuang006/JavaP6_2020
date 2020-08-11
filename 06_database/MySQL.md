# MySQL







# 数据库分库分表利器 ShardingSphere

官网地址：

http://shardingsphere.apache.org

官方文档4.x版本：

https://shardingsphere.apache.org/document/legacy/4.x/document/en/overview/



思维导图：

![image-20200806134135968](MySQL.assets/image-20200806134135968.png)







# 知识点扫盲

## MYSQL 之DDL、DML、DCL、TCL的区别

TCL （Transaction Control Language）：事务控制语言

DML（data manipulation language）： 它们是SELECT、UPDATE、INSERT、DELETE，这4条命令是用来对数据库里的数据进行操作的语言 


 DDL（data definition language）： DDL比DML要多，主要的命令有CREATE、ALTER、DROP等，DDL主要是用在定义或改变表（TABLE）的结构，数据类型，表之间的链接 和约束等初始化工作上，他们大多在建立表时使用 

 DCL（Data Control Language）： 是数据库控制功能。是用来设置或更改数据库用户或角色权限的语句，包括（grant,deny,revoke等）语句。在默认状态下，只有

sysadmin,dbcreator,db_owner或db_securityadmin等人员才有权力执行DCL