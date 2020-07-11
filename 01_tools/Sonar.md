# Sonar

https://www.sonarqube.org/

sonar的安装以及使用

https://www.cnblogs.com/qlqwjy/p/10551283.html

sonar 扫描代码并不是一件很容易的事。
 为什么这么说呢，出结果出报告，相对来说很容易，但是谁去follow，谁是owner，优先级等等，背后是一个组织，而且是一个高效、认同、执行力强的组织。所以还是慎入。
 整理下sonar相关的信息。

## sonar key point

### code viewer

核心是代码审查，展示代码源文件和高层次的数据。
 -> 行数
 -> 问题数
 -> 单元覆盖率
 -> 重复度
 -> SCM信息（近期提交代码某行代码的人和时间）
 -> 给定测试文件的测试结果，执行时间和状态

### coverage

coverage中有三种颜色标记：红色表示没有被覆盖；橙色表示部分覆盖；绿色表示完全覆盖。Jacoco还可以显示覆盖特定一行不同测试的数量，同时也能列出这些测试，并定位出这些测试的文件。

### duplications

重复代码的行数并定位。重复密度=重复行数/总行数*100

### tests

可以查询哪个文件被单元测试覆盖，以及有多少行代码被测试覆盖。

### issues

issues有5个等级：

1. confirm 确认一个问题，从open变成confirm。
2. false positive 在全文中查看发现不是一个真正的问题，标记false positive。
3. won‘t fix 可以被接受的技术债。
4. change severity 根据自己的经验来调整严重等级。
5. resolve 修复，修改正确，下次状态就会关闭，否则状态仍然开放。

### dispositioning

讨论决定由谁来解决问题，默认为最后一个提交代码的人。

### general

在issue生命周期中，都可以备注注释，在运行日志中显示细节注释。

### bulk change

所有的这些变更都可以一次性做成多个问题，通过使用问题搜索结果面板的Bulk Change。

### complexity

基于代码路径数量计算复杂度。功能控制流分裂，复杂度依次增加。

1. class 类的平均复杂度
2. file 文件的平均复杂度
3. method 函数的平均复杂度

### documentation

1. line 包含注释或注释代码的行数。不包括仅有注释符号的行数。
2. comment(%) 注释行数密度=注释行数/(代码行数+注释行数)*100。
3. public documented API(%) 公有记录API密度=（公有的API-公有未记录的API）/公有API*100。
4. public undocumented API 不带注释头的公有API
5. commented-out LOC(%) 代码注释行数

### severity

1. blocker 致命的
2. critical 关键的
3. major 主要的
4. minor 微小的
5. info 未知的

### maintainability

code smells 既不算bug，也不在脆弱性里。
 new code smells
 maintainability Rating:A=0-0.05, B=0.06-0.1, C=0.11-0.20, D=0.21-0.5, E=0.51-1
 technical Debt:技术债，修复所有维护问题的成本。
 technical Debt on new code：新代码上的技术债
 technical Debt Ratio：技术债比例=修复成本/开发成本
 technical Debt Ratio on new code：开发者变更代码的花费与相关问题的花费比



作者：jaymz明
链接：https://www.jianshu.com/p/2de96cfcff30
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。