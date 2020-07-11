# MyBatis源码分析





## MyBatis架构原理-架构设计



## MyBatis初始化过程



## 源码剖析-执行SQL流程

SqlSession

SqlSession 是一个接口， 他有两个实现类：DefaultSqlSession(默认)





## MyBatis执行器Executor源码剖析





## MyBatis StatementHandler源码剖析





## MyBatis的mapper代理方式getMapper源码剖析





## MyBatis的invoke方法源码剖析





## 设计模式-构建者设计模式



## 设计模式-工厂模式





## 设计模式-代理模式







# 常见问题



## MyBatis insert 返回id或对象

转载： https://www.cnblogs.com/ws563573095/p/10301809.html

一、背景描述

　　1、在有些场景中，需要根据之前插入的返回值如id（甚至是对象）来设置后续插入，如第一次参入的是父表，后续的是子表的情况。 　　

　　2、如诉讼案件中，存在案件实体表（案件相关人信息，包括原告/被告的代理）entity以及表示代理人和原处理人关系的表relation,后者中要持有实体中代理的id和被代理人的id(parentId)

　因为一个案件常包括很多实体，所以为了方便，实体插入后需要返回带id的实体对象，然后遍历构造代理关系记录。

二、技术分析

　　1、mybatis单挑记录插入返回id(在入参的id属性中，直接返回的依然是影响的行数)

　　　　a、mybatis展示　　　

```xml
<insert id="insertSelective" keyProperty="id" parameterType="DO"  useGeneratedKeys="true">
    insert into fuji_base_entity(ID,*****)
    values(#{id,jdbcType=INTEGER},****)
</insert>
```

　　　　b、keyProperty：获取数据库生成的id放到哪个属性中

　　　　c、useGeneratedKeys：是否使用JDBC的getGenereatedKeys方法获取主键并赋值到keyProperty设置的领域模型属性中

　　PS:   数据库不支持自增的情况（如oracle）

　　　　　　a、mybatis展示　

```xml
<insert id="add" parameterType="EStudent">
    <selectKey keyProperty="id" resultType="_long" order="BEFORE">
        select CAST(RANDOM * 100000 as INTEGER) a FROM SYSTEM.SYSDUMMY1
    </selectKey>
    insert into TStudent(id, name, age) values(#{id}, #{name}, #{age})
</insert>
```

　　　　　　b、order必须是BEFORE,表示在insert执行前处理 　　　　　　

　　　　　　c、keyProperty表示获取的主键存放的属性值 　　

　　　　　　d、selectKey一般在oracle中表示获取序列值

　　2、mybatis批量记录插入返回id

　　　　a、mybatis展示　

```xml
<insert id="insertAuthor" useGeneratedKeys="true"
    keyProperty="id">
  insert into Author (username, password, email, bio) values
  <foreach item="item" collection="list" separator=",">
    (#{item.username}, #{item.password}, #{item.email}, #{item.bio})
  </foreach>
</insert>
```

　　　　b、依然的userGeneratedKeys和keyProperty

　　　　c、入参必须是list，返回是也是回写list中对象的id字段

　　　　d、升级Mybatis版本到3.3.1

　　3、mybatis批量记录插入返回包含id的的对象

　　1、同上2

　　2、循环处理上1　　

三、其他方法返回

　　1、insert操作

　　　　a、默认返回的是插入的记录数

　　2、update操作

　　　　a、底层执行中update操作分两步：查询匹配的记录 和 更新这些结论。 　　　

　　　　b、默认情况下，mybatis的update方法返回的结果是匹配上的记录数，针对同一条sql被执行了两边的情况下影响数为零情况无法判断。

　　　　![img](MyBatisSource.assets/1331298-20190122125301226-977172400.png)

　　　　c、此时，若想update返回的值为受影响的记录数据就需要在声明数据链接是添加设置，如：jdbc:mysql://localhost:3306/ssm?useAffectedRows=true

　　3、delete操作

　　　　a、删除的记录数















