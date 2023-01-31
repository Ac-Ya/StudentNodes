# 第十章、创建和管理数据库/表(DDL)

## 1.基础知识

> 数据库/数据表的创建，修改，删除等操作数据 DDL（数据定义语言）范畴

**一条数据存储的过程**

​	存储数据是处理数据的第一步 。只有正确地把数据存储起来，我们才能进行有效的处理和分析。

​	在 MySQL 中，一个完整的数据存储过程总共有 4 步，

​		**创建数据库、确认字段、创建数据表、插入数据。**

![1675060756480521c59ec4e44dce9.png](https://img.picgo.net/2023/01/30/1675060756480521c59ec4e44dce9.png)

## 2.创建和管理数据库

### 2.1 数据库的创建

> 关键字：CREATE DATABASE  (create database)

方式一：

```sql
CREATE DATABASE 数据库名；
```

方式二：创建数据库并指定字符集

```sql
CREATE DATABASE 数据库名 CHARACTER SET 字符集；
```

方式三：判断数据库是否已经存在，不存在则创建数据库（ 推荐 ）

```sql
CREATE DATABASE IF NOT EXISTS 数据库名;
```

【注意】：`DATABASE 不能改名。一些可视化工具可以改名，它是建新库，把所有表复制到新库，再删旧库完成的。`

### 2.2 数据库的使用

> 关键字：SHOW ，USE 

- 查看所有的数据库 (database+s)

```sql
SHOW DATABASES;
```

- 使用/切换数据库

```sql
USE 数据库名；
```

- 查看当前使用的数据库

```sql
SHOW DATABASE();
```

- 查看数据库的创建信息

```sql
SHOW CREATE DATABASE 数据库名；

SHOW CREATE DATABASE 数据库名\G
```

- 查看指定数据库的所有表（不用进入到该数据库 USE）

```sql
SHOW TABLES FROM 数据库名；
```

> **注意**：`要操作表格和数据之前必须先说明是对哪个数据库进行操作，否则就要对所有对象加上“数据库名.”。`

### 2.3 数据库的修改

> 关键字：ALTER DATABASE

- 更改数据库字符集

```sql
ALTER DATABASE 数据库名 CHARACTER SET 字符集； #比如：gbk、utf8等
```

### 2.4 数据库的删除

> 关键字：DROP DATABASE

- 删除指定的数据库方法一：

```sql
DROP DATABASE 数据库名；
```

- 删除指定的数据库方法二：

```sql
DROP DATABASE IF EXISTS 数据库名；
```

## 3.创建和管理表

### 3.1 表的创建

> 关键字：CREATE TABLE

**方式一**

具备条件

 - CREATE TABLE 权限
 - 存储空间

语法格式

```sql
CREATE TABLE [IF NOT EXISTS] 表名(
    字段1, 数据类型 [约束条件] [默认值],
    字段2, 数据类型 [约束条件] [默认值],
    字段3, 数据类型 [约束条件] [默认值],
    ……
		[表约束条件]
);
```

【注】加上了**IF NOT EXISTS**关键字，则表示：如果当前数据库中不存在要创建的数据表，则创建数据表；如果当前数据库中已经存在要创建的数据表，则忽略建表语句，不再创建数据表。

必须指明

- 表名
- 列名，数据类型，长度

可选指定

- 约束条件
- 默认值

```sql
-- 创建表
CREATE TABLE emp (
  -- int类型
  emp_id INT,
  -- 最多保存20个中英文字符
  emp_name VARCHAR(20),
  -- 总位数不超过15位
  salary DOUBLE,
  -- 日期类型
  birthday DATE
);
```

【注】MySQL在执行建表语句时，将id字段的类型设置为int(11)，这里的11实际上是int类型指定的显示宽度，**默认的显示宽度为11**。也可以在创建数据表的时候指定数据的显示宽度。

> 在MySQL 8.x版本中，不再推荐为INT类型指定显示长度，并在未来的版本中可能去掉这样的语法。

**方式二** 通过子查询将子查询的数据作为新表的数据

使用 AS subquery 选项，将创建表和插入数据结合起来

指定的列和子查询中的列要一一对应

![1675080066348ccd5527905977e4b.png](https://img.picgo.net/2023/01/30/1675080066348ccd5527905977e4b.png)

通过列名和默认值定义列

```sql
CREATE TABLE emp1 AS SELECT * FROM employees;
CREATE TABLE emp2 AS SELECT * FROM employees WHERE 1=2; -- 创建的emp2是空表
```

### 3.2 查看表结构

> 在MySQL中创建好数据表之后，可以查看数据表的结构。MySQL支持使用 DESCRIBE/DESC 语句查看数据表结构，也支持使用 SHOW CREATE TABLE 语句查看数据表结构。

```sql
SHOW CREATE TABLE 表名\G
-- 使用SHOW CREATE TABLE语句不仅可以查看表创建时的详细语句，还可以查看存储引擎和字符编码。
DESCRUBE 表名;
```

### 3.3 表的修改

> **关键字**：ALTER TABLE
>
> ​      修改表指的是修改数据库中已经存在的**数据表的结构(不是表中的数据)。**

**使用`ALTER TABLE`能够实现**

- 向表中添加新的列（字段）
- 修改表中的列（字段）
- 删除表中的列（字段）
- 重命名表中的列（字段）

**`添加新字段`**

语法格式：ALTER TABLE 表名 **ADD** 【COLUMN】 字段名 字段类型 【FIRST|AFTER 字段名】;

```sql
ALTER TABLE dept80 ADD job_id varchar(15);
```

**`修改字段`**

可以修改字段的数据类型，长度、默认值和位置

语法格式：ALTER TABLE 表名 **MODIFY** 【COLUMN】 字段名1 字段类型 【DEFAULT 默认值】【FIRST|AFTER 字段名2】;

```sql
ALTER TABLE dept80 MODIFY last_name VARCHAR(30);

ALTER TABLE dept80 MODIFY salary double(9,2) default 1000;
```

**`重命名字段`**

语法格式：ALTER TABLE 表名 **CHANGE** 【column】 **字段名 新字段名 新数据类型;**

```sql
ALTER TABLE dept80 CHANGE department_name dept_name varchar(15);
```

**`删除字段`**

语法格式：ALTER TABLE 表名 **DROP** [column] 字段名;

```sql
ALTER TABLE dept80 DROP COLUMN job_id;
```

### 3.4 重命名表

> **关键字**：RENAME

方法一:

```sql
RENAME TABLE 表名 TO 新表名；
```

方法二:

```sql
ALTER TABLE 表名 RENAME 新表名；
```

### 3.5 表的删除

> 关键字：DROP TABLE

- 在MySQL中，当一张数据表 没有与其他任何数据表形成关联关系 时，可以将当前数据表直接删除。
- 数据和结构都被删除
- 所有正在运行的相关事务被提交
- 所有相关索引被删除

**语法格式：**DROP TABLE [IF EXISTS] 数据表1 [, 数据表2, …, 数据表n];

IF EXISTS 的含义为：如果当前数据库中存在相应的数据表，则删除数据表；如果当前数据库中不存在相应的数据表，则忽略删除语句，不再执行删除数据表的操作。

```sql
DROP TABLE dept80;
```

【注】**`DROP TABLE 语句不能回滚`**

### 3.6 清空表

> **关键字**：TRUNCATE TABLE 表名

- 删除表中所有的数据
- 释放表的存储空间

```sql
TRUNCATE TABLE detail_dept;
```

【注】**`TRUNCATE（属DDL语言范畴）语句不能回滚，而使用 DELETE 语句删除数据(属DML语言范畴)，可以回滚`**





> 【参考】TRUNCATE TABLE 比 DELETE 速度快，且使用的系统和事务日志资源少，但 TRUNCATE 无
> 事务且不触发 TRIGGER，有可能造成事故，故不建议在开发代码中使用此语句。
> 说明：TRUNCATE TABLE 在功能上与不带 WHERE 子句的 DELETE 语句相同。



# 第十一章、数据处理之增删改（DML）

## 1.插入数据

> 关键字：INSTER INTO 表名 、 VALUES

### 1.1 使用VALUES

- **`为表的所有字段按默认顺序插入数据`**（不用指定字段名）

  语法格式：INSERT INTO 表名 VALUES (value1,value2,....);

  【注】value的顺序与定义表中字段的顺序一样

```sql
INSERT INTO departments
VALUES (70, 'Pub', 100, 1700);
```

- **`为表指定字段添加值`**

  语法格式：INSERT INTO 表名(字段名1,字段名2,字段名3...) VALUES(value1,value2,value3...)

  【注】在INSERT语句中只向部分字段中插入值，而其他字段的值为表定义时的默认值或null。

  ​	字段名与值的数据类型应该是对应的。否则会报错。

```sql
INSERT INTO departments(department_id, department_name)
VALUES (80, 'IT');
```

- **`同时插入多条记录`**

  语法格式：

   	INSERT INTO 表名
           VALUES
   	(value1 [,value2, …, valuen]),
   	(value1 [,value2, …, valuen]),
   	……
   	(value1 [,value2, …, valuen]);

```sql
mysql> INSERT INTO emp(emp_id,emp_name)
-> VALUES (1001,'shkstart'),
-> (1002,'atguigu'),
-> (1003,'Tom');
Query OK, 3 rows affected (0.00 sec)
Records: 3 Duplicates: 0 Warnings: 0
```

【注】使用INSERT同时插入多条记录时，MySQL会返回一些在执行单行插入时没有的额外信息，这些信息的含
义如下：

 ●　Records：表明插入的记录条数。

 ●　Duplicates：表明插入时被忽略的记录，原因可能是这些记录包含了重复的主键值。

 ●　Warnings：表明有问题的数据值，例如发生数据类型转换。

> 一个同时插入多行记录的INSERT语句等同于多个单行插入的INSERT语句，但是**多行的INSERT语句在处理过程中 效率更高** 。因为MySQL执行单条INSERT语句插入多行数据比使用多条INSERT语句快，所以在插入多条记录时最好选择使用单条INSERT语句的方式插入。

### 1.2 将查询结果插入到表中

> **INSERT还可以将SELECT语句查询的结果插入到表中**，此时不需要把每一条记录的值一个一个输入，只需要使用一条INSERT语句和一条SELECT语句组成的组合语句即可快速地从一个或多个表中向一个表中插入多行。

- 在 INSERT 语句中加入**子查询**。
- **不必书写 VALUES 子句。**
- 子查询中的值列表应与 INSERT 子句中的列名对应。

语法格式：

 	**INSERT INTO 目标表名** **(目标字段名1 [, 目标字段名2, …, 目标字段名n])**

 	**SELECT** **(源字段名1 [, 源字段名2, …, 源字段名n])**

 	**FROM 源表名**

​	 **[WHERE condition]**

```sql
INSERT INTO sales_reps(id, name, salary, commission_pct)
SELECT employee_id, last_name, salary, commission_pct
FROM employees
WHERE job_id LIKE '%REP%';
```

## 2.更新数据

> **关键字：** UPDATE 表名 SET

语法格式：	

​	**UPDATE 表名**

​	**SET column1=value1, column2=value2, … , column=valuen**

​	**[WHERE condition]**

- 可以一次更新多条数据（不使用WHERE）。
- 如果需要回滚数据，需要保证在DML前，进行设置：**SET AUTOCOMMIT = FALSE**

**`使用WHERE 更新指定的数据`**

```sql
UPDATE employees
SET department_id = 70
WHERE employee_id = 113;
```

**`省略WHERE 更新表中所有数据`**

```sql
UPDATE copy_emp
SET department_id = 110;
```

**`更新中的数据完整性错误`**

```sql
#将部门id为110的部门id改为55
UPDATE employees
SET department_id = 55
WHERE department_id = 110;

#此sql会报错因为在部门表中不存在55号部门
```

## 3.删除数据

> **关键字**：DELETE FROM 表名

语法格式：DELETE FROM table_name [WHERE];

- table_name指定要执行删除操作的表；
- “[WHERE ]”为可选参数，指定删除条件，如果没有WHERE子句，DELETE语句将删除表中的所有记录。

**`使用 WHERE 子句删除指定的记录。`**

```sql
DELETE FROM departments
WHERE department_name = 'Finance';
```

**`如果省略 WHERE 子句，则表中的全部数据将被删除`**

```sql
DELETE FROM copy_emp;
```

**`删除中的数据完整性错误`**

```sql
# 删除部门表中部门id为60 的部门
DELETE FROM departments
WHERE department_id = 60;

# 删除会报错因为在员工表中department_id作为外键进行约束
```

# 第十二章、MySQL数据类型

## 1.MySQL中的数据类型

**`常见的数据类型`**

![1675145828498cd785058b7e3712b.png](https://img.picgo.net/2023/01/31/1675145828498cd785058b7e3712b.png)

**`常见的数据类型的属性`**

![16751459594296f14d0e744fa99af.png](https://img.picgo.net/2023/01/31/16751459594296f14d0e744fa99af.png)

## 2.整数类型

### 2.1 类型介绍

> **整数类型**一共有 5 种，包括 **TINYINT、SMALLINT、MEDIUMINT、INT（INTEGER）和 BIGINT。**

![1675146157467](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1675146157467.png)

### 2.2 可选属性

整数类型的可选属性有三个：M，UNSIGNED,ZEROFILL

**`M`**: 表示显示宽度，M的取值范围是(0, 255)。例如，int(5)：当数据宽度小于5位的时候在数字前面需要用字符填满宽度。该项功能需要配合“ ZEROFILL ”使用，表示用“0”填满宽度，否则指定显示宽度无效。

【注】如果设置了显示宽度，那么插**入的数据宽度超过显示宽度限制**，会不会截断或插入失败？

答案：不会对插入的数据有任何影响，还是按照类型的实际宽度进行保存，即 **显示宽度与类型可以存储的值范围无关** 。**从MySQL 8.0.17开始，整数数据类型**

**不推荐使用显示宽度属性。**

整型数据类型可以在定义表结构时指定所需要的显示宽度，如果不指定，则系统为每一种类型指定默认的宽度值。

```sql
CREATE TABLE test_int1 ( x TINYINT, y SMALLINT, z MEDIUMINT, m INT, n BIGINT );

-- 查看表结构 （MySQL5.7中显式如下，MySQL8中不再显式范围）
mysql> desc test_int1;
+-------+--------------+------+-----+---------+-------+
| Field | Type | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| x | tinyint(4) | YES | | NULL | |
| y | smallint(6) | YES | | NULL | |
| z | mediumint(9) | YES | | NULL | |
| m | int(11) | YES | | NULL | |
| n | bigint(20) | YES | | NULL | |
+-------+--------------+------+-----+---------+-------+
5 rows in set (0.00 sec)
```



**`UNSIGNED`**:**无符号类型（非负**），**所有的整数类型**都有一个可选的属性UNSIGNED（无符号属性），无符号整数类型**的最小取值为0**。所以，如果需要在MySQL数据库中保存**非负整数值**时，可以将整数类型**设置为无符号类型**。

【注】int类型默认显示宽度为int(11)，无符号int类型默认显示宽度为int(10)。

```sql
CREATE TABLE test_int3(
f1 INT UNSIGNED
);
mysql> desc test_int3;
+-------+------------------+------+-----+---------+-------+
| Field | Type | Null | Key | Default | Extra |
+-------+------------------+------+-----+---------+-------+
| f1 | int(10) unsigned | YES | | NULL | |
+-------+------------------+------+-----+---------+-------+
1 row in set (0.00 sec)
```

**`ZEROFILL :`** **0填充,**（如果某列是ZEROFILL，那么MySQL会自动为当前列添加UNSIGNED属性），如果指定了ZEROFILL只是表示不够M位时，用0在左边填充，如果超过M位，只要不超过数据存储范围即可。

原来，在 int(M) 中，M 的值跟 int(M) 所占多少存储空间并无任何关系。 **int(3)、int(4)、int(8) 在磁盘上都是占用 4 bytes 的存储空间**。也就是说，int(M)，必须和UNSIGNED ZEROFILL一起使用才有意义。如果整数值超过M位，就按照实际位数存储。只是无须再用字符 0 进行填充。

### 2.3 适用场景

**`TINYINT`** ：一般用于枚举数据，比如系统设定取值范围很小且固定的场景。

**`SMALLINT`** ：可以用于较小范围的统计数据，比如统计工厂的固定资产库存数量等。

**`MEDIUMINT`** ：用于较大整数的计算，比如车站每日的客流量等。

**`INT、INTEGER`** ：取值范围足够大，一般情况下不用考虑超限问题，用得最多。比如商品编号。

**`BIGINT`** ：只有当你处理特别巨大的整数时才会用到。比如双十一的交易量、大型门户网站点击量、证券公司衍生产品持仓等。

### 2.4 如何选择？

在评估用哪种**整数类型**的时候，你需要考虑 **存储空间** 和 **可靠性 平衡**问题：

​	一方面，用占用字节数少的整数类型可以节省存储空间；

​	另一方面，要是为了节省存储空间， 使用的整数类型取值范围太小，一旦遇到超出取值范围的情况，就可能引起 系统错误 ，影响可靠性。

举个例子，**商品编号采用的数据类型是 INT**。原因就在于，客户门店中流通的商品种类较多，而且，每天都有旧商品下架，新商品上架，这样不断迭代，日积月累。如果使用 **SMALLINT 类型**，虽然占用字节数比 INT 类型的整数少，但是却不能保证数据不会超出范围**65535**。相反，使用 INT，就能确保有足够大的取值范围，不用担心数据超出范围影响可靠性的问题。你要注意的是，在实际工作中，**`系统故障产生的成本远远超过增加几个字段存储空间所产生的成本`**。因此，我建议你首先确保数据不会超过取值范围，在这个前提之下，再去考虑如何节省存储空间。

## 3.浮点数类型

### 3.1 类型介绍

> **`浮点数和定点数类型的特点是可以 处理小数`**，你可以把整数看成小数的一个特例。因此，浮点数和定点数的使用场景，比整数大多了。
>
>  MySQL支持的浮点数类型，分别是 **`FLOAT、DOUBLE、REAL`**。

- FLOAT 表示**单精度浮点数**； 4字节，32位
- DOUBLE 表示**双精度浮点数**；8字节，64位

![167514755434222ea3f4947cd6fa4.png](https://img.picgo.net/2023/01/31/167514755434222ea3f4947cd6fa4.png)

- REAL默认就是 DOUBLE。

  如果你把 SQL 模式设定为启用“ REAL_AS_FLOAT ”，那 么，MySQL 就认为REAL 是 FLOAT。如果要启用“REAL_AS_FLOAT”，可以通过以下 SQL 语句实现：SET sql_mode = “REAL_AS_FLOAT”;

  问题1：FLOAT 和 DOUBLE 这两种数据类型的区别是啥呢？

  ​	FLOAT 占用字节数少，取值范围小；DOUBLE 占用字节数多，取值范围也大。

  问题2：为什么浮点数类型的无符号数取值范围，只相当于有符号数取值范围的一半，也就是只相当于有符号数取值范围大于等于零的部分呢？

  ​	MySQL 存储浮点数的格式为： **符号(S) 、 尾数(M) 和 阶码(E)** 。因此，无论有没有符号，MySQL 的浮点数都会存储表示符号的部分

  ​	因此， **所谓的无符号数取值范围，其实就是有符号数取值范围大于等于零的部分。**

### 3.2 数据精度说明

