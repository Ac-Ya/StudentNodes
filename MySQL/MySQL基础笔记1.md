# **第三章**、基本的SELECT	

## 1.SQL概述

### 1.1SQL 背景知识

- 1946 年，世界上第一台电脑诞生，如今，借由这台电脑发展起来的互联网已经自成江湖。在这几十
  年里，无数的技术、产业在这片江湖里沉浮，有的方兴未艾，有的已经几幕兴衰。但在这片浩荡的
  波动里，有一门技术从未消失，甚至“老当益壮”，那就是SQL。
  - 45 年前，也就是1974年IBM 研究员发布了一篇揭开数据库技术的论文《SEQUEL：一门结构
    化的英语查询语言》，直到今天这门结构化的查询语言并没有太大的变化，相比于其他语
    言，`SQL的半衰期可以说是非常长了`。
- 不论是前端工程师，还是后端算法工程师，都一定会和数据打交道，都需要了解如何又快又准确地
  提取自己想要的数据。更别提数据分析师了，他们的工作就是和数据打交道，整理不同的报告，以
  便指导业务决策。

- SQL（Structured Query Language，结构化查询语言）是使用关系模型的数据库应用语言， 与数据直
  接打交道 ，由 IBM 上世纪70年代开发出来。后由美国国家标准局（ANSI）开始着手制定SQL标准，
  先后有 SQL-86 ，SQL-89，SQL-92 ，SQL-99 等标准。
  - SQL 有两个重要的标准，分别是 `SQL92 和 SQL99`，它们分别代表了 92 年和 99 年颁布的 SQL 标
    准，我们今天使用的 SQL 语言依然遵循这些标准。
- 不同的数据库生产厂商都支持SQL语句，但都有特有内容。

![09PX.png](https://i.328888.xyz/img/2022/11/27/09PX.png)

### 1.2 SQL分类

SQL语言在功能上主要分为如下3大类：

- `DDL（Data Definition Languages、数据定义语言`，这些语句定义了不同的数据库、表、视图、索引等数据库对象，还可以用来创建、删除、修改 	数据库和数据表的结构。
  	主要的语句关键字包括 `CREATE 、 DROP 、 ALTER `等。

- `DML（Data Manipulation Language、数据操作语言）`，用于添加、删除、更新和查询数据库记录，并检查数据完整性。
  	主要的语句关键字包括 INSERT 、 DELETE 、 UPDATE 、 SELECT 等。
    	`SELECT是SQL语言的基础，最为重要`。
- `DCL（Data Control Language、数据控制语言）`，用于定义数据库、表、字段、用户的访问权限和安全级别。
  	主要的语句关键字包括 GRANT 、 REVOKE 、 COMMIT 、 ROLLBACK 、 SAVEPOINT 等。
- `DQL(Data Query Language 数据查询语言)` ,用于查询数据。

> 还有单独将 COMMIT 、 ROLLBACK 取出来称为TCL （Transaction Control Language，事务控制语言）。



## 2.SQL语言的规则与规范

### 2.1 基本规则

- SQL 可以写在一行或者多行。为了`提高可读性，各子句分行写，必要时使用缩进`
- 每条命令以 `; 或 \g 或 \G `结束
- `关键字不能被缩写也不能分行`
- 关于标点符号
  - 必须保证所有的()、单引号、双引号是成对结束的
  - 必须使用`英文状态下的半角输入方式`
  - `字符串型和日期时间类型的数据可以使用单引号（' '）表示`
  - `列的别名，尽量使用双引号（" "）`，而且不建议省略`as`

### 2.2 SQL大小写规范（建议遵守）

- MySQL 在 `Windows 环境下是大小写不敏感的`
- MySQL 在 `Linux 环境下是大小写敏感的`
  - `数据库名、表名、表的别名、变量名是严格区分大小写的`
  - `关键字、函数名、列名(或字段名)、列的别名(字段的别名) 是忽略大小写的。`
- 推荐采用统一的书写规范：
  - `数据库名、表名、表别名、字段名、字段别名等都小写`
  - `SQL 关键字、函数名、绑定变量等都大写`

### 2.3 注释

- 单行注释：#注释文字(MySQL特有的方式)
- 单行注释：-- 注释文字(--后面必须包含一个空格。)
- 多行注释：/* 注释文字 */

### 2.4 命名规则

- 数据库、表名不得超过30个字符，变量名限制为29个
- 必须只能包含 A–Z, a–z, 0–9, _共63个字符
- 数据库名、表名、字段名等对象名中间不要包含空格
- 同一个MySQL软件中，数据库不能同名；同一个库中，表不能重名；同一个表中，字段不能重名
  必须保证你的字段没有和保留字、数据库系统或常用方法冲突。如果坚持使用，请在SQL语句中使
  用``（着重号）引起来
- 保持字段名和类型的一致性，在命名字段并为其指定数据类型的时候一定要保证一致性。假如数据
  类型在一个表里是整数，那在另一个表里可就别变成字符型了

### 2.5 导入数据库表

- 方法一、通过指令： `source 【文件的全路径名】`

- 方法二、基于图形化界面的工具导入数据

## 3.基本的select语句

### 3.0 select 无子句

```sql
SELECT 1；
SELECT 9/2;

# 与下面结构一样
SELECT 1
FROM DUAL;  -- dual 伪表
```

### 3.1 select ... from 

基本语法 `SELECT 字段1,字段2,... FROM 表名`

```SQL
SELECT  标识选择那些列
FROM    标识从那张表中查询

SELECT *
FROM　employee; 
# （*） 表示查询表中的所有列
```

> 一般情况下，除非需要使用表中所有的字段数据，最好不要使用通配符‘*’。使用通配符虽然可以节省输入查询语句的时间，但是获取不需要的列数据通常会降低查询和所使用的应用程序的效率。通配符的优势是，当不知道所需要的列的名称时，可以通过它获取它们。
> 	在生产环境下，不推荐你直接使用 SELECT * 进行查询。

### 3.2 列的别名 AS

使用 `AS` 关键字来给列取别名,当字段名过长，或需要重新计算时，我们可以重命名一个列名

```sql
# 使用AS（alias） 关键字 可省略
# 列的别名可以使用 "" 引起来 也可以使用中文
#【注】列的别名使用双引号，不要使用单引号
SELECT employee_id AS emp_id,last_name AS lname,department_id AS depm_id
FROM  employees;

SELECT employee_id AS "员工ID",last_name AS "姓",department_id AS "部门ID"
FROM  employees;
```

### 3.3 去除重复行 DISTINCT

​	默认情况下，查询会返回所有行的数据（包括重复的），我们可以通过关键字`DISTINCT` 来去除重复行,提高查询效率

```sql
# 在employees中查询所有部门ID
SELECT department_id    -- 没有去重的共107条记录
FROM employees;

SELECT DISTINCT department_id -- 去重后的共12条记录
FROM employees;
```

### 3.4 空值参与运算

​	所有`运算符或列`值遇到null值，运算的`结果都为null`

```sql
SELECT employee_id,salary,commission_pct,
12 * salary * (1 + commission_pct) "annual_sal"
FROM employees;
```

​	`【注】`在 MySQL 里面， 空值不等于空字符串。一个空字符串的长度是 0，而一个空值的长度是空。而且，在 MySQL 里面，空值是占用空间的。

### 3.5 着重号 ``

​	如果表中的字段名，表明等，和保留字、数据库系统或常用方法冲突，并且我们需要使用该命名时，我们可以通过 `` 来标识。

```sql
# 在数据库中有一张ORDER 表，查询该表时需要使用``
SELECT * 
FROM ORDER;  -- 错误语法   ORDER为关键字

SELECT * 
FROM `ORDER`;
```

### 3.6 显示表结构 DESCRIBE

​	使用 `DESCRIBE` 或 `DESC` 命令，表示表结构。

```sql
# 语法
DESCRIBE employees;
DESC employees;
/*
	其中，各个字段的含义分别解释如下：
	Field：表示字段名称。
	Type：表示字段类型，这里 barcode、goodsname 是文本型的，price 是整数类型的。
  	Null：表示该列是否可以存储NULL值。
	Key：表示该列是否已编制索引。PRI表示该列是表主键的一部分；UNI表示该列是UNIQUE索引的一
			部分；MUL表示在列中某个给定值允许出现多次。
	Default：表示该列是否有默认值，如果有，那么值是多少。
	Extra：表示可以获取的与给定列有关的附加信息，例如AUTO_INCREMENT等。
*/
```

### 3.7 基本WHERE语句

​	使用`WHERE`关键字来对表中数据进行过滤

```sql
# 基本语法
# SELECT 字段1,字段2
# FROM 表名
# WHERE 过滤条件
-- 使用WHERE 子句，将不满足条件的行过滤掉
-- WHERE子句紧随 FROM子句

# 查询部门ID为90的员工信息
SELECT employee_id, last_name, job_id, department_id
FROM employees
WHERE department_id = 90 ;
```





# 第四章、运算符

## 1.运算符优先级

![gPGQ.png](https://i.328888.xyz/img/2022/11/28/gPGQ.png)



## 2.算术运算符

![Mfgz.png](https://i.328888.xyz/img/2022/11/29/Mfgz.png)

### 2.1 加法和减法运算

```sql
SELECT 100, 100 + 0, 100 - 0, 
100 + 50 -30, 100 + 35.5, 100 - 35.5,
100 + '1',100 + null
FROM DUAL;
```

`【结论】`

- 一个`整数类型`的值对`整数`进行加法和减法操作，结果还是一个`整数`；

- 一个`整数类型`的值对`浮点数`进行加法和减法操作，结果是一个`浮点数`；

- `加法和减法的优先级相同`，进行先加后减操作与进行先减后加操作的结果是一样的；

- 在Java中，+的左右两边如果有字符串，那么表示字符串的拼接。

  但是在`MySQL`中` + `只表示数值`相加`,`没有字符串拼接的用途`。

  如果遇到`非数值类型`，先尝试转成数值(隐式转换)，如果转失败，就按0计算。"1" 转为 1 ，"a"转为 0

- （补充：MySQL中字符串拼接要使用字符串函数CONCAT()实现）

  

### 2.2 乘法、除法和取模运算

```sql
SELECT 100 * 2,100 * 1.0,100 / 2,100 / 2.0,
100 * 1 / 2,100 + 50 - 100 * 1 / 2,
100 * '2',100 * null,100 * 'a',100 / 0   -- 100 / 0结果为null
FROM DUAL;

# 除法的第二种写法
SELECT 100 DIV 2
FROM DUAL;

# 计算员工的年工资
SELECT employee_id,salary * 12 AS 'ANNUL_SAL'
FROM employees;

# 取模运算有两种写法 一种是符号 %  另一种是字符 MOD
SELECT 12 % 3, 12 MOD 5 FROM DUAL;
```

`【结论】`

- 一个数乘以整数1和除以整数1后仍得原数；
- 一个数`乘以浮点数`1和`除以浮点数`1后变成浮点数，`数值与原数相等`；
- 一个数除以整数后，不管是否能除尽，结果都为一个浮点数；
- 一个数除以另一个数，除不尽时，结果为一个浮点数，并保留到小数点后4位；
- 乘法和除法的优先级相同，进行先乘后除操作与先除后乘操作，得出的结果相同。
- `在数学运算中，0不能用作除数，在MySQL中，一个数除以0为NULL。`

## 3.比较运算符

> 比较运算符用来对表达式左边的操作数和右边的操作数进行比较，`比较的结果为真则返回1`，`比较的结果为假则返回0`，`其他情况则返回NULL`。

![MWjp.png](https://i.328888.xyz/img/2022/11/29/MWjp.png)

### 3.1 等于运算

```sql
SELECT 1 = 1, 1 = '1', 1 = 0, 'a' = 'a', 'A' = 'a',
(5 + 3) = (2 + 6),
'' = NULL , NULL = NULL
FROM DUAL;

# 结果 1 1 0 1 1 1 null null	

SELECT 'a' = 'a' , 'ab' > 'aaa'
FROM DUAL;
```

`【遵循等号比较规则】`

- 如果等号两边的值、字符串或表达式都为字符串，则MySQL会按照字符串进行比较，其比较的

  是每个字符串中字符的ANSI编码是否相等。【注】windows中会忽略大小写

  （`一个字符串多个字符，则会依次比较从第一个字符开始，如果相同位数的字符相同就会比较下一位，直到出现不同的`）

- 如果等号两边的值都是整数，则MySQL会按照整数来比较两个值的大小。

- 如果等号两边的值一个是整数，另一个是字符串，则MySQL会将字符串转化为数字进行比较（能转的就转数字不能的就转为0）。

- 如果等号两边的值、字符串或表达式中有一个为NULL，则比较结果为NULL。 【注】 NULL = NULL 的结果为0

- SQL中赋值符号使用 :=

### 3.2 安全等于运算

`安全等于` : <=> 在进行大部分比较运算时与 = 的作用一样，在进行 null 的比较时会有不同

```sql
# 查询 commission_pct 为 NULL的员工信息 
SELECT * 
FROM employees
WHERE commission_pct = NULL; -- 执行此语句没有结果
-- 使用 = 时null参与运算时没有结果

# 使用 <=> 可以查询 NULL <=> NULL的结果为 1
SELECT * 
FROM employees
WHERE commission_pct <=> NULL;
```

<u>可以看到，使用安全等于运算符时，两边的操作数的值都为NULL时，返回的结果为1而不是NULL，其他返回结果与等于运算符相同。</u>

### 3.3 不等于运算

```sql
# sql语句中不等于运算可以使用 <> 和 != 两种符号
SELECT 1 <> 1, 1 != 2, 
'a' != 'b', (3+4) <> (2+6),
'a' != NULL, NULL <> NULL
FROM DUAL;

# 结果  0 1 1 1 null null
```

- 不等于运算符（<>和!=）用于判断两边的数字、字符串或者表达式的值是否不相等，

  如果不相等则返回1，相等则返回0。

- 不等于运算符不能判断NULL值。

- `如果两边的值有任意一个为NULL，或两边都为NULL，则结果为NULL。`

### 3.4 非符号的比较运算

![MpMt.png](https://i.328888.xyz/img/2022/11/29/MpMt.png)

#### 3.4.1 空运算

​	`IS NULL或者ISNULL() 判断一个值是否为NULL，如果为NULL则返回1，否则返回0。 `

```sql
# 查询 commission_pct 为 NULL的员工信息 
# 1
SELECT * FROM employees WHERE commission_pct <=> NULL;
# 2
SELECT * FROM employees WHERE commission_pct IS NULL;
#3
SELECT * FROM employees WHERE ISNULL(commission_pct);
```

#### 3.4.2 非空运算

​	`IS NOT NULL 判断一个值是否不为NULL，如果不为NULL则返回1，否则返回0。`

```sql
# 查询 commission_pct 不为 NULL的员工信息 
# 1
SELECT * FROM employees WHERE commission_pct IS NOT NULL;
# 2 
SELECT * FROM employees WHERE NOT commission_pct <=> NULL;
```

#### 3.4.3 最大最小运算符

```sql
# 最大运算符	语法格式为：GREATEST(值1，值2，...，值n)。其中，n表示参数列表中有n个值。当有
# 两个或多个参数时，返回值为最大值。假如任意一个自变量为NULL，则GREATEST()的返回值为NULL。
SELECT GREATEST(1,0,2), GREATEST('b','a','c'), GREATEST(1,NULL,2)
FROM DUAL;
# 结果 2 c NULL 

# 最小运算符：语法格式为：LEAST(值1，值2，...，值n)。
# 其中，“值n”表示参数列表中有n个值。在有两个或多个参数的情况下，返回最小值。假如任意一个自变量为NULL，则LEAST()的返回值为NULL。
SELECT LEAST (1,0,2), LEAST('b','a','c'), LEAST(1,NULL,2);
# 结果 0 a NULL 
```

`【结论】`

- 当参数中是整数或者浮点数时，GREATEST或LEAST将返回其中最大的值或最小的值；
- 当参数为字符串时，返回字母表中顺序最靠后的字符或靠前的字符；当比较值列表中有NULL时，不能判断大小，返回值为NULL。

#### 3.4.4 BETWEEN AND运算符

 	BETWEEN运算符使用的格式通常为 

​		SELECT D 

​		FROM TABLE 

​		WHERE C BETWEEN A AND B

 	`WHERE后面的条件是:  C 是否属于A 到 B 这个范围内（包含A 和 B）`  在该范围就是1 ，不在就是0

```SQL
SELECT 1 BETWEEN 0 AND 1, 10 BETWEEN 11 AND 12, 'b' BETWEEN 'a' AND 'c',
1 BETWEEN 1 AND NULL,NULL BETWEEN 1 AND NULL;

# 结果 1 0 1 NULL NULL 
# 【注】 NULL参与运算结果为NULL

# 查询salary在2500到3500的员工信息
# 1
SELECT last_name, salary
FROM employees
WHERE salary BETWEEN 2500 AND 3500;
# 2
SELECT last_name, salary
FROM employees
WHERE salary >= 2500 AND salary <= 3500;

#  查询salary不在2500到3500的员工信息
SELECT last_name, salary
FROM employees
WHERE salary NOT BETWEEN 2500 AND 3500;

# 【注】BETWEEN AND主要是某一个范围的值
```

#### 3.4.5 IN和NOT IN运算符

​	`IN运算符`用于判断给定的值是否是IN列表中的一个值，如果是则返回1，否则返回0。

​	如果`给定的值为NULL`，或者`IN列表中存在NULL`，则`结果为NULL`。

​	`NOT IN运算`符用于判断给定的值是否不是IN列表中的一个值，如果不是IN列表中的一个值，则返回1，否则返回0

```sql
SELECT 2 IN(1,2,3,4,5),3 NOT IN(1,2,3,4),
NULL IN(1,2,3,NULL),NULL NOT IN(1,2,3)
FROM DUAL;
# 结果 1 0 NULL NULL
```

#### 3.4.6 LIKE 运算符

​	`LIKE运算符`主要用来`匹配字符串`，通常用于`模糊匹配`，如果满足条件则返回1，否则返回0。

​	如果`给定的值`或者`匹配条件为NULL`，则返回`结果为NULL`。

​	与LIKE运算符结合使用的通配符：

​		`"%"：匹配0个或多个字符。`

​		`"_"：只能匹配一个字符。`

```sql
# 查询last_name 中 S 开头的
SELECT last_name 
FROM employees
WHERE last_name LIKE 'S%'；

# 查询 last_name 中包含 s 和 k字符的
SELECT last_name 
FROM employees
WHERE last_name LIKE '%S%k%' OR last_name LIKE '%k%s%';

# 查询 last_name 中包含第三个字符是 s 的
SELECT last_name 
FROM employees
WHERE last_name LIKE '__S%'；
```

#### 3.4.7 ESCAPE运算符

​	如果使用\表示转义，要省略ESCAPE。如果不是\，则要加上ESCAPE。

```sql
# 通过 ESCAPE 将字符 $ 作为转义字符

SELECT job_id
FROM jobs
WHERE job_id LIKE 'IT$_%' escape '$';
```

#### 3.4.8 REGEXP运算符

​	`REGEXP运算符`用来`匹配字符串`，语法格式为： expr REGEXP 匹配条件 。如果`expr满足匹配条件`，返回1，反之返回0，expr为null结果为null

​	（1）`'^'`匹配以`该字符后面的字符开头的字符串。`
​	（2）`'$'`匹配以`该字符前面的字符结尾的字符串。`
​	（3）`'.'`匹配`任何一个单字符。`
​	（4）`'[...]'`匹配在`方括号内的任何字符`。例如，“[abc]”匹配“a”或“b”或“c”。为了命名字符的范围，使用一
​		个'-'。'[a-z] [A-Z]'匹配任何大小写字母，而'[0-9]'匹配任何数字。
​	（5）`' * '`匹配`零个或多个在它前面的字符`。例如，'x *'匹配任何数量的'x'字符，'[0-9] * '匹配任何数量的数字，
​		而'*'匹配任何数量的任何字符。

## 4.逻辑运算符

​	`逻辑运算符`主要用来`判断表达式的真假`，在MySQL中，`逻辑运算符的返回结果为1、0或者NULL。`

![iAOtF.png](https://i.328888.xyz/img/2022/11/30/iAOtF.png)

### 4.1 逻辑非运算符

​	`逻辑非（ NOT 或 ! ）运算符`表示当给定的值为0时返回1；当给定的值为非0值时返回0；当给定的值为NULL时，返回NULL。

```sql
 SELECT NOT 1, NOT 0, NOT(1+1), NOT !1, NOT NULL;
 
 # 结果 0 1 0 1 null
```

### 4.2 逻辑与 和 逻辑或运算符

​	`逻辑与（AND或&&）运算符`是当给定的所有值均为非0值，并且都不为NULL时，返回1；当给定的一个值或者多个值为0时则返回0；否则返回NULL。

​	【注】 && 或 AND `全 1 为 1`，`有 0 为 0    ( 0 和 NULL结果也为 0 ) `，

​			`NULL和 NULL 结果为 NULL (1 和 NULL的结果为 NULL)`

​	

```sql
 SELECT 1 AND 1, 1 AND 0, 0 AND 0,
 1 AND NULL,
 0 AND NULL, 
 NULL AND NULL
 FROM DUAL;
 
 # 结果 1 0 0 NULL 0 NULL
```



​	`逻辑或（OR或||）运算符`是当给定的值都不为NULL，并且任何一个值为非0值时，则返回1，否则返回0；

​	当一个值为NULL，并且另一个值为非0值时，返回1，否则返回NULL；当两个值都为NULL时，返回NULL。

​	【注】 OR 或 || `全 0 为 0` ，`有 1 为 1 （1 和 NULL结果也为 1） ` 

​			`NULL和 NULL 结果为 NULL (0 和 NULL的结果为 NULL)`

```sql
 SELECT 0 OR 0,1 OR 0, 1 OR 1,
 1 OR NULL,
 0 OR NULL,
 NULL OR NULL
 FROM DUAL;

# 结果 0 1 1 1 NULL NULL
```

> OR可以和AND一起使用，但是在使用时要注意两者的优先级，由于`AND的优先级高于OR`，因此先对AND两边的操作数进行操作，再与OR中的操作数结合。

### 4.3 逻辑异或运算符

​	`逻辑异或（XOR）运算符`是当给定的值中任意一个值为NULL时，则返回NULL；

​	如果两个非NULL的值都是0或者都不等于0时，则返回0；如果一个值为0，另一个值不为0时，则返回1。

​	【注】XOR  `运算符两边 全 0 或 全 1时结果为0 `，`两边一个 0，一个 1 时结果才为1` `有一个为NULL结果为NULL`

```sql
SELECT 
1 XOR 1, 0 XOR 0, 
1 XOR 0,0 XOR 1,
NULL XOR 1, NULL XOR 0,NULL XOR NULL
FROM DUAL;

# 结果 0 0 1 1 NULL NULL NULL
```

## 5.位运算符

​	`位运算符`是在`二进制数`上进行计算的运算符。`位运算符会先将操作数变成二进制数`，然后进行位运算，最后将`计算结果从二进制变回十进制数。`

![iAxvN.png](https://i.328888.xyz/img/2022/11/30/iAxvN.png)

### 5.1 按位与 和 按位或 运算符

​	`按位与（&）运算符`将给定`值对应的二进制数逐位进行逻辑与运算`。当给定值对应的二进制位的`数值都为1`时，则`该位返回1`，否则`返回0`。

​	【注】`全 1 为 1`，`有 0 为 0  `

​	`按位或（|）运算符`将给定的`值对应的二进制数逐位进行逻辑或运算`。当给定值对应的二进制位的`数值有一个或两个为1`时，则该位`返回1`否则返回0。 	

​	【注】`全 0 为 0 ，有 1 为 1`

### 5.2 按位异或 运算符

​	`按位异或（^）运算符`将给定的`值对应的二进制数逐位进行逻辑异或运算`。当给定值对应的二进制位的`数值有一个0另一个为1`时，则该位`返回1`，否则返回0。 	

​	【注】`全 0 全 1 为 0，一个 0 一个 1 为 1`

### 5.3 按位取反 运算符

​	`按位取反（~）运算符`将给定的值的二进制数逐位进行取反操作，即将`1变为0，将0变为1。`

### 5.4 按位右移和按位左移 运算符

​	`按位右移（>>）运算符`将给定的`值的二进制数`的`所有位右移指定的位数`。右移指定的位数后，`右边低位的数值被移出并丢弃`，`左边高位空出的位置用0补齐`。

​	`按位左移（<<）运算符`将给定的`值的二进制数的所有位左移指定的位数`。左移指定的位数后，`左边高位的数值被移出并丢弃`，`右边低位空出的位置用0补齐`。



# 第五章、排序与分页

## 1.排序

### 1.1 排序规则

​	在MySQL中，使用 `ORDER BY `关键字来进行排序

​	语法格式： `ORDER BY ...  ASC  或 DESC`

​		   ASC (ascend):升序   默认

​		   DESC (descend):降序 

​	【注】ORDER BY 一般用在SELECT 语句的结尾 LIMIT语句的前面

### 1.2 单列排序和多列排序

​	`单列排序 ORDER BY 关键字后面只有一个字段名`

```sql
# 单列排序
# 根据员工薪水升序排序
SELECT employee_id,salary 
FROM employees
ORDER BY salary ASC; -- ASC 可以省略
# 根据员工薪水降序排序
SELECT employee_id,salary 
FROM employees
ORDER BY salary DESC;
```

​	在对多列进行排序的时候，`首先排序的第一列必须有相同的列值，才会对第二列进行排序。`

​	`如果第一列数据中所有值都是唯一的，将不再对第二列进行排序。`

```sql
#  下面排序方法，只会对第一列排序，因为employee_id 是唯一值
SELECT employee_id,salary 
FROM employees
ORDER BY employee_id,salary DESC;

#  下面排序方法，会先根据部门号进行升序排序，然后再排序好的部门里面对员工薪水进行降序排序
SELECT employee_id,salary,department_id
FROM employees
ORDER BY department_id,salary DESC;
```

## 2.分页

### 2.1 分页规则

​	在MySQL中使用 `LIMIT` 关键字来实现分页

​	MySQL5.7语法格式： ` LIMIT 位置偏移量 每页显示行数 `      

​	MySQL8.0语法格式： `LIMIT 每页显示行数 OFFSET 位置偏移量  `

​	【注】` LIMIT 子句必须放在整个SELECT语句的最后！`，对表进行过滤，排序后再进行分页

```sql
# 显示employees表前10条记录
SELECT * FROM employees LIMIT 0 10;
SELECT * FROM employees LIMIT 10 OFFSET 0;

# 显示employees表11 - 20条记录
SELECT * FROM employees LIMIT 10 20;
SELECT * FROM employees LIMIT 20 OFFSET 10;

# 显示employees表第4-9 条记录
SELECT * FROM employees LIMIT 3 6;
```

​	【结论】 分页显示公式：**LIMIT（当前页数-1）*每页条数，每页条数**

​			     **LIMIT 每页条数 offset （当前页数-1）*每页条数**

分页显示的优点：	

​	约束返回结果的数量可以 减少数据表的网络传输量 ，也可以提升查询效率 。

​	如果我们知道返回结果只有1 条，就可以使用 LIMIT 1 ，告诉 SELECT 语句只需要返回一条记录即可。

​	这样的好处就是 SELECT 不需要扫描完整的表，只需要检索到一条符合条件的记录即可返回。

### 2.2 拓展

在不同的 DBMS 中使用的关键字可能不同。在 MySQL、PostgreSQL、MariaDB 和 SQLite 中使用 LIMIT 关键字，而且需要放到 SELECT 语句的最后面。

如果是 SQL Server 和 Access，需要使用 TOP 关键字，比如：

```sql
SELECT TOP 5 name, hp_max FROM heros ORDER BY hp_max DESC
```

如果是 DB2，使用 FETCH FIRST 5 ROWS ONLY 这样的关键字：

```sql
SELECT name, hp_max FROM heros ORDER BY hp_max DESC FETCH FIRST 5 ROWS ONLY
```

如果是 Oracle，你需要基于 ROWNUM 来统计行数：

```sql
SELECT rownum,last_name,salary FROM employees WHERE rownum < 5 ORDER BY salary DESC;
```

需要说明的是，这条语句是先取出来前 5 条数据行，然后再按照 hp_max 从高到低的顺序进行排序。但这样产生的结果和上述方法的并不一样。我会在后面讲到子查询，你可以使用

```sql
SELECT rownum, last_name,salary
FROM (
    SELECT last_name,salary
    FROM employees
    ORDER BY salary DESC)
WHERE rownum < 10;
```



# 第六章、多表查询

## 6.1 基本概念

> **多表查询**，也称为关联查询，是指两个或多个表进行关联查询数据。
>
> **前提条件**：两个或多个表之间有关联关系（一对一，一对多，多对多），它们之间一定是有关联字段，这个
> 关联字段可能建立了外键，也可能没有建立外键。比如：员工表和部门表，这两个表依靠“部门编号”进
> 行关联。

`基本语法 ` :       <span style="color:#CC0000;font-size:20px;font-weight:bold"> select * from 表1，表2;  </span>



现有两张表

![j9MVw.png](https://i.328888.xyz/2023/01/29/j9MVw.png)

查询所有员工所在的部门名称：

```sql
SELECT last_name, department_name
FROM employees, departments;
```

上述查询的结果会有 ：2889 rows in set (0.01 sec)  而我们总共才107名员工

产生错误的原因是：笛卡尔积，将两张表的所有数据进行组合得到2889条数据。

## 6.2 笛卡尔积（或交叉连接）的理解

> 笛卡尔乘积是一个数学运算。假设我有两个集合 X 和 Y，那么 X 和 Y 的笛卡尔积就是 X 和 Y 的所有可能组合。

[![jJ4j8.md.png](https://i.328888.xyz/2023/01/29/jJ4j8.md.png)](https://imgloc.com/i/jJ4j8)

> SQL92中，笛卡尔积也称为 交叉连接 ，英文是 **CROSS JOIN** 。在 SQL99 中也是使用 CROSS JOIN表示交叉连接。它的作用就是可以把任意表进行连接，即使这两张表不相关。

**笛卡尔积错误的条件：**

 - 省略多个表的连接条件（或关联条件）
 - 连接条件（或关联条件）无效
 - 所有表中的所有行互相连接

**消除笛卡尔积：**

​	可以在 WHERE子句中 加入有效的连接条件。

​	例如：<span style="color:#CC0000;font-size:20px;font-weight:bold"> select * from 表1,表2 where 表1.外键 = 表2.主键</span>

​	则上述查询所有员工所在的部门名称：

```sql
SELECT last_name, department_name
FROM employees, departments
WHERE employees.department_id = departments.department_id;
```

【注】**在表中有相同列时，在列名之前加上表名前缀。**

## 6.3 多表查询的分类

### 6.3.1 等值连接

> **等值连接：**通过笛卡尔积在WHERE子句中使用 ”=“ 的比较运算符将两张表联系起来，并去除**无用的行**来消除笛卡尔积
>
> ​	`但是其查询结果中会列出被连接表中所有的列（字段）包括重复的列。`

[![jJeMp.md.png](https://i.328888.xyz/2023/01/29/jJeMp.md.png)](https://imgloc.com/i/jJeMp)

上面两张表进行等值连接：

```sql
# SQL92写法
SELECT employees.employee_id, employees.last_name,
employees.department_id, departments.department_id,
departments.location_id
FROM employees, departments
WHERE employees.department_id = departments.department_id;
```

```sql
# SQL99写法
SELECT employees.employee_id, employees.last_name,
employees.department_id, departments.department_id,
departments.location_id
FROM employees INNER JOIN departments 
ON employees.department_id = departments.department_id;
```



![jJGs3.png](https://i.328888.xyz/2023/01/29/jJGs3.png)

**拓展：**

​	（1）多个连接条件使用AND符

​	（2）区分重复的列名   

​		多个表中有相同列时，必须在列名之前加上表名前缀。

​	（3）表的别名

​		使用别名可以简化查询。

​		列名前使用表名前缀可以提高查询效率	

```sql
SELECT e.employee_id, e.last_name, e.department_id,
d.department_id, d.location_id
FROM employees e , departments d
WHERE e.department_id = d.department_id;
```

​	（4）连接多个表

​		连接 n个表,至少需要n-1个连接条件。比如，连接三个表，至少需要两个连接条件。

[![jJ585.md.png](https://i.328888.xyz/2023/01/29/jJ585.md.png)](https://imgloc.com/i/jJ585)

### 6.3.2 自连接

> **自连接**：将两张物理上相同的表 通过取别名的方式 进行连接查询。

![jJayX.png](https://i.328888.xyz/2023/01/29/jJayX.png)

**上面两张物理上相同的表来进行自连接查询： 查询每一个员工的管理员名字**

```sql
# SQL92写法
SELECT CONCAT(worker.last_name ,' works for '
, manager.last_name)
FROM employees worker, employees manager
WHERE worker.manager_id = manager.employee_id ;

#SQL99写法
SELECT CONCAT(worker.last_name ,' works for '
, manager.last_name)
FROM employees worker INNER JOIN employees manager
ON worker.manager_id =  manager.employee_id ;

```

![1674975704633](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1674975704633.png)

### 6.3.3 自然连接

> **自然连接**：是一种**特殊的等值连接**。我们知道等值连接会将所有列都显示出来，而自然连接会将等值连接的结果去掉重复的列
>
> ​	SQL99 在 SQL92 的基础上提供了一些特殊语法，比如 **NATURAL JOIN** 用来表示自然连接。我们可以把
>
> ​	自然连接理解为 SQL92 中的等值连接。它会帮你自动查询两张连接表中 所有相同的字段 ，然后进行 等值连接 。

```sql
# SQL92写法
SELECT employee_id,last_name,department_name
FROM employees e INNER JOIN departments d
ON e.`department_id` = d.`department_id`
AND e.`manager_id` = d.`manager_id`;

# SQL99写法
SELECT employee_id,last_name,department_name
FROM employees e NATURAL JOIN departments d;
```

### 6.3.4 内连接

> **内连接**：合并具有同一列的两个以上的表的行, 结果集中不包含一个表与另一个表不匹配的行。【消除笛卡尔积后的结果】
>
> ​	上面的**等值连接，自连接和自然连接都是内连接的一种。**
>
> 关键字： `INNER JOIN`

**语法：**

​	隐式内连接   select 查询列表 from 表1,表2 where 条件;

​	显示内连接   select 字段列表 from 表1 [inner] join 表2 on 连接条件 WHERE 其他筛选条件;

### 6.3.5 外连接

> **外连接**： 两个表在连接过程中除了返回满足连接条件的行以外还返回左（或右）表中不满足条件的行 ，这种连接称为左（或右） 外连接。没有匹配的行	时, 结果表中相应的列为空(NULL)。
>
> 例如：新员工还没有分配部门，则新员工的部门id为null
>
> ​	使用内连接时查询出的数据就不会包含新员工，这样会造成数据缺失
>
> ​	而我们可以通过外连接来查询出所有员工的数据，则不满足条件的列为null
>
> 关键字 `OUTER JOIN`
>
> **外连接包含 左外连接（left [outer] join），右外连接(right [outer] join)，完全外连接(full [outer] join)**    `outer可省略`

**左外连接**

​	连接条件中左边的表也称为 **主表** ，右边的表称为 **从表**。

​	语法：

```sql
# 可以查询到A表中的所有数据
SELECT 字段列表
FROM A表 LEFT JOIN B表
ON 关联条件
WHERE 等其他子句;
```

**右外连接**

​	连接条件中右边的表也称为 **主表** ，左边的表称为 **从表**。

​	语法:

```sql
# 可以查询到B表中的所有数据
SELECT 字段列表
FROM A表 RIGHT JOIN B表
ON 关联条件
WHERE 等其他子句;
```

> 【注】需要注意的是，LEFT JOIN 和 RIGHT JOIN 只存在于 SQL99 及以后的标准中，在 SQL92 中不存在，只能用 (+) 表示。

**完全外连接/满外连接**

​	返回两个连接中所有的记录数据，是**左外连接和右外连接的并集。**

​	语法：

```sql
SELECT 字段列表
FROM A表 FULL JOIN B表
ON 关联条件
WHERE 等其他子句;
```

​	满外连接的结果 = 左右表匹配的数据 + 左表没有匹配到的数据 + 右表没有匹配到的数据。

​	SQL99是支持满外连接的。使用FULL JOIN 或 FULL OUTER JOIN来实现。

​	需要注意的是，**MySQL不支持FULL JOIN**，但是可以用 **LEFT JOIN UNION RIGHT JOIN**代替。

## 6.4 UNION的使用

> **UNION:**合并查询结果 利用UNION关键字，可以给出多条SELECT语句，并将它们的结果组合成单个结果集。
>
> ​      合并时，两个表对应的**列数**和**数据类型必须相同**，并且相互对应。各个SELECT语句之间使用UNION或UNIONALL关键字分隔。
>
> 例如：上面的满外连接 MySQL中不支持FULL JOIN 可以使用UNION

语法：

```sql
SELECT column,... FROM table1
UNION [ALL]
SELECT column,... FROM table2
```

<span style="color:#CC0000;font-size:20px;font-weight:bold"> UNION操作符返回两个查询的结果集的并集，去除重复记录。</span>

<a href='https://postimages.org/' target='_blank'><img src='https://i.postimg.cc/dQzJRk8s/1674994586920.png' border='0' alt='1674994586920'/></a>

<span style="color:#CC0000;font-size:20px;font-weight:bold"> UNION ALL操作符返回两个查询的结果集的并集。对于两个结果集的重复部分，不去重。</span>



[![1674994797469.png](https://i.postimg.cc/mr0mpsVH/1674994797469.png)](https://postimg.cc/sB4P1bkj)

> 注意：执行UNION ALL语句时所需要的资源比UNION语句少。如果明确知道合并数据后的结果数据不存在重复数据，或者不需要去除重复的数据，则尽量使用UNION ALL语句，以提高数据查询的效率。



## 6.5 7种JOIN的实现

[![1674995016146b7204dafc4dd1854.md.png](https://img.picgo.net/2023/01/29/1674995016146b7204dafc4dd1854.md.png)](https://www.picgo.net/image/dfxT2)

```sql
#中间 内连接
SELECT employee_id,last_name,department_name
FROM employees e JOIN departments d
ON e.`department_id` = d.`department_id`;

#左上 左外连接
SELECT employee_id,last_name,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`;

#右上 右外连接
SELECT employee_id,last_name,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`;

#左中 左外连接去除null
SELECT employee_id,last_name,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL;

#右中 右外连接去除null
SELECT employee_id,last_name,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL;

#左下 满外连接
# 左中图 + 右上图  # mysql中的写法
SELECT employee_id,last_name,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL
UNION ALL                                          #没有去重操作，效率高
SELECT employee_id,last_name,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`;

SELECT employee_id,last_name,department_name
FROM employees e FULL JOIN departments d
ON e.`department_id` = d.`department_id`;


#右下 
#左中图 + 右中图
SELECT employee_id,last_name,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL
UNION ALL
SELECT employee_id,last_name,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL;
```





# 第七章、单行函数  

## 1.函数的理解

### 1.1 什么是函数？

函数在计算机语言的使用中贯穿始终，函数的作用是什么呢？

​	它可以把我们经常使用的代码封装起来，需要的时候直接调用即可。这样既`提高了代码效率`，又`提高了可维护性`。

​	在 `SQL` 中我们也可以使用函数`对检索出来的数据进行函数操作`。使用这些函数，可以极大地`提高用户对数据库的管理效率`。

![iYCaN.png](https://i.328888.xyz/img/2022/12/03/iYCaN.png)

从函数定义的角度出发，我们可以将函数分成`内置函数`和`自定义函数`。

在 SQL 语言中，同样也包括了内置函数和自定义函数。`内置函数是系统内置的通用函数`，而`自定义函数是我们根据自己的需要编写的`

### 1.2 不同DBMS函数的差异

​	我们在使用 SQL 语言的时候，不是直接和这门语言打交道，而是通过它使用不同的数据库软件，即 DBMS。<u>DBMS 之间的差异性很大，远大于同一个语言不同版本之间的差异。实际上，只有很少的函数是被 DBMS 同时支持的。比如，大多数 DBMS 使用（||）或者（+）来做拼接符，而在 MySQL 中的字符串拼接函数为concat()</u>。

​	大部分 DBMS 会有自己特定的函数，这就意味着`采用 SQL 函数`的`代码可移植性是很差的`，因此在使用函数的时候需要特别注意。

###  1.3 MySQL的内置函数及分类

​	MySQL提供了丰富的内置函数，这些函数使得数据的维护与管理更加方便，能够更好地提供数据的分析与统计功能，在一定程度上提高了开发人员进行数

据分析与统计的效率。

​	MySQL提供的内置函数从`实现的功能角度`可以分为数值函数、字符串函数、日期和时间函数、流程控制函数、加密与解密函数、获取MySQL信息函数、聚合函数等。这里，我将这些丰富的内置函数再分为两类：<span style="color:#DC143C;font-size:18px;font-weight:bold">`单行函数`、`聚合函数（或分组函数）`</span>

![iYbAq.png](https://i.328888.xyz/img/2022/12/03/iYbAq.png)

`单行函数`

- 操作数据对象
- 接受参数返回一个结果
- **只对一行进行变换**
- **每行返回一个结果**
- 可以嵌套
- 参数可以是一列或一个值

## 2.数值函数

### 2.1 基本数值函数

![iYNZa.png](https://i.328888.xyz/img/2022/12/03/iYNZa.png)

```sql
# 绝对值 Absolute
SELECT ABS(-123),ABS(32),ABS(0),ABS(-0) FROM DUAL;
# 结果 123 32 0 0

# 符号 sign
SELECT SIGN(0),SIGN(123),SIGN(-123) FROM DUAL;
# 结果 0 1 -1

# Π值
SELECT PI() FROM DUAL;
# 结果 3.141593

# 向上取整CEIL和向下取整FLOOR
SELECT CEIL(10.00),CEIL(10.01),CEIL(-10.01),CEIL(10.50)
FLOOR(10.00),FLOOR(10.01),FLOOR(-10.01).FLOOR(10.50)
FROM DUAL;
# 结果 10 11 -10 11
#      10 10 -11 10

# 求集合中最小值LEAST和最大值GREATEST
SELECT LEAST(0,1,2,3,5),LEAST(NULL,1,2,3,4),
GREATEST(0,1,2,3,4,5),GREATEST(NULL,1,2,3,4)
FROM DUAL;
# 结果 0 NULL 5 NULL

# 取随机数RAND 取0-1的随机数
SELECT RAND(),RAND(),
RAND(1),RAND(1)
FROM DUAL;

# 案例 取0-10的随机整数
SELECT TRUNCATE(RAND()*10,0),
FROM DUAL;

# 前两次结果不一样，后两次结果一样

# 四舍五入 ROUND() ROUND(x,y) 四舍五入保留y位小数（从y+1位开始四舍五入）
SELECT ROUND(1.44),ROUND(1.54),
ROUND(1.44,1),ROUND(1.55,1)
FROM DUAL;
# 结果 1 2 1.4 1.6 

# 返回数字x截断为y位小数的结果 TRUNCATE(x,y)
SELECT TRUNCATE(1.44,0),TRUNCATE(1.44,1),TRUNCATE(1.44,2)
FROM DUAL;
# 结果 1 1.4 1.44

# 取余 MOD(x,y) 求x除y后的余数
SELECT MOD(10,3), 10 MOD 3, 10 % 3
FROM DUAL;
```

### 2.2 角度°与弧度rad的互换

[![iYJiJ.png](https://i.328888.xyz/img/2022/12/03/iYJiJ.png)](https://imgloc.com/i/iYJiJ)
$$
1° = Π / 180 (rad)  |  1 rad = 180 / Π（°） |   360° = 2Π （rad）
$$

```sql
SELECT RADIANS(30),RADIANS(60),RADIANS(90),DEGREES(2*PI()),DEGREES(RADIANS(90))
FROM DUAL;
```

### 2.3 三角函数

​	[![iYM1o.png](https://i.328888.xyz/img/2022/12/03/iYM1o.png)](https://imgloc.com/i/iYM1o)

ATAN2(M,N)函数返回两个参数的反正切值。 

与ATAN(X)函数相比，ATAN2(M,N)需要两个参数，例如有两个点point(x1,y1)和point(x2,y2)，使用ATAN(X)函数计算反正切值为ATAN((y2-y1)/(x2-x1))，

使用ATAN2(M,N)计算反正切值则为ATAN2(y2-y1,x2-x1)。

由使用方式可以看出，当x2-x1等于0时，ATAN(X)函数会报错，而ATAN2(M,N)函数则仍然可以计算

```sql
SELECT SIN(RADIANS(30)),DEGREES(ASIN(1)),TAN(RADIANS(45)),DEGREES(ATAN(1)),DEGREES(ATAN2(1,1))
FROM DUAL;
```

### 2.4 指数与对数

![iYagV.png](https://i.328888.xyz/img/2022/12/03/iYagV.png)

```sql
mysql> SELECT POW(2,5),POWER(2,4),EXP(2),LN(10),LOG10(10),LOG2(4)
-> FROM DUAL;
+----------+------------+------------------+-------------------+-----------+---------+
| POW(2,5) | POWER(2,4) | EXP(2) | LN(10) | LOG10(10) | LOG2(4) |
+----------+------------+------------------+-------------------+-----------+---------+
| 32 | 16 | 7.38905609893065 | 2.302585092994046 | 1 | 2 |
+----------+------------+------------------+-------------------+-----------+---------+
1 row in set (0.00 sec)
```

### 2.5 进制间的转换

![iYq3q.png](https://i.328888.xyz/img/2022/12/03/iYq3q.png)

```sql
mysql> SELECT BIN(10),HEX(10),OCT(10),CONV(10,2,8)
-> FROM DUAL;
+---------+---------+---------+--------------+
| BIN(10) | HEX(10) | OCT(10) | CONV(10,2,8) |
+---------+---------+---------+--------------+
| 1010 | A | 12 | 2 |
+---------+---------+---------+--------------+
1 row in set (0.00 sec)

```

## 3.字符串函数

| 函数                              | 用法                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| ASCII(S)                          | 返回字符串S中的第一个字符的ASCII码值                         |
| CHAR_LENGTH(s)                    | 返回字符串s的字符数。作用与CHARACTER_LENGTH(s)相同           |
| LENGTH(s)                         | 返回字符串s的字节数，和字符集有关                            |
| CONCAT(s1,s2,......,sn)           | 连接s1,s2,......,sn为一个字符串                              |
| CONCAT_WS(x, s1,s2,......,sn)     | 同CONCAT(s1,s2,...)函数，但是每个字符串之间要加上x           |
| INSERT(str, idx, len, replacestr) | 将字符串str从第idx位置开始，len个字符长的子串替换为字符串replacestr |
| REPLACE(str, a, b)                | 用字符串b替换字符串str中所有出现的字符串a                    |
| UPPER(s) 或 UCASE(s)              | 将字符串s的所有字母转成大写字母                              |
| LOWER(s) 或LCASE(s)               | 将字符串s的所有字母转成小写字母                              |
| LEFT(str,n)                       | 返回字符串str最左边的n个字符                                 |
| RIGHT(str,n)                      | 返回字符串str最右边的n个字符                                 |
| LPAD(str, len, pad)               | 用字符串pad对str最左边进行填充，直到str的长度为len个字符     |
| RPAD(str ,len, pad)               | 用字符串pad对str最右边进行填充，直到str的长度为len个字符     |
| LTRIM(s)                          | 去掉字符串s左侧的空格                                        |
| RTRIM(s)                          | 去掉字符串s右侧的空格                                        |
| TRIM(s)                           | 去掉字符串s开始与结尾的空格                                  |
| TRIM(s1 FROM s)                   | 去掉字符串s开始与结尾的s1                                    |
| TRIM(LEADING s1 FROM s)           | 去掉字符串s开始处的s1                                        |
| TRIM(TRAILING s1 FROM s)          | 去掉字符串s结尾处的s1                                        |
| REPEAT(str, n)                    | 返回str重复n次的结果                                         |
| SPACE(n)                          | 返回n个空格                                                  |
| STRCMP(s1,s2)                     | 比较字符串s1,s2的ASCII码值的大小                             |
| SUBSTR(s,index,len)               | 返回从字符串s的index位置其len个字符，作用与SUBSTRING(s,n,len)、MID(s,n,len)相同 |
| LOCATE(substr,str)                | 返回字符串substr在字符串str中首次出现的位置，作用于POSITION(substr IN str)、INSTR(str,substr)相同。未找到，返回0 |
| ELT(m,s1,s2,…,sn)                 | 返回指定位置的字符串，如果m=1，则返回s1，如果m=2，则返回s2，如果m=n，则返回sn |
| FIELD(s,s1,s2,…,sn)               | 返回字符串s在字符串列表中第一次出现的位置                    |
| FIND_IN_SET(s1,s2)                | 返回字符串s1在字符串s2中出现的位置。其中，字符串s2是一个以逗号分隔的字符串 |
| REVERSE(s)                        | 返回s反转后的字符串                                          |
| NULLIF(value1,value2)             | 比较两个字符串，如果value1与value2相等，则返回NULL，否则返回value1 |

【注意】<span style="color:#DC143C;font-size:18px;font-weight:bold">MySQL中，字符串的位置是从1开始的。</span>

## 4.日期和时间函数

### 4.1 获取时间和日期

| 函数                                                         | 用法                           |
| ------------------------------------------------------------ | ------------------------------ |
| `CURDATE()` ，CURRENT_DATE()                                 | 返回当前日期，只包含年、月、日 |
| `CURTIME()` ， CURRENT_TIME()                                | 返回当前时间，只包含时、分、秒 |
| `NOW() `/ SYSDATE() / CURRENT_TIMESTAMP() / LOCALTIME() / LOCALTIMESTAMP() | 返回当前系统日期和时间         |
| UTC_DATE()                                                   | 返回UTC（世界标准时间）日期    |
| UTC_TIME()                                                   | 返回UTC（世界标准时间）时间    |

```sql
SELECT CURDATE(),CURTIME(),NOW(),SYSDATE()+0,SYSDATE,UTC_DATE(),UTC_DATE()+0,UTC_TIME(),UTC_TIME()+0
FROM DUAL;
# 结果 2022-12-03 15:07:50 2022-12-03 15:07:50 20221203151056 2022-12-03 15:10:56 2022-12-03 20221203 07:10:56 71056
# 【注】 SYSDATE()+0，UTC_DATE()+0，UTC_TIME()+0 会将时间格式从XXXX-XX-XX  转为XXXXXXXX
```

### 4.2 日期与时间戳的转换

| 函数                     | 用法                                                         |
| ------------------------ | ------------------------------------------------------------ |
| UNIX_TIMESTAMP()         | 以UNIX时间戳的形式返回当前时间。SELECT UNIX_TIMESTAMP() ->1634348884 |
| UNIX_TIMESTAMP(date)     | 将时间date以UNIX时间戳的形式返回。                           |
| FROM_UNIXTIME(timestamp) | 将UNIX时间戳的时间转换为普通格式的时间                       |

```sql
SELECT UNIX_TIMESTAMP(),
UNIX_TIMESTAMP(CURDATE()),
UNIX_TIMESTAMP(NOW()),
FROM_UNIXTIME(UNIX_TIMESTAMP(NOW()))
FROM DUAL;
# #################################################
mysql> SELECT UNIX_TIMESTAMP(now());
+-----------------------+
| UNIX_TIMESTAMP(now()) |
+-----------------------+
|            1576380910 |
+-----------------------+
1 row in set (0.01 sec)
# #################################################
mysql> SELECT UNIX_TIMESTAMP('2011-11-11 11:11:11')
+---------------------------------------+
| UNIX_TIMESTAMP('2011-11-11 11:11:11') |
+---------------------------------------+
|                            1320981071 |
+---------------------------------------+
1 row in set (0.00 sec)
# #################################################
mysql> SELECT FROM_UNIXTIME(1576380910);
+---------------------------+
| FROM_UNIXTIME(1576380910) |
+---------------------------+
| 2019-12-15 11:35:10       |
+---------------------------+
1 row in set (0.00 sec)
```

###  4.3 获取月份、星期、星期数、天数等函数

| 函数                                       | 用法                                            |
| ------------------------------------------ | ----------------------------------------------- |
| `YEAR(date) / MONTH(date) / DAY(date)`     | 返回具体的日期值 年，月，日                     |
| `HOUR(time) / MINUTE(time) / SECOND(time)` | 返回具体的时间值 时，分，秒                     |
| MONTHNAME(date)                            | 返回月份：January，...                          |
| DAYNAME(date)                              | 返回星期几：MONDAY，TUESDAY.....SUNDAY          |
| `WEEKDAY(date)`                            | 返回周几，注意，周1是0，周2是1，。。。周日是6   |
| QUARTER(date)                              | 返回日期对应的季度，范围为1～4                  |
| WEEK(date) ， WEEKOFYEAR(date)             | 返回一年中的第几周                              |
| DAYOFYEAR(date)                            | 返回日期是一年中的第几天                        |
| DAYOFMONTH(date)                           | 返回日期位于所在月份的第几天                    |
| `DAYOFWEEK(date)`         dayofweek        | 返回周几，注意：周日是1，周一是2，。。。周六是7 |

```sql
SELECT YEAR(CURDATE()),MONTH(CURDATE()),DAY(CURDATE()),
HOUR(CURTIME()),MINUTE(NOW()),SECOND(SYSDATE())
FROM DUAL;
# 结果 2022	12	3	15	47	43

SELECT MONTHNAME(NOW()),DAYNAME(NOW()),WEEKDAY(NOW()),
QUARTER(CURDATE()),WEEK(CURDATE()),DAYOFYEAR(NOW()),
DAYOFMONTH(NOW()),DAYOFWEEK(NOW())
FROM DUAL;
# 结果 December	Saturday	5	4	48	337	3
```

### 4.4 日期的操作函数

| 函数                               | 用法                                       |
| ---------------------------------- | ------------------------------------------ |
| EXTRACT(type FROM date)    extract | 返回指定日期中特定的部分，type指定返回的值 |

`EXTRACT(type FROM date)函数中type的取值与含义：`

![iqecb.png](https://i.328888.xyz/img/2022/12/03/iqecb.png)

```sql
SELECT EXTRACT(MINUTE FROM NOW()),EXTRACT( WEEK FROM NOW()),
EXTRACT( QUARTER FROM NOW()),EXTRACT( MINUTE_SECOND FROM NOW())
FROM DUAL;
# 结果 54	48	4	5404
```

###  4.5 时间和秒钟转换的函数

（从当天的00：00：00开始计算）

| 函数                 | 用法                                                         |
| -------------------- | ------------------------------------------------------------ |
| TIME_TO_SEC(time)    | 将 time 转化为秒并返回结果值。转化的公式为：`小时*3600+分钟*60+秒` |
| SEC_TO_TIME(seconds) | 将 seconds 描述转化为包含小时、分钟和秒的时间                |

```sql
mysql> SELECT TIME_TO_SEC(NOW());
+--------------------+
| TIME_TO_SEC(NOW()) |
+--------------------+
|               78774 |
+--------------------+
1 row in set (0.00 sec)
# ###############################################
mysql> SELECT SEC_TO_TIME(78774);
+--------------------+
| SEC_TO_TIME(78774) |
+--------------------+
| 21:52:54            |
+--------------------+
1 row in set (0.12 sec)
```

###  4.6 计算日期和时间的函数

第一组：

| 函数                                                         | 用法                                           |
| ------------------------------------------------------------ | ---------------------------------------------- |
| `DATE_ADD(datetime, INTERVAL expr type)`，ADDDATE(date,INTERVAL expr type) | 返回与给定日期时间相差INTERVAL时间段的日期时间 |
| `DATE_SUB(date,INTERVAL expr type)`，SUBDATE(date,INTERVAL expr type) | 返回与date相差INTERVAL时间间隔的日期           |

type可取的值：

![A5SGp.png](https://i.328888.xyz/2022/12/22/A5SGp.png)

```sql
# DATE_ADD 是给定时间加上相差的值
# DATE_SUB 是给定时间减去相差的值

SELECT
DATE_ADD(NOW(),INTERVAL 1 HOUR) AS COL1,  # 返回与当前时间相差1小时的时间  
DATE_ADD(NOW(),INTERVAL '1_1' DAY_HOUR) AS COL2 # 返回与当前时间相差1天1小时的时间
DATE_SUB(NOW(),INTERVAL 1 HOUR) AS COL1,  # 返回与当前时间相差1小时的时间  
DATE_SUB(NOW(),INTERVAL '1_1' DAY_HOUR) AS COL2 # 返回与当前时间相差1天1小时的时间
FROM DUAL;
```

第二组：

| 函数                         | 用法                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| ADDTIME(time1,time2)         | 返回time1加上time2的时间。当time2为一个数字时，代表的是`秒`，可以为负数 |
| SUBTIME(time1,time2)         | 返回time1减去time2后的时间。当time2为一个数字时，代表的是`秒`，可以为负数 |
| DATEDIFF(date1,date2)        | 返回date1 - date2的日期间隔天数                              |
| TIMEDIFF(time1, time2)       | 返回time1 - time2的时间间隔                                  |
| FROM_DAYS(N)                 | 返回从0000年1月1日起，N天以后的日期                          |
| TO_DAYS(date)                | 返回日期date距离0000年1月1日的天数                           |
| LAST_DAY(date)               | 返回date所在月份的最后一天的日期                             |
| MAKEDATE(year,n)             | 针对给定年份与所在年份中的天数返回一个日期                   |
| MAKETIME(hour,minute,second) | 将给定的小时、分钟和秒组合成时间并返回                       |
| PERIOD_ADD(time,n)           | 返回time加上n后的时间                                        |

例子：查询7天内新增的用户数

```sql
SELECT COUNT(*) as num FROM new_user WHERE TO_DAYS(NOW()) - TO_DAYS(regist_time)<=7;
# 当前时间到0000年1月1日的天数 减去 regist_time到0000年1月1日 小于等于7

SELECT COUNT（*）as num FROM new_user WHERE DATEDIFF(NOW(),regist_time) <= 7;
```

### 4.7 日期的格式化与解析

| 函数                  | 用法                                       |
| --------------------- | ------------------------------------------ |
| DATE_FORMAT(date,fmt) | 按照字符串fmt格式化日期date值              |
| TIME_FORMAT(time,fmt) | 按照字符串fmt格式化时间time值              |
| STR_TO_DATE(str, fmt) | 按照字符串fmt对str进行解析，解析为一个日期 |

`非GET_FORMAT`函数中fmt参数常用的格式符：

| 格式符 | 说明                                                        | 格式符 | 说明                                                        |
| ------ | ----------------------------------------------------------- | ------ | ----------------------------------------------------------- |
| %Y     | 4位数字表示年份                                             | %y     | 表示两位数字表示年份                                        |
| %M     | 月名表示月份（January,....）                                | %m     | 两位数字表示月份（01,02,03。。。）                          |
| %b     | 缩写的月名（Jan.，Feb.，....）                              | %c     | 数字表示月份（1,2,3,...）                                   |
| %D     | 英文后缀表示月中的天数（1st,2nd,3rd,...）                   | %d     | 两位数字表示月中的天数(01,02...)                            |
| %e     | 数字形式表示月中的天数（1,2,3,4,5.....）                    |        |                                                             |
| %H     | 两位数字表示小数，24小时制（01,02..）                       | %h和%I | 两位数字表示小时，12小时制（01,02..）                       |
| %k     | 数字形式的小时，24小时制(1,2,3)                             | %l     | 数字形式表示小时，12小时制（1,2,3,4....）                   |
| %i     | 两位数字表示分钟（00,01,02）                                | %S和%s | 两位数字表示秒(00,01,02...)                                 |
| %W     | 一周中的星期名称（Sunday...）                               | %a     | 一周中的星期缩写（Sun.，Mon.,Tues.，..）                    |
| %w     | 以数字表示周中的天数(0=Sunday,1=Monday....)                 |        |                                                             |
| %j     | 以3位数字表示年中的天数(001,002...)                         | %U     | 以数字表示年中的第几周，（1,2,3。。）其中Sunday为周中第一天 |
| %u     | 以数字表示年中的第几周，（1,2,3。。）其中Monday为周中第一天 |        |                                                             |
| %T     | 24小时制                                                    | %r     | 12小时制                                                    |
| %p     | AM或PM                                                      | %%     | 表示%                                                       |

| 函数                              | 用法                     |
| --------------------------------- | ------------------------ |
| GET_FORMAT(date_type,format_type) | 返回日期字符串的显示格式 |

GET_FORMAT函数中date_type和format_type参数取值如下：

![A5vwv.png](https://i.328888.xyz/2022/12/22/A5vwv.png)

```sql
mysql> SELECT DATE_FORMAT(NOW(), '%H:%i:%s');
+--------------------------------+
| DATE_FORMAT(NOW(), '%H:%i:%s') |
+--------------------------------+
| 22:57:34                        |
+--------------------------------+
1 row in set (0.00 sec)
```



```sql
SELECT STR_TO_DATE('09/01/2009','%m/%d/%Y')
FROM DUAL;

SELECT STR_TO_DATE('20140422154706','%Y%m%d%H%i%s')
FROM DUAL;

SELECT STR_TO_DATE('2014-04-22 15:47:06','%Y-%m-%d %H:%i:%s')
FROM DUAL;
```



```mysql
mysql> SELECT GET_FORMAT(DATE, 'USA');
+-------------------------+
| GET_FORMAT(DATE, 'USA') |
+-------------------------+
| %m.%d.%Y                |
+-------------------------+
1 row in set (0.00 sec)

SELECT DATE_FORMAT(NOW(),GET_FORMAT(DATE,'USA')),
FROM DUAL;
```



```sql
mysql> SELECT STR_TO_DATE('2020-01-01 00:00:00','%Y-%m-%d'); 
+-----------------------------------------------+
| STR_TO_DATE('2020-01-01 00:00:00','%Y-%m-%d') |
+-----------------------------------------------+
| 2020-01-01                                    |
+-----------------------------------------------+
1 row in set, 1 warning (0.00 sec)
```

## 5.流程控制函数

流程处理函数可以根据不同的条件，执行不同的处理流程，可以在SQL语句中实现不同的条件选择。

MySQL中的流程处理函数主要包括`IF()、IFNULL()和CASE()函数`。

| 函数                                                         | 用法                                            |
| ------------------------------------------------------------ | ----------------------------------------------- |
| IF(value,value1,value2)                                      | 如果value的值为TRUE，返回value1，否则返回value2 |
| IFNULL(value1, value2)                                       | 如果value1不为NULL，返回value1，否则返回value2  |
| CASE WHEN 条件1 THEN 结果1 WHEN 条件2 THEN 结果2 .... [ELSE resultn] END | 相当于Java的if...else if...else...              |
| CASE expr WHEN 常量值1 THEN 值1 WHEN 常量值1 THEN 值1 .... [ELSE 值n] END | 相当于Java的switch...case...                    |

```sql
SELECT IF(1 > 0,'正确','错误')    
->正确

SELECT IFNULL(null,'Hello Word')
->Hello Word
```

```sql
SELECT CASE 
　　WHEN 1 > 0
　　THEN '1 > 0'
　　WHEN 2 > 0
　　THEN '2 > 0'
　　ELSE '3 > 0'
　　END
->1 > 0

SELECT CASE 1 
　　WHEN 1 THEN '我是1'
　　WHEN 2 THEN '我是2'
ELSE '你是谁'

# 查询员工信息并为其添加薪资描述
SELECT employee_id,salary, CASE WHEN salary>=15000 THEN '高薪' 
				  WHEN salary>=10000 THEN '潜力股'  
				  WHEN salary>=8000 THEN '屌丝' 
				  ELSE '草根' END  "描述"
FROM employees; 

# 根据status查询订单状态
SELECT oid,`status`, CASE `status` WHEN 1 THEN '未付款' 
								   WHEN 2 THEN '已付款' 
								   WHEN 3 THEN '已发货'  
								   WHEN 4 THEN '确认收货'  
								   ELSE '无效订单' END 
FROM t_order;

# 根据job_id计算出涨幅后的薪水
SELECT last_name, job_id, salary,
       CASE job_id WHEN 'IT_PROG'  THEN  1.10*salary
                   WHEN 'ST_CLERK' THEN  1.15*salary
                   WHEN 'SA_REP'   THEN  1.20*salary
       			     	ELSE   salary END  "REVISED_SALARY"
FROM   employees;

# 练习：查询部门号为 10,20, 30 的员工信息, 若部门号为 10, 则打印其工资的 1.1 倍, 20 号部门, 则打印其工资的 1.2 倍, 30 号部门打印其# 工资的 1.3 倍数。
SELECT last_name,department_id,
			CASE department_id WHEN 10 THEN 1.10*salary
			WHEN 20 THEN 1.20*salary
			WHEN 30 THEN 1.30*salary
			ELSE salary END
FROM employees
WHERE department_id IN (10,20,30);
```

## 6.加密与解密函数

加密与解密函数主要用于对数据库中的数据进行加密和解密处理，以防止数据被他人窃取。这些函数在保证数据库安全时非常有用。

| 函数                        | 用法                                                         |
| --------------------------- | ------------------------------------------------------------ |
| PASSWORD(str)               | 返回字符串str的加密版本，41位长的字符串。加密结果`不可逆`，常用于用户的密码加密 |
| MD5(str)                    | 返回字符串str的md5加密后的值，也是一种加密方式。若参数为NULL，则会返回NULL |
| SHA(str)                    | 从原明文密码str计算并返回加密后的密码字符串，当参数为NULL时，返回NULL。`SHA加密算法比MD5更加安全`。 |
| ENCODE(value,password_seed) | 返回使用password_seed作为加密密码加密value                   |
| DECODE(value,password_seed) | 返回使用password_seed作为加密密码解密value                   |

可以看到，ENCODE(value,password_seed)函数与DECODE(value,password_seed)函数互为反函数。

举例：

```sql
mysql> SELECT PASSWORD('mysql'), PASSWORD(NULL);
+-------------------------------------------+----------------+
| PASSWORD('mysql')                         | PASSWORD(NULL) |
+-------------------------------------------+----------------+
| *E74858DB86EBA20BC33D0AECAE8A8108C56B17FA |                |
+-------------------------------------------+----------------+
1 row in set, 1 warning (0.00 sec)
```

```sql
SELECT md5('123')
->202cb962ac59075b964b07152d234b70
```

```
SELECT SHA('Tom123')
->c7c506980abc31cc390a2438c90861d0f1216d50
```

```sql
mysql> SELECT ENCODE('mysql', 'mysql');
+--------------------------+
| ENCODE('mysql', 'mysql') |
+--------------------------+
| íg　¼　ìÉ                  |
+--------------------------+
1 row in set, 1 warning (0.01 sec)
```

```sql
mysql> SELECT DECODE(ENCODE('mysql','mysql'),'mysql');
+-----------------------------------------+
| DECODE(ENCODE('mysql','mysql'),'mysql') |
+-----------------------------------------+
| mysql                                   |
+-----------------------------------------+
1 row in set, 2 warnings (0.00 sec)
```

## 7.MySQL信息函数

MySQL中内置了一些可以查询MySQL信息的函数，这些函数主要用于帮助数据库开发或运维人员更好地对数据库进行维护工作。

| 函数                                                  | 用法                                                     |
| ----------------------------------------------------- | -------------------------------------------------------- |
| VERSION()                                             | 返回当前MySQL的版本号                                    |
| CONNECTION_ID()                                       | 返回当前MySQL服务器的连接数                              |
| DATABASE()，SCHEMA()                                  | 返回MySQL命令行当前所在的数据库                          |
| USER()，CURRENT_USER()、SYSTEM_USER()，SESSION_USER() | 返回当前连接MySQL的用户名，返回结果格式为“主机名@用户名” |
| CHARSET(value)                                        | 返回字符串value自变量的字符集                            |
| COLLATION(value)                                      | 返回字符串value的比较规则                                |

举例：

```sql
mysql> SELECT DATABASE();
+------------+
| DATABASE() |
+------------+
| test       |
+------------+
1 row in set (0.00 sec)

mysql> SELECT DATABASE();
+------------+
| DATABASE() |
+------------+
| test       |
+------------+
1 row in set (0.00 sec)
```

```sql
mysql> SELECT USER(), CURRENT_USER(), SYSTEM_USER(),SESSION_USER();
+----------------+----------------+----------------+----------------+
| USER()         | CURRENT_USER() | SYSTEM_USER()  | SESSION_USER() |
+----------------+----------------+----------------+----------------+
| root@localhost | root@localhost | root@localhost | root@localhost |
+----------------+----------------+----------------+----------------+
```

```sql
mysql> SELECT CHARSET('ABC');
+----------------+
| CHARSET('ABC') |
+----------------+
| utf8mb4        |
+----------------+
1 row in set (0.00 sec)
```

```sql
mysql> SELECT COLLATION('ABC');
+--------------------+
| COLLATION('ABC')   |
+--------------------+
| utf8mb4_general_ci |
+--------------------+
1 row in set (0.00 sec)
```

## 8.其他函数

MySQL中有些函数无法对其进行具体的分类，但是这些函数在MySQL的开发和运维过程中也是不容忽视的。

| 函数                           | 用法                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| FORMAT(value,n)                | 返回对数字value进行格式化后的结果数据。n表示`四舍五入`后保留到小数点后n位 |
| CONV(value,from,to)            | 将value的值进行不同进制之间的转换                            |
| INET_ATON(ipvalue)             | 将以点分隔的IP地址转化为一个数字                             |
| INET_NTOA(value)               | 将数字形式的IP地址转化为以点分隔的IP地址                     |
| BENCHMARK(n,expr)              | 将表达式expr重复执行n次。用于测试MySQL处理expr表达式所耗费的时间 |
| CONVERT(value USING char_code) | 将value所使用的字符编码修改为char_code                       |

举例：

```sql
# 如果n的值小于或者等于0，则只保留整数部分
mysql> SELECT FORMAT(123.123, 2), FORMAT(123.523, 0), FORMAT(123.123, -2); 
+--------------------+--------------------+---------------------+
| FORMAT(123.123, 2) | FORMAT(123.523, 0) | FORMAT(123.123, -2) |
+--------------------+--------------------+---------------------+
| 123.12             | 124                | 123                 |
+--------------------+--------------------+---------------------+
1 row in set (0.00 sec)
```

```sql
mysql> SELECT CONV(16, 10, 2), CONV(8888,10,16), CONV(NULL, 10, 2);
+-----------------+------------------+-------------------+
| CONV(16, 10, 2) | CONV(8888,10,16) | CONV(NULL, 10, 2) |
+-----------------+------------------+-------------------+
| 10000           | 22B8             | NULL              |
+-----------------+------------------+-------------------+
1 row in set (0.00 sec)
```

```sql
mysql> SELECT INET_ATON('192.168.1.100');
+----------------------------+
| INET_ATON('192.168.1.100') |
+----------------------------+
|                 3232235876 |
+----------------------------+
1 row in set (0.00 sec)

# 以“192.168.1.100”为例，计算方式为192乘以256的3次方，加上168乘以256的2次方，加上1乘以256，再加上100。
```

```sql
mysql> SELECT INET_NTOA(3232235876);
+-----------------------+
| INET_NTOA(3232235876) |
+-----------------------+
| 192.168.1.100         |
+-----------------------+
1 row in set (0.00 sec)
```

```sql
mysql> SELECT BENCHMARK(1, MD5('mysql'));
+----------------------------+
| BENCHMARK(1, MD5('mysql')) |
+----------------------------+
|                          0 |
+----------------------------+
1 row in set (0.00 sec)

mysql> SELECT BENCHMARK(1000000, MD5('mysql')); 
+----------------------------------+
| BENCHMARK(1000000, MD5('mysql')) |
+----------------------------------+
|                                0 |
+----------------------------------+
1 row in set (0.20 sec)
```

```sql
mysql> SELECT CHARSET('mysql'), CHARSET(CONVERT('mysql' USING 'utf8'));
+------------------+----------------------------------------+
| CHARSET('mysql') | CHARSET(CONVERT('mysql' USING 'utf8')) |
+------------------+----------------------------------------+
| utf8mb4          | utf8                                   |
+------------------+----------------------------------------+
1 row in set, 1 warning (0.00 sec)
```





# 第八章、聚合函数和分组

## 1.聚合函数的介绍

> 聚合函数作用于一组数据，并对一组数据返回一个值。（例如：求一组数据的平均值，最大值等）

![Dim0z.png](https://i.328888.xyz/2022/12/23/Dim0z.png)

常见的聚合函数：

​	AVG() : 求平均值

​	SUM() : 求和

​	MAX() : 求最大值

​	MIN() : 求最小值

​	COUNT() : 求记录条数

聚合函数语法：

![DihX5.png](https://i.328888.xyz/2022/12/23/DihX5.png)

**`【注】聚合函数不能嵌套调用。比如不能出现类似“AVG(SUM(字段名称))”形式的调用。`**

## 2.AVG 和 SUM 函数

可以对`数值型数据`使用AVG()和SUM()函数

```mysql
# 求工作id为REP的平均薪水和薪水总和

SELECT AVG(salary), SUM(salary)
FROM employees
WHERE job_id LIKE '%REP%';
```

## 3.MIN 和 MAX 函数

可以对`任意数据类型的数据`使用 MIN 和 MAX 函数。

```mysql
# 查询员工表中最小和最大的入职时间

SELECT MIN(hire_date), MAX(hire_date)
FROM employees;
```

## 4.COUNT 函数

`count函数用于返回记录条数`

COUNT(*)返回表中记录总数，适用于任意数据类型。

```mysql
# 查询部门id为50的记录数

SELECT COUNT(*)
FROM employees
WHERE department_id = 50;
```

COUNT(expr) 返回`expr不为空`的记录总数。  

```mysql
# 查询commission_pct不为空的部门id为50 的记录数
SELECT COUNT(commission_pct)
FROM employees
WHERE department_id = 50;
```

- 问题：用count( * )，count(1)，count(列名)谁好呢?
  其实，对于MyISAM引擎的表是没有区别的。这种引擎内部有一计数器在维护着行数。
  Innodb引擎的表用count( * ),count(1)直接读行数，复杂度是O(n)，因为innodb真的要去数一遍。但好
  于具体的count(列名)。
- 问题：能不能使用count(列名)替换count( * )?
  不要使用 count(列名)来替代 count( * ) ， count( * ) 是 SQL92 定义的标准统计行数的语法，跟数
  据库无关，跟 NULL 和非 NULL 无关。
  说明： **count(*)会统计值为 NULL 的行，而 count(列名)不会统计此列为 NULL 值的行**



## 5.GROUP BY分组

使用GROUP BY子句可以将表中的数据进行分组

```sql
SELECT column, group_function(column)
FROM table
[WHERE condition]
[GROUP BY group_by_expression]
[ORDER BY column];
```

> 明确：WHERE一定放在FROM后面
>

在使用group by 时需要注意：

- 在select列表中所有`未包含`在`聚合函数`中的列都应该包含在group by子句中 

  ```sql
  SELECT department_id, AVG(salary)
  FROM employees
  GROUP BY department_id ;
  
  # 上述查询语句中select中department_id字段也应该存在于group by子句中
  ```

  

- `包含在 GROUP BY 子句`中的列`不必包含在SELECT` 列表中

  ```sql
  SELECT AVG(salary)
  FROM employees
  GROUP BY job_id ;
  ```

  

> 可以对多个字段进行分组

```sql
SELECT department_id dept_id, job_id, SUM(salary)
FROM employees
GROUP BY department_id, job_id ;

# 上述查询语句 现根据部门id进行分组，然后再根据工作id进行分组最后求和
```

**WITH ROLLUP关键字**

​	使用 WITH ROLLUP 关键字之后，在所有查询出的分组记录之后增加一条记录，该记录计算查询出的所
​	有记录的总和，即统计记录数量。

```sql
SELECT department_id,AVG(salary)
FROM employees
WHERE department_id > 80
GROUP BY department_id WITH ROLLUP;
```

> 注意：
> 当使用ROLLUP时，不能同时使用ORDER BY子句进行结果排序，即**ROLLUP和ORDER BY是互相排斥**的。

## 6.HAVING 

> HAVING  （1）用来过滤数据 常用来对组数据进行过滤，一般在GROUP BY 后面使用。
>
> ​	（2）在mysql中HAVING也可以单独使用，将表中所有数据看成一组。
>
> ​	（3）在 HAVING 中可以使用聚合函数，而 WHERE 中不能使用聚合函数。
>
> ​	（4）HAVING的三要素
>
> ​		常数  聚合函数  聚合键（**聚合键也就是 GROUP BY 子句中指定的列名**）
>
> ​	（5）聚合键所对应的条件应该书写在 WHERE 子句中 

```sql
SELECT department_id, MAX(salary)
FROM employees
GROUP BY department_id
HAVING MAX(salary)>10000 ;
```

## 7.HAVING 和 WHERE对比

**区别1：WHERE 可以直接使用表中的字段作为筛选条件，但不能使用分组中的`计算函数`作为筛选条件；
	HAVING 必须要与 GROUP BY 配合使用，可以把分组计算的函数和分组字段作为筛选条件。**

​	这决定了，在需要对数据进行分组统计的时候，HAVING 可以完成 WHERE 不能完成的任务。这是因为，在查询语法结构中，WHERE 在 GROUP BY 之前，所以无法对分组结果进行筛选。HAVING 在 GROUP BY 之后，可以使用分组字段和分组中的计算函数，对分组的结果集进行筛选，这个功能是 WHERE 无法完成的。另外，WHERE排除的记录不再包括在分组中。

**区别2：如果需要通过连接从关联表中获取需要的数据，WHERE 是先筛选后连接，而 HAVING 是先连接后筛选。**

​	这一点，就决定了在关联查询中，WHERE 比 HAVING 更高效。因为 WHERE 可以先筛选，用一个筛选后的较小数据集和关联表进行连接，这样占用的资源比较少，执行效率也比较高。HAVING 则需要先把结果集准备好，也就是用未被筛选的数据集进行关联，然后对这个大的数据集进行筛选，这样占用的资源就比较多，执行效率也较低。



小结：

​	（1）WHERE 子句和 HAVING 子句的作用是不同的；前面已经说过，HAVING 子句是用来指定“组”的条件的，而“行”所对应的条件应该写在 WHERE 子句中，这样一来，写出来的 SQL 语句不但可以分清两者各自的功能，而且理解起来也更容易

​	（2）使用 COUNT 等函数对表中数据进行聚合操作时，DBMS 内部进行排序处理，而排序处理会大大增加机器的负担，从而降低处理速度；因此，尽可能减少排序的行数，可以提高处理速度`通过 WHERE 子句指定条件时，由于排序之前就对数据进行了过滤`，那么就`减少了聚合操作时的需要排序的记录数量`；而 `HAVING 子句是在排序之后才对数据进行分组的`，与在 WHERE 子句中指定条件比起来，需要排序的数量就会多得多。另外，索引是 WHERE 根据速度优势的另一个有利支持，在 WHERE 子句指定条件所对应的列上创建索引，可以大大提高 WHERE 子句的处理速度。



`开发中的选择：`
	WHERE 和 HAVING 也不是互相排斥的，我们可以在一个查询里面同时使用 WHERE 和 HAVING。包含分组统计函数的条件用 HAVING，普通条件用 WHERE。这样，我们就既利用了 WHERE 条件的高效快速，又发挥了 HAVING 可以使用包含分组统计函数的查询条件的优点。当数据量特别大的时候，运行效率会有很大的差别。

## 8.SELECT执行过程

常见的查询语句的结构：

> 方式1：
>
> SELECT ...,....,...
> FROM ...,...,....
> WHERE 多表的连接条件
> AND 不包含组函数的过滤条件
> GROUP BY ...,...
> HAVING 包含组函数的过滤条件
> ORDER BY ... ASC/DESC
> LIMIT ...,...
>
> 
>
> #方式2：
> SELECT ...,....,...
> FROM ... JOIN ...
> ON 多表的连接条件
> JOIN ...
> ON ...
> WHERE 不包含组函数的过滤条件
> AND/OR 不包含组函数的过滤条件
> GROUP BY ...,...
> HAVING 包含组函数的过滤条件
> ORDER BY ... ASC/DESC
> LIMIT ...,...
>
> 
>
> #其中：
> #（1）from：从哪些表中筛选
> #（2）on：关联多表查询时，去除笛卡尔积
> #（3）where：从表中筛选的条件
> #（4）group by：分组依据
> #（5）having：在统计结果中再次筛选
> #（6）order by：排序
> #（7）limit：分页



**SELECT查询的书写顺序**

​	SELECT ... FROM ... WHERE ... GROUP BY ... HAVING ... ORDER BY ... LIMIT...

**SELECT查询的执行顺序**

​	FROM -> WHERE -> GROUP BY -> HAVING -> SELECT 的字段 -> DISTINCT -> ORDER BY -> LIMIT

![jxNNv.png](https://i.328888.xyz/2023/01/28/jxNNv.png)

```sql
SELECT DISTINCT player_id, player_name, count(*) as num # 顺序 5
FROM player JOIN team ON player.team_id = team.team_id # 顺序 1
WHERE height > 1.80 # 顺序 2
GROUP BY player.team_id # 顺序 3
HAVING num > 2 # 顺序 4
ORDER BY num DESC # 顺序 6
LIMIT 2 # 顺序 7
```

## 9.SQL的执行原理

SELECT 是先执行 **FROM** 这一步的。在这个阶段，如果是多张表联查，还会经历下面的几个步骤：
1. 首先先通过 CROSS JOIN 求笛卡尔积，相当于得到虚拟表 vt（virtual table）1-1；
2. 通过 ON 进行筛选，在虚拟表 vt1-1 的基础上进行筛选，得到虚拟表 vt1-2；
3. 添加外部行。如果我们使用的是左连接、右链接或者全连接，就会涉及到外部行，也就是在虚拟
    表 vt1-2 的基础上增加外部行，得到虚拟表 vt1-3。

当然如果我们操作的是**两张以上的表，**还会**重复上面的步骤**，直到所有表都被处理完为止。这个过程得到是我们的原始数据。

当我们拿到了查询数据表的原始数据，也就是最终的虚拟表 vt1 ，就可以在此基础上再进行 **WHERE 阶段** 。在这个阶段中，会根据 vt1 表的结果进行筛选过滤，得到虚拟表 vt2 。然后进入第三步和第四步，也就是 **GROUP 和 HAVING 阶段** 。在这个阶段中，实际上是在虚拟表 vt2 的基础上进行分组和分组过滤，得到中间的虚拟表 vt3 和 vt4 。

当我们完成了条件筛选部分之后，就可以筛选表中提取的字段，也就是进入到 **SELECT 和 DISTINCT阶段** 。

首先在 **SELECT 阶段**会提取想要的字段，然后在 **DISTINCT 阶段过**滤掉重复的行，分别得到中间的虚拟表vt5-1 和 vt5-2 。

当我们提取了想要的字段数据之后，就可以按照指定的字段进行排序，也就是 **ORDER BY 阶段** ，得到虚拟表 vt6 。

最后在 vt6 的基础上，取出指定行的记录，也就是 **LIMIT** 阶段 ，得到最终的结果，对应的是虚拟表vt7 。

当然我们在写 SELECT 语句的时候，不一定存在所有的关键字，相应的阶段就会省略。同时因为 SQL 是一门类似英语的结构化查询语言，所以我们在写 SELECT 语句的时候，还要注意相应的关键字顺序，所谓底层运行的原理，就是我们刚才讲到的执行顺序。



# 第九章、子查询

## 1.基本概念

> **子查询**: 指一个查询语句嵌套在另一个查询语句内部的查询，这个特性从MySQL 4.1开始引入。
>
> ​	SQL 中子查询的使用大大增强了 SELECT 查询的能力，因为很多时候查询需要从结果集中获取数据，或者
>
> ​	需要从同一个表中先计算得出一个数据结果，然后与这个数据结果（可能是某个标量，也可能是某个集合）进行比较。

**问题分析：**在employees表中我们需要知道那些人的工资比某个人高，则我们需要先查询到这个人的工资信息，然后再进行查询。

以往的做法：

```sql
#方式一：
SELECT salary
FROM employees
WHERE last_name = 'Abel';

SELECT last_name,salary
FROM employees
WHERE salary > 11000;

#方式二：自连接
SELECT e2.last_name,e2.salary
FROM employees e1,employees e2
WHERE e1.last_name = 'Abel'
AND e1.`salary` < e2.`salary`
```

使用子查询：

```sql
SELECT last_name,salary
FROM employees
WHERE salary > (
      SELECT salary
      FROM employees
      WHERE last_name = 'Abel'
);
```

## 2.基本使用

**语法结构：**

​	![167499927933187cc01a0ea465c79.png](https://img.picgo.net/2023/01/29/167499927933187cc01a0ea465c79.png)

- 子查询（内查询）在主查询之前一次执行完成。
- 子查询的结果被主查询（外查询）使用 。
- **注意事项：**
  - 子查询要包含在括号内
  - 将子查询放在比较条件的右侧
  - 单行操作符对应单行子查询，多行操作符对应多行子查询

## 3.子查询的分类

方式1：我们按**子查询的结果**返回**一条**还是**多条记录**，将子查询分为 `单行子查询 、 多行子查询 `。

方式2：我们按**子查询是否被执行多次**，将子查询划分为 **相关(或关联)子查询** 和 **不相关(或非关联)子查询** 。

​	子查询从数据表中查询了数据结果，如果这个`数据结果只执行一次`，然后这个数据结果作为主查询的条件进行执行，那么该子查询叫**不相关子查询。**
​	同样，如果`子查询需要执行多次`，即采用循环的方式，先从外部查询开始，每次都传入子查询进行查询，然后再将结果反馈给外部，这种嵌套的执行方式就称为**相关子查询。**

### 3.1 单行子查询

单行比较操作符

![167499999597430befb401194b7d6.png](https://img.picgo.net/2023/01/29/167499999597430befb401194b7d6.png)

代码实例：返回job_id与141号员工相同，salary比143号员工多的员工姓名，job_id和工资

```sql
SELECT last_name, job_id, salary
FROM employees
WHERE job_id =
      (SELECT job_id
      FROM employees
      WHERE employee_id = 141)
AND salary >
      (SELECT salary
      FROM employees
      WHERE employee_id = 143);
```

代码示例：返回公司工资最少的员工的last_name,job_id和salary

```sql
SELECT last_name, job_id, salary
FROM employees
WHERE salary =
      (SELECT MIN(salary)
      FROM employees);
```



**HAVING中的子查询**

​	首先执行子查询。

​	向主查询中的HAVING 子句返回结果。

代码示例：查询最低工资大于   50号部门最低工资（未知） 的部门id和其最低工资

```sql
SELECT department_id, MIN(salary)
FROM employees
GROUP BY department_id
HAVING MIN(salary) >
      (SELECT MIN(salary)
      FROM employees
      WHERE department_id = 50);
```

**CASE中的子查询**

代码示例：显式员工的employee_id,last_name和location。其中，若员工department_id与   `location_id为1800的department_id（未知）`  相同，则location为’Canada’，其余则为’USA’。

```sql
SELECT employee_id, last_name,
        (CASE department_id
        WHEN
            (SELECT department_id FROM departments
            WHERE location_id = 1800)
				THEN 'Canada' ELSE 'USA' END) location
FROM employees;
```

### 3.2 多行子查询

多行比较操作符

![1675000914985d010e181861b362b.png](https://img.picgo.net/2023/01/29/1675000914985d010e181861b362b.png)

**IN操作符**代码示例：查询与  141号或174号员工的manager_id和department_id(未知) 相同的其他员工的employee_id，manager_id，department_id

```sql
SELECT employee_id, manager_id, department_id
FROM employees
WHERE manager_id IN
        (SELECT manager_id
        FROM employees
        WHERE employee_id IN (174,141))
AND department_id IN
        (SELECT department_id
        FROM employees
        WHERE employee_id IN (174,141))
AND employee_id NOT IN(174,141);


SELECT employee_id, manager_id, department_id
FROM employees
WHERE (manager_id, department_id) IN
              (SELECT manager_id, department_id
              FROM employees
              WHERE employee_id IN (141,174))
AND employee_id NOT IN (141,174);
```

**ANY操作符**代码示例：返回其它job_id中比job_id为‘IT_PROG’部门任一工资（未知）低的员工的员工号、姓名、job_id 以及salary

（只要有比子查询查询到的集合数据中小的即可）

![1675043919195fea102905f408e0f.png](https://img.picgo.net/2023/01/30/1675043919195fea102905f408e0f.png)

**ALL操作符**代码示例：返回其它job_id中比job_id为‘IT_PROG’部门所有工资（未知）低的员工的员工号、姓名、job_id 以及salary

（要比子查询查询到的集合数据都要小）

![1675044146441d62d2318fe1842fc.png](https://img.picgo.net/2023/01/30/1675044146441d62d2318fe1842fc.png)

### 3.3 相关子查询

> **相关子查询执行流程：**
> 	如果子查询的执行依赖于外部查询，通常情况下都是因为子查询中的表用到了外部的表，并进行了条件
>
> ​	关联，因此每执行一次外部查询，子查询都要重新计算一次，这样的子查询就称之为 关联子查询 。
>
> ​	相关子查询按照一行接一行的顺序执行，主查询的每一行都执行一次子查询。

![1675044813855e42fbc9056d39a5b.png](https://img.picgo.net/2023/01/30/1675044813855e42fbc9056d39a5b.png)

**代码实例：**查询员工中工资大于 本部门平均工资（未知）的员工的last_name,salary和其department_id

本部门平均工资需要当前员工所处部门id

```sql
# 使用相关子查询
SELECT last_name,salary,department_id
FROM employees AS outer
WHERE salary > (
						SELECT AVG(salary)
						FROM employees
						WHERE emplutees.`department_id` = outer.`department_id`;
)

#在FROM中使用子查询
SELECT last_name,salary,department_id
FROM employees AS e,(
	SELECT department_id,AVG(salary) dep_AVGS
  FROM employees
  GROUP BY department_id
) AS a
WHERE e.`salary` > a.`dep_AVGS` AND e.`department_id` = a.`department_id`;
```

**from型的子查询：子查询是作为from的一部分，子查询要用()引起来，并且要给这个子查询取别名， 把它当成一张“临时的虚拟的表”来使用。**



**在ORDER BY 中使用子查询**

**代码实例：**查询员工的id,salary,按照department_name（未知） 排序

```sql
SELECT employee_id,salary
FROM employees e
    ORDER BY (
    SELECT department_name
    FROM departments d
    WHERE e.`department_id` = d.`department_id`
);
```

## 4.EXISTS 与 NOT EXISTS关键字

> 关联子查询通常也会和 EXISTS操作符一起来使用，用来检查在子查询中是否存在满足条件的行。

- 如果在子查询中不存在满足条件的行：
    - 条件返回 FALSE
    - 继续在子查询中查找

- 如果在子查询中存在满足条件的行：
  - 不在子查询中继续查找
  - 条件返回 TRUE

- NOT EXISTS关键字表示如果不存在某种条件，则返回TRUE，否则返回FALSE

（我们一般在新建数据库、表时会加上IF NOT EXISTS）

**代码示例：**查询departments表中，不存在于employees表中的部门的department_id和department_name

```sql
SELECT department_id, department_name
FROM departments d
WHERE NOT EXISTS (SELECT 'X'
									FROM employees
									WHERE department_id = d.department_id);
```



