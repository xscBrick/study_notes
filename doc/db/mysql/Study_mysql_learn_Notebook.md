# Study_mysql_learn_Notebook

[TOC]

row :  行
column： 列

每个数据库文件夹下都有一个opt文件，保存的是对应的数据库选项  ( .opt )。

每当一张数据表创建，那么就会再对应的数据库下创建一些文件 ( .frm 与存储引擎有关)

.frm 代表结构文件

注意：这个结构文件来自于innodb存储引擎，innodb存储引擎所有的文件都存储在外部的ibdata文件中

## DQL:Data Query Language 数据查询



select/show... order by/group by/having...

其语句，也称为“数据检索语句”，用以从表中获得数据，确定数据怎样在应用程序给出。保留字SELECT是DQL（也是所有SQL）用得最多的动词，其他DQL常用的保留字有WHERE，ORDER BY，GROUP BY和HAVING。这些DQL保留字常与其他类型的SQL语句一起使用。

专门用于查询数据：代表指令为select/show

## DML：Data Manipulation Language 数据操作语言

insert/update/delete

其语句包括动词INSERT，UPDATE和DELETE。它们分别用于添加，修改和删除表中的行。也称为动作查询语言。

专门用于写数据：代表指令为，**insert，update和delete**

## TPL 事务处理语言

begin/transaction/commit/rollback

它的语句能确保被**DML**语句影响的表的所有行及时得以更新。TPL语句包括B**EGIN TRANSACTION，COMMIT**和**ROLLBACK**。（不是所有的关系型数据库都提供事务安全处理）

**专门用于事务安全处理**：transaction

## DCL 数据控制语言

grant/revoke

它的语句通过**GRANT**或**REVOKE**获得许可，确定单个用户和用户组对数据库对象的访问。某些RDBMS可用GRANT或REVOKE控制对表单个列的访问。
**专门用于权限管理**：代表指令为grant和revoke

## DDL 数据定义语言

create/ drop

其语句包括动词CREATE和DROP。在数据库中创建新表或删除表（CREAT TABLE 或 DROP TABLE）；为表加入索引等。DDL包括许多与人数据库目录中获得数据有关的保留字。它也是动作查询的一部分。

专门用于结构管理：代表指令create和drop（alter）

## 数据库操作

### 创建数据库 create database

```mysql
create database test; //创建一个 名为 test 的数据库
create database test charset gbk; //charset 字符集
```



### 查看数据库 show 

```mysql
show databases; //显示全部数据库
show databases like ‘my%’; //显示以my 开头的数据库
show create database test；
```



### 选择数据库 use

```mysql
use test; //选择test 数据库
```



### 修改数据库 alter

修改数据库字符集： 字符集（charset） / 校对集 collate

```mysql
alter  database test charset = gbk;
```



### 删除数据库 drop

```mysql
//删库一时爽， drop需谨慎
drop database test；
```



## 数据表操作

> 表选项
>
> engine : 存储引擎， mysqk 提供具体的存储数据的方式，默认有一个 innodb / myisam
>
> charset ： 字符集，只对当前自己表有效（级别高于数据库）
>
> collate :  校对集



### 创建数据表 create table

```mysql
create table 表名（
字段名 字段类型[字段属性],
字段名 字段类型[字段属性],
...
）[表选项];
```

```mysql
create table test.test_table(name varchar(10));
```



### 复制已有表结构 

#### create table new_table_name like old_table_name;



### 显示所有表 show tables；

#### 匹配显示表 show tables like '匹配模式'；

```mysql
show tables like 'c%';
```

#### 显示表结构

本质含义： 显示表钟所包含的字段信息（名字， 类型， 属性等）

```mysql
describe 表名；
desc 表名；
show column from 表名；
```

#### 显示表创建语句 show create table 表名；



## 修改表结构 

### 修改表名： rename table

```mysql
rename table old_table_name to new_tablename;
```



### 修改表选项 alter table

```mysql
// alter table table_name 表选项=新值;
alter table table_name charset=gbk;
```



### 新增字段： alter table table_name add[column]

```mysql
alter table test_table add column age int(10);
//alter table 表名 add [column] 新字段名 列类型 [列属性] [位置first/after 字段名]
```



### 修改字段名 alter table table_name change

alter table 表名 change 旧字段名 新字段名 字段类型 [列属性] [新位置]

#### 修改字段类型（属性）alter table table_name modify column_name 

alter table 表名 modify 字段名 新类型 [新属性] [新位置]

#### 删除字段 alter table table_name drop column_name

### 删除表结构 drop table table_name1[, table_name2 ...]

批量删除： drop tables；

alter table  t_migrate_vbcgw_log modify region varchar(30) 

## 数据操作

### 插入操作 insert into

向表钟指定字段插入数据

insert into 表名[(字段列表)] values(对应字段列表)

```mysql
insert into table_name (name, age) values('jack', 30);
 //后面（values中）对应的值列表只需要与前面的字段列表相对应即可（不一定与表结构完全一致）
insert into table_name (age, name) values(30,'jack');
```

### 向表中所有字段插入数据 insert into

后面（values中）对应的值列表只需要与前面的字段列表相对应即可（不一定与表结构完全一致）

```mysql
insert into table_name values('jack', 30);
```



### 查询操作 select 

```mysql
select * from table_name;
select * from table_name \G;
select namme from table_name \G;
```



### 删除操作  delete

```mysql
delete from table_name where ..
```



### 更新操作 update ... set

```mysql
update table_name set 字段名 = 新值 [where 条件];//如果没有where条件，那么所有的表中对应的那个字段都会被修改成统一值。
```



## 字符集

#### 字符编码： 

字符集(Character set)是多个字符的集合，字符集种类较多，每个字符集包含的字符个数不同。

常见字符集名称：ASCII字符集、GB2312字符集、BIG5字符集、 GB18030字符集、Unicode字符集等。计算机要准确的处理各种字符集文字，需要进行字符编码，以便计算机能够识别和存储各种文字。中文文字数目大，而且还分为简体中文和繁体中文两种不同书写规则的文字，而计算机最初是按英语单字节字符设计的，因此，对中文字符进行编码，是中文信息交流的技术基础。

 

### 设置客户端所有字符集

如果直接通过cmd下的mysql.exe进行中文数据插入，那么可能出错

出错原因：
1、	用户是通过mysql.exe来操作mysqld.exe
2、	真正的SQL执行是Mysqld.exe来执行
3、	mysql.exe将数据传入mysqld.exe的时候，没有告知其对应的符号规则（字符集），而mysqld也没有能力自己判断，就会使用自己默认的（字符集）

解决方案：mysql.exe客户端在进行数据操作之前将自己所使用的字符集告诉mysqld
Cmd下的mysql.exe默认都只有一个字符集：GBK

Mysql.exe如果告知Mysqld.exe对应的字符集类型为gbk？
快捷方式：set names 字符集

重新进行数据插入：中文（GBK）
深层原理：客户端，服务端，连接层（show variables like ‘character_set_%’）
Mysql.exe与Mysqld.exe之间的处理关系一共分为三层
客户端传入数据给服务端：client:character_set_client
服务端返回数据给客户端：server:character_set_results
客户端与服务端之间的连接：connection:character_set_connection

Set names 字符集的本质：就是一次性打通三层关系的字符集，变得一致。
在系统中有三个变量来记录着这三个关系对应的字符集：show variables like ‘character_set_%’;

查看一个新的客户端的对应的字符集关系

### 修改服务器端变量的值

Set 变量名 = 值;

重新进行数据插入和查看的结果：插入OK，但是查看乱码

修改结果字符集为GBK

Connection只是为了更方便客户端与服务端进行字符集转换而设。

Set names gbk;

Set character_set_client = gbk; //为了让服务器识别客户端传来的数据

Set character_set_connection = gbk;//更好的帮助客户端与服务端之间进行字符集转换

Set character_set_results = gbk;//为了告诉客户端服务端所有的返回的数据字符集



# 列属性

列属性又称之为字段属性，在mysql中一共有6个属性：null，默认值，列描述，主键，唯一键和自动增长

### null 属性： 字段为空

注意：
1、	在设计表的时候，尽量不要让数据为空
2、	Mysql的记录长度为65535个字节，如果一个表中有字段允许为NULL，那么系统就会设计保留一个字节来存储NULL，最终有效存储长度为65534个字节

### 默认值 Default：

默认值，当字段被设计的时候，如果允许默认条件下，用户不进行数据的插入，那么就可以使用事先准备好的数据来填充：通常填充的是NULL

### 列描述 comment

是专门用于给开发人员进行维护的一个注释说明
基本语法：comment ‘字段描述’;

### 主键 primary key

在一张表中有且只有一个主键，里面的值具有唯一性

### 创建主键

#### 随表创建主键

系统提供了两种增加主键的方式

方案1：直接在需要当做主键的字段之后，增加 primary key 属性来确定主键

方案2： 在所有字段之后增加 primary key 选项：  primary key (字段信息)

```mysql
//方案1
create table class(
username varchar(10) primary key
)charset utf8;
//方案2
create table class(
username varchar(10),
primary key(username)
)charset utf8;
```

#### 

#### 创建表后增加主键 alter table ...add primary key();

```mysql
create table class_test(
username varchar(10)
)charset utf8;
alter table class_test add primary key(username);
```



#### 删除主键 alter table ... drop primary key()

```mysql
alter table class_test drop primary key(username);
```



#### 复合主键 primary key(column1, column2)

```mysql
create table class_test(
username varchar(10),
class varchar(10),
age int(6),
primary key(unsername, class)
)charset utf8;
alter table class_test add primary key(username);
desc class_test;
```



#### 主键约束 

主键一旦增加，那么对应的字段有如下约束:

> 1. 当前字段对应的数据不能为空；
> 2. 当前字段对应的数据不能有任何重复



#### 主键分类 

业务主键：具有业务意义（学生ID...）

逻辑主键：自然增长的整型

### 自动增长 auto increment

自动增长的原理：

1. 在系统中有维护一组数据，用来保存当前使用了自动增长属性的字段，记住当前对应的数据中，在给定一个指定的步长，
2. 当用户进行数据插入的时候，如果没有给定值，系统在原始值上再加上补偿变成新的数据
3. 自动增长的触发：给定属性的字段没有提供值
4. 自动增长只适用于数值

```mysql
create table auto_increment_test(
id int primary key auto_increment,
    username varchar(10) not null commment '用户名'，
    password varchar(10) not null comment '密码' 
)charset utf8;

//插入数据，验证
insert into auto_increment_test(null, 'Tom', '123456');
```

## 唯一键 unique key

 唯一键：unique key，用来保证对应的字段中的数据唯一的
主键也可以用来保证字段数据唯一性，但是一张表只有一个主键。

1.唯一键在一张表中可以有多个。
2.唯一键允许字段数据为NULL，NULL可以有多个（NULL不参与比较）

### 创建唯一键

```mysql
//方案1
create table class(
username varchar(10) unique
)charset utf8;
//方案2
create table class(
username varchar(10),
unique key(username)
)charset utf8;
```



### 删除唯一键

```mysql
alter table class drop index username;
```

### 修改唯一键 先删除 后增加



# 表关系

表关系：表与表之间（实体）有什么样的关系，每种关系应该如何设计表结构

## 一对一

一张表中一条记录与另外一张表中最多有一条明确的关系，此设计方案保证两张表中使用同样的主键即可

学生表

| 学生ID（PRI） | 姓名 | 年龄 | 性别 | 籍贯 | 婚否 | 住址 |
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
|               |      |      |      |      |      |      |

表的使用过程中：常用的信息会经常去查询，而不常用的信息会偶尔才会用到
解决方案：将两张表拆分，常见的放一张表，不常见的放一张表
常用表

| 学生ID（PRI） | 姓名 | 年龄 | 性别 |
| ------------- | ---- | ---- | ---- |
|               |      |      |      |

不常用表

| 学生ID（PRI） | 籍贯 | 婚否 | 住址 |
| ------------- | ---- | ---- | ---- |
|               |      |      |      |

## 一对多

通常也叫多对一的关系，通常一对多的关系设计的方案，在 多 关系的表中去维护一个字段，这个字段是 一  关系的主键

母亲表

| 母亲ID | 姓名 | 年龄 | 身高 |
| ------ | ---- | ---- | ---- |
| M1     |      |      |      |
| M2     |      |      |      |

孩子表

| 孩子ID | 姓名 | 年龄 | 身高 | 母亲ID |
| ------ | ---- | ---- | ---- | ------ |
| K1     |      |      |      | M1     |
| K2     |      |      |      | M1     |

##  多对多 

增加第三张表，让中间表与对应的其他表形成两个多对一的关系： 多表中 增加 一 表 对应的主键字段

# 高级数据操作

## 多数据插入

insert into 表名 [(字段列表)]
values(值列表), (值列表)…;

## 主键冲突

键冲突：在有的表中，使用的是业务主键（字段有业务含义），但是往往在进行数据插入的时候，又不确定数据表中是否已经存在对应的主键。

解决方案： 更新 /替换

更新：Insert into 表名 [(字段列表)] values(值列表) on duplicate key
update 字段 = 新值;

替换：当主键冲突之后，干掉原来的数据，重新插入进去。

replace into [(字段列表)] values(值列表);

## 蠕虫复制

蠕虫复制：一分为二，成倍的增加。从已有的数据中获取数据，并且将获取到的数据插入到数据表中。

```mysql
insert into 表名 [(字段列表)] select */字段列表 from 表;
```

注意：

1、  蠕虫复制的确通常是重复数据，没有太大业务意义：可以在短期内快速增加表的数据量，从而可以测试表的压力，还可以通过大量数据来测试表的效率（索引）

2、  蠕虫复制虽好，但是要注意主键冲突。

# 更新数据 update set

1、	在更新数据的时候，特别要注意：通常一定是跟随条件更新

```mysql
Update 表名 set 字段名 = 新值 where 判断条件;
```

2、	如果没有条件，是全表更新数据。但是可以使用limit 来限制更新的数量；

```mysql
Update 表名 set 字段名 = 新值 [where 判断条件] limit 数量;
```

# 删除数据

1、	删除数据的时候尽量不要全部删除，应该使用where进行 判定；
2、	删除数据的时候可以使用limit来限制要删除的具体数量

* Delete删除数据的时候无法重置auto_increment

Mysql有一个能够重置表选项中的自增长的语法;

```mysql
truncate 表名;(实现原理：先drop, 再creae)
```

# 查询数据

```mysql
select select选项 字段列表 from 数据源 where条件 group by分组 having条件 order by排序 limit限制;
```

```mysql
All：默认的，表示保存所有的记录
select all * from class;
distinct
select distinct * from class;
select distinct cls.username from class cls;
select * from class1 cls1, class2 cls2;
结果：两张表的记录数相乘，字段数拼接
本质：从第一张表取出一条记录，去拼凑第二张表的所有记录，保留所有结果。得到的结果在数学上有一个专业的说法：笛卡尔积，这个结果出了给数据库造成压力，没有其他意义：应该尽量避免出现笛卡尔积。
#动态查询
select * from (select username,class from class) as cls;

```

### 统计函数：（聚合函数）

count()：统计每组中的数量，如果统计目标是字段，那么不统计为空NULL字段，如果为*那么代表统计记录

avg()：求平均值

sum()：求和

max()：求最大值

min()：求最小值

Group_concat()：为了将分组中指定的字段进行合并（字符串拼接）

```mysql
select class_id, group_concat(stu_name), count(*), max(stu_age), min(stu_height), avg(stu_age) from my_student group by class_id \G;
```



### 回溯统计 rollup

当分组进行多分组之后，往上统计的过程中，需要进行层层上报，将这种层层上报统计的过程称之为回溯统计：每一次分组向上统计的过程都会产生一次新的统计数据，而且当前数据对应的分组字段为NULL。

基本语法：

```mysql
group by 字段 [asc|desc] with rollup;
```

### Having子句

Having的本质和where一样，是用来进行数据条件筛选。

1、	Having是在group by子句之后：可以针对分组数据进行统计筛选，但是where不行
查询班级人数大于等于4个以上的班级
Where不能使用聚合函数：聚合函数是用在group by分组的时候，where已经运行完毕
Having在group by分组之后，可以使用聚合函数或者字段别名（where是从表中取出数据，别名是在数据进入到内存之后才有的）
**强调：**having是在group by之后，group by是在where之后：where的时候表示将数据从磁盘拿到内存，where之后的所有操作都是内存操作。

### 分页

利用limit来限制获取指定区间的数据。

基本语法：

```mysql
limit offset,length;       //offset偏移量：从哪开始，length就是具体的获取多少条记录
```

Mysql中记录的数量从0开始

Limit 0,2; 表示获取前两条记录

## is运算符

is是专门用来判断字段是否为NULL的运算符

基本语法：is null / is not null

## 连接查询

连接查询：将多张表连到一起进行查询（会导致记录数行和字段数列发生改变）

### 连接查询的意义

在关系型数据库设计过程中，实体（表）与实体之间是存在很多联系的。在关系型数据库表的设计过程中，遵循着关系来设计：一对一，一对多和多对多，通常在实际操作的过程中，需要利用这层关系来保证数据的完整性。

### 连接查询分类

连接查询一共有以下几类：

#### 交叉连接 cross join

内连接
外连接：左外连接（左连接）和右外连接（右连接）
自然连接
交叉连接

#### 交叉连接：将两张表的数据与另外一张表彼此交叉

##### 原理

1、	从第一张表依次取出每一条记录
2、	取出每一条记录之后，与另外一张表的全部记录挨个匹配
3、	没有任何匹配条件，所有的结果都会进行保留
4、	记录数 = 第一张表记录数 * 第二张表记录数；字段数 = 第一张表字段数  + 第二张表字段数（笛卡尔积）

##### 语法

基本语法：表1 cross join 表2;

##### 应用

交叉连接产生的结果是笛卡尔积，没有实际应用。
本质：from 表1,表2;

#### 内连接 inner join

内连接：inner join，从一张表中取出所有的记录去另外一张表中匹配：利用匹配条件进行匹配，成功了则保留，失败了放弃。

##### 原理

1、	从第一张表中取出一条记录，然后去另外一张表中进行匹配
2、	利用匹配条件进行匹配：
2.1	匹配到：保留，继续向下匹配
2.2	匹配失败：向下继续，如果全表匹配失败，结束

##### 语法

基本语法：表1 [inner] join 表2 on 匹配条件;

1、	如果内连接没有条件（允许），那么其实就是交叉连接（避免）

```mysql
select * from my_student inner join my_class;
```

2.使用匹配条件进行匹配:        因为表的设计通常容易产生同名字段，尤其是ID，所以为了避免重名出现错误，通常使用表名.字段名，来确保唯一性

3.通常，如果条件中使用到对应的表名，而表名通常比较长，所以可以通过表别名来简化

```mysql
select * from mys_student inner join my_class on class_id = id;
select * from my_student inner jooin my_class on my_student.class_id = my_class.id;
select * from my_student s inner join my_class c on s.class_id = c.id;
```

4.内连接匹配的时候，必须保证匹配到才会保存

5.内连接因为不强制必须使用匹配条件（on）因此可以在数据匹配完成之后，使用where条件来限制，效果与on一样（建议使用on）

##### 应用

内连接通常是在对数据有精确要求的地方使用：必须保证两种表中都能进行数据匹配。

#### 外连接

外链接：outer join，按照某一张表作为主表（表中所有记录在最后都会保留），根据条件去连接另外一张表，从而得到目标数据。

外连接分为两种：左外连接（left join），右外连接（right join）
左连接：左表是主表
右连接：右表是主表

##### 原理

1、	确定连接主表：左连接就是left join左边的表为主表；right join就是右边为主表
2、	拿主表的每一条记录，去匹配另外一张表（从表）的每一条记录
3、	如果满足匹配条件：保留；不满足即不保留
4、	如果主表记录在从表中一条都没有匹配成功，那么也要保留该记录：从表对应的字段值都未NULL

##### 语法

基本语法：
左连接：主表 left join 从表 on 连接条件;
右连接：从表 right join 主表 on连接条件;

左连接对应的主表数据在左边；右连接对应的主表数据在右边：

```mysql
select * from my_student as s right join my_class as c on s.class_id = c.class_id;
```



##### 特点

1、	外连接中主表数据记录一定会保存：连接之后不会出现记录数少于主表（内连接可能）
2、	左连接和右连接其实可以互相转换，但是数据对应的位置（表顺序）会改变

##### 应用

非常常用的一种获取的数据方式：作为数据获取对应主表以及其他数据（关联）

#### Using关键字

是在连接查询中用来代替对应的on关键字的，进行条件匹配。

##### 原理

1、	在连接查询时，使用on的地方用using代替
2、	使用using的前提是对应的两张表连接的字段是同名（类似自然连接自动匹配）
3、	如果使用using关键字，那么对应的同名字段，最终在结果中只会保留一个。

##### 语法

基本语法：表1 [inner,left,right] join 表2 using(同名字段列表); //连接字段

```mysql
select * from my_student as s right join my_class as c using class_id;
```



## 子查询 sub query

子查询是一种常用计算机语言SELECT-SQL语言中嵌套查询下层的程序模块。当一个查询是另一个查询的条件时，称之为子查询。

子查询：指在一条select语句中，嵌入了另外一条select语句，那么被嵌入的select语句称之为子查询语句
主查询：主要的查询对象，第一条select语句，确定的用户所有获取的数据目标（数据源），以及要具体得到的字段信息。

### 子查询和主查询的关系

1、	子查询是嵌入到主查询中的；
2、	子查询的辅助主查询的：要么作为条件，要么作为数据源
3、	子查询其实可以独立存在：是一条完整的select语句

#### 子查询分类

##### 按功能分

标量子查询：子查询返回的结果是一个数据（一行一列）
列子查询：返回的结果是一列（一列多行）
行子查询：返回的结果是一行（一行多列）
表子查询：返回的结果是多行多列（多行多列）
Exists子查询：返回的结果1或者0（类似布尔操作）

##### 按位置分

​	Where子查询：子查询出现的位置在where条件中
​	From子查询：子查询出现的位置在from数据源中（做数据源）

### 标量子查询

子查询得到结果是一个数据（一行一列）

##### 语法

基本语法：select * from 数据源 where 条件判断 =/<> (select 字段名 from 数据源 where 条件判断); //子查询得到的结果只有一个值

```mysql
select * from my_class where class_id = (select class_id from my_student where stu_name = '张三');
```

### 列子查询

子查询得到的结果是一列数据（一列多行）

##### 语法

主查询 where 条件 in (列子查询);

```mysql
select name from my_classs where class_id in (select class_id from my_student);
```

### 行子查询

子查询返回的结果是一行多列

##### 行元素

字段元素是指一个字段对应的值，行元素对应的就是多个字段：多个字段合起来作为一个元素参与运算，把这种情况称之为行元素。

##### 基本语法：

主查询 where 条件[（构造一个行元素）] = (行子查询);

```mysql
select * from my_student where (stu_age, stu_height) = (select max(stu_age), max(stu_height) from my_student);
```

### 表子查询

子查询返回的结果是多行多列，表子查询与行子查询非常相似，只是行子查询需要产生行元素，而表子查询没有。
行子查询是用于where条件判断：where子查询
表子查询是用于from数据源：from子查询

##### 基本语法：

**Select 字段表 from (表子查询) as 别名 [where] [group by] [having] [order by] [limit];**

```mysql
select * from (select * from my_student order by stu_height desc) as temp group by class_id;
```

### Exists子查询

查询返回的结果只有0或者1，1代表成立，0代表不成立

##### 基本语法：

where exists(查询语句); //exists就是根据查询得到的结果进行判断：如果结果存在，那么返回1，否则返回0

Where 1：永远为真

```mysql
select * from my_class as c where exits(select stu_id from my_student as s where s.class_id = c.class_id);
```

# 整库数据备份与还原

整库数据备份也叫SQL数据备份：备份的结果都是SQL指令

在Mysql中提供了一个专门用于备份SQL的客户端：**mysqldump.exe**

##### 应用场景

SQL备份是一种mysql非常常见的备份与还原方式，SQL备份不只是备份数据，还备份对应的SQL指令（表结构）：即便是数据库遭到毁灭性的破坏（数据库被删），那么利用SQL备份依然可以实现数据还原。

SQL备份因为需要备份结构，因此产生的备份文件特别大，因此不适合特大型数据备份，也不适合数据变换频繁型数据库备份。

##### 应用方案

SQL备份
SQL备份用到的是专门的备份客户端，因此还没与数据库服务器进行连接。

基本语法：mysqldump/mysqldump.exe   -hPup   数据库名字 [表1   [表2…]]  >  备份文件地址

备份可以有三种形式：
1、	整库备份（只需要提供数据库名字）
2、	单表备份：数据库后面跟一张表
3、	多表备份：数据库后跟多张表

```mysql
//1
mysqldump.exe -hlocalhost -p3306 -uroot -proot mydatabase2 > c:/server/temp/mydatabase2.sql
//2
//3
msyqldump -uroot -proot mydatabae2 my_student my_class c:/server/temp/student_int.sql
```

## 数据还原

Mysql提供了多种方式来实现：两种
Mysqldump备份的数据中没有关于数据库本身的操作，都是针对表级别的操作：当进行数据（SQL还原），必须指定数据库

1、	利用mysql.exe客户端：没有登录之前，可以直接用该客户端进行数据还原
Mysql.exe –hPup 数据库 < 文件位置
2、	在SQL指令，提供了一种导入SQL指令的方式
Source  SQL文件位置;		//必须先进入到对应的数据库
3、	人为操作：打开备份文件，复制所有SQL指令，然后到mysql.exe客户端中去粘贴执行。（不推荐）

```mysql
//1
mysql -uroot -proot mydb < c:server/temp/mydatabase2.sql;
//2
source c:/server/temp/student_int.sql;
```

# 用户权限管理

用户权限管理：在不同的项目中给不同的角色（开发者）不同的操作权限，为了保证数据库数据的安全。
通常，一个用户的密码不会长期不变，所以需要经常性的变更数据库用户密码来确保用户本身安全（mysql客户端用户）

## 用户管理

Mysql需要客户端进行连接认证才能进行服务器操作：需要用户信息。Mysql中所有的用户信息都是保存在mysql数据库下的user表中。

```mysql
select * from mysql.user \G;
```

默认的，在安装Mysql的时候，如果不选择创建匿名用户，那么意味着所有的用户只有一个：root超级用户
在mysql中，对用的用户管理中，是由对应的Host和User共同组成主键来区分用户。
User：代表用户的用户名
Host：代表本质是允许访问的客户端（IP或者主机地址）。如果host使用%代表所有的用户（客户端）都可以访问

```mysql
desc mysql.user;
```

### 创建用户

理论上讲可以采用两种方式创建用户：
1、	直接使用root用户在mysql.user表中插入记录（不推荐）
2、	专门创建用户的SQL指令
基本语法：create user 用户名 identified by ‘明文密码’;
用户：用户名@主机地址
主机地址：’’ / ‘%’

```mysql
create user 'user1'@'%' identified by '123456';
//
```

### 删除用户

注意：mysql中user是带着host本身的（具有唯一性）
基本语法：drop user 用户名@host;

### 修改用户密码

Mysql中提供了多种修改的方式：基本上都必须使用对应提供的一个系统函数：password()，需要靠该函数对密码进行加密处理。

##### 1、	使用专门的修改密码的指令

基本语法：set password for 用户 = password(‘新的明文密码’);

##### 2、	使用更新语句update来修改表

基本语法：update mysql.user set password = password(‘新的明文密码’) where user = ‘’ and host= ‘’;

### 权限管理

在mysql中将权限管理分为三类：
1、	数据权限：增删改查（select\update\delete\insert）
2、	结构权限：结构操作（create\drop）
3、	管理权限：权限管理（create user\grant\revoke）：通常只给管理员如此权限

### 授予权限：grant

将权限分配给指定的用户
基本语法：grant 权限列表 on 数据库/*.表名/* to 用户;
权限列表：使用逗号分隔，但是可以使用all privileges代表全部权限
数据库.表名：可以是单表（数据库名字.表名），可以是具体某个数据库（数据库.*），也可以整库（*.*）

```mysql
grant select on mydb.my_student to 'user1'@'%';
//用户被分配权限以后不需要退出就可以看到效果
show databases;
show tables;
```

### 取消权限：revoke

权限回收：将权限从用户手中收回
基本语法：revoke 权限列表/all privileges on 数据库/*.表/* from 用户;

```mysql
revoke all privileges on mydb.my_student from 'user1'@'%';
```

### 刷新权限：flush

Flush：刷新，将当前对用户的权限操作，进行一个刷新，将操作的具体内容同步到对应的表中。
基本语法：flush privileges;

### 密码丢失的解决方案

如果忘记了root用户密码，就需要去找回或者重置root用户密码

1、	停止服务
2、	重新启动服务：mysqld.exe –skip-grant-tables //启动服务器但是跳过权限
3、	当前启动的服务器没有权限概念：非常危险，任何客户端，不需要任何用户信息都可以直接登录，而且是root权限：新开客户端，使用mysql.exe登录即可
4、	修改root用户的密码：指定 用户名@host
5、	赶紧关闭服务器，重启服务

## 外键

如果公共关键字在一个关系中是主关键字，那么这个公共关键字被称为另一个关系的外键。由此可见，外键表示了两个关系之间的相关联系。以另一个关系的外键作主关键字的表被称为主表，具有此外键的表被称为主表的从表。外键又称作外关键字。

**外键：foreign key**
一张表（A）中有一个字段，保存的值指向另外一张表（B）的主键
B：主表
A：从表

### 外键的操作

### 增加外键

Mysql中提供了两种方式增加外键

##### 方案1：在创建表的时候增加外键（类似主键）

基本语法：在字段之后增加一条语句
[constraint `外键名`] foreign key(外键字段) references 主表(主键);

```mysql
create table my_foreign(
id int primary key auto_increment,
name varchar(10) not null,
--关联班级 my_class
class_id int,
--增加外键
foreign key(class_id) references my_class(class_id)
)charset utf8;
desc my_foreign;
```

MUL：多索引，外键本身是一个索引，外键要求外键字段本身也是一种普通索引

##### 方案2：在创建表后增加外键

Alter table 从表 add [constraint `外键名`] foreign key(外键字段) references 主表(主键);

```mysql
alter table my_student add constraint 'student_class' foreign key(class_id) references my_class(class_id);
```

修改&删除外键
外键不允许修改，只能先删除后增加
基本语法：alter table 从表 drop foreign key 外键名字;

```mysql
alter table my_student drop foreign key 'student_class_ibfk_1'
```

外键创建会自动增加一个索引，但是外键删除值会删除自己，不会删除索引
外键不能删除产生的普通索引，只会删除外键自己
如果想删除对应的索引：alter table 表名 drop index 索引名字;

##### 外键基本要求

1、	外键字段需要保证与关联的主表的主键字段类型完全一致；
2、	基本属性也要相同
3、	如果是在表后增加外键，对数据还有一定的要求（从表数据与主表的关联关系）
4、	外键只能使用innodb存储引擎：myisam不支持

##### 外键约束

外键约束：通过建立外键关系之后，对主表和从表都会有一定的数据约束效率。

##### 约束的基本概念

1、	当一个外键产生时：外键所在的表（从表）会受制于主表数据的存在从而导致数据不能进行某些不符合规范的操作（不能插入主表不存在的数据）；
2、	如果一张表被其他表外键引入，那么该表的数据操作就不能随意：必须保证从表数据的有效性（不能随便删除一个被从表引入的记录）

##### 外键约束的概念

可以在创建外键的时候，对外键约束进行选择性的操作。

基本语法： add foreign key(外键字段) references 主表(主键)  on 约束模式;

##### 约束模式有三种：

1、	district：严格模式，默认的，不允许操作
2、	cascade：级联模式，一起操作，主表变化，从表数据跟着变化
3、	set null：置空模式，主表变化（删除），从表对应记录设置为空：前提是从表中对应的外键字段允许为空

**外键约束主要约束的对象是主表操作：从表就是不能插入主表不存在的数据**

通常在进行约束时候的时候，需要指定操作：update和delete
常用的约束模式： on update cascade, on delete set null，更新级联，删除置空

##### 约束作用

保证数据的完整性：主表与从表的数据要一致

正是因为外键有非常强大的数据约束作用，而且可能导致数据在后台变化的不可控。导致程序在进行设计开发逻辑的时候，没有办法去很好的把握数据（业务），所以外键比较少使用。

# 视图基本操作

### 创建视图

视图的本质是SQL指令（select语句）
基本语法：create view 视图名字 as select指令;	//可以是单表数据，也可以是连接查询，联合查询或者子查询

```mysql
create view student_class_v as 
select s.*, c.name from my_student as s left join
my_class as c
on
s.class_id = c.class_id;
```

查看视图结构：视图本身是虚拟表，所以关于表的一些操作都适用于视图
Show tables/show create table[view]/desc 视图名字；

```mysql
desc student_class_v;
show create view student_class_v \G;
```



### 使用视图

视图是一张虚拟表：可以直接把视图当做“表”操作，但是视图本身没有数据，是临时执行select语句得到对应的结果。视图主要用户查询操作。

基本语法：select 字段列表 from 视图名字 [子句];

```mysql
select * from student_class_v;
```



### 修改视图

修改视图：本质是修改视图对应的查询语句
基本语法：alter view 视图名字 as 新select指令;

```mysql
alter view student_class_v as 
select * from my_student as s left join
my_class as c
using(class_id);
```



### 删除视图

基本语法：drop view 视图名字;

```mysql
drop view student_class_v;
```



# 事务安全 Transaction

##### 事务概念

事务(Transaction)是访问并可能更新数据库中各种数据项的一个程序执行单元(unit)。事务通常由高级数据库操纵语言或编程语言书写的用户程序的执行所引起。事务由事务开始(begin transaction)和事务结束(end transaction)之间执行的全体操作组成。

##### 事务基本原理

基本原理：Mysql允许将事务统一进行管理（存储引擎INNODB），将用户所做的操作，暂时保存起来，不直接放到数据表（更新），等到用于确认结果之后再进行操作。
事务在mysql中通常是自动提交的，但是也可以使用手动事务。

![1571323592145](C:\Users\22909\AppData\Roaming\Typora\typora-user-images\1571323592145.png)

### 自动事务

自动事务：autocommit，当客户端发送一条SQL指令（写操作：增删改）给服务器的时候，服务器在执行之后，不用等待用户反馈结果，会自动将结果同步到数据表。

证明：利用两个客户端，一个客户端执行SQL指令，另外一个客户端查看执行结果

自动事务：系统做了额外的步骤来帮助用户操作，系统是通过变量来控制的。Autocommit
Show variables like ‘autocommit%’;

关闭自动事务：关闭之后系统就不在帮助用户提交结果了
Set autocommit = Off;

```mysql
show variables like 'autocommit';
set autocommit = off;
```

一旦自动事务关闭，那么需要用户提供是否同步的命令
Commit：提交（同步到数据表：事务也会被清空）
Rollback：回滚（清空之前的操作，不要了）
事务没有提交的对比查看：在执行事务端的客户端中，系统在进行数据查看的时候会利用事务日志中保存的结果对数据进行加工
通常，我们不会关闭自动事务：这样操作太麻烦。因此只会在需要使用事务处理的时候，才会进行操作（手动事务）

### 手动事务

手动事务：不管是开始还是过程还是结束都需要用户（程序员），手动的发送事务操作指令来实现。

手动事务对应的命令：
1、	start transaction; //开启事务：从这条语句开始，后面的所有语句都不会直接写入到数据表（保存在事务日志中）
2、	事务处理：多个写指令构成
3、	事务提交：commit/rollback，到这个时候所有的事务才算结束

#### 开启事务

```mysql
start transaction;
```



#### 执行事务

将多个连续的但是是一个整体的SQL指令，逐一执行
1、	事务操作1：新增数据
2、	事务操作2：更新数据

#### 提交事务

确认提交：commit，数据写到数据表（清空）


```mysql
insert into my_class values(6, '6班');
select * from my_class;
update my_student set class_id=6 where stu_id='stu0007';
select * from my_student;
commit; --提交事务
```

## 回滚操作：rollback，所有数据无效并清空

### 回滚点 savepoint

回滚点：savepoint，当有一系列事务操作时，而其中的步骤如果成功了，没有必要重新来过，可以在某个点（成功），设置一个记号（回滚点），然后如果后面有失败，那么可以回到这个记号位置。

增加回滚点：savepoint 回滚点名字; //字母数字和下划线构成
回到回滚点：rollback to 回滚点名字; //那个记号（回滚点）之后的所有操作没有了

注意：在一个事务处理中，如果有很多个步骤，那么可以设置多个回滚点。但是如果回到了前面的回滚点，后面的回滚点就失效；

1、	增加回滚点操作
2、	出现错误步骤
3、	回到正确点：回滚

### 事务特点

事务应该具有4个属性：**原子性、一致性、隔离性、持久性**。这四个属性通常称为ACID特性。

##### 原子性（atomicity）

一个事务是一个不可分割的工作单位，事务中包括的诸操作要么都做，要么都不做。

事务从start transaction起到提交事务（commit或者rollback），要么所有的操作都成功，要么就是所有的操作都失败；

##### 一致性（consistency）

事务必须是使数据库从一个一致性状态变到另一个一致性状态。一致性与原子性是密切相关的。
数据表中的数据修改，要么是所有操作一次性修改，要么是根本不懂

##### 隔离性（isolation）

一个事务的执行不能被其他事务干扰。即一个事务内部的操作及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能互相干扰。
	如果一个客户端在使用事务操作一个数据（可能是一行/整表）的时候，另外一个客户端不能对该数据进行操作

**什么时候是行被隔离？什么时候是整表被隔离？**
说明：如果条件中使用了索引（主键），那么系统是根据主键直接找到某条记录，这个时候与其他记录无关，那么只隔离一条记录；反之，如果说系统是通过全表检索（每一条记录都去检查：没有索引），被检索的所有数据都会被锁定（整表）

##### 持久性（durability）

持久性也称永久性（permanence），指一个事务一旦提交，它对数据库中数据的改变就应该是永久性的。接下来的其他操作或故障不应该对其有任何影响。

# 变量

Mysql本质是一种编程语言，需要很多变量来保存数据。Mysql中很多的属性控制都是通过mysql中固有的变量来实现的。

### 系统变量

系统内部定义的变量，系统变量针对所有用户（MySQL客户端）有效。
查看系统所有变量：show variables [like ‘pattern’];

```mysql
show variables like ‘pattern’;
```

Mysql允许用户使用select查询变量的数据值（系统变量）
基本语法：select @@变量名;

```mysql
select @@autocommit;
```

修改系统变量：分为两种修改方式
1、	局部修改（会话级别）：只针对当前自己客户端当次连接有效
基本语法：set 变量名 = 新值;
2、	全局修改：针对所有的客户端，“所有时刻”都有效
基本语法：set global 变量名 = 值; || set @@global.变量名 = 值;

```mysql
set autocommit = 0;
set global autocommit = 0;
set @@global.auto_increment_increment = 2;
```



全局修改之后：所有连接的客户端并没发现改变？全局修改只针对新客户端生效（正在连着的无效）



注意：如果想要本次连接对应的变量修改有效，那么不能使用全局修改，只能使用会话级别修改（set 变量名 = 值）;

### 会话变量

会话变量也称之为用户变量，会话变量跟mysql客户端是绑定的，设置的变量，只对当前用户使用的客户端生效。

定义用户变量：set @变量名 = 值;


在mysql中因为没有比较符号==，所以是用=代替比较符号：有时候在赋值的时候，会报错：mysql为了避免系统分不清是赋值还是比较：特定增加一个变量的赋值符号：  :=
Set @变量名 := 值;


Mysql是专门存储数据的：允许将数据从表中取出存储到变量中：查询得到的数据必须只能是一行数据（一个变量对应一个字段值）：Mysql没有数组。
1、	赋值且查看赋值过程：select @变量1 := 字段1，@变量2 := 字段2 from 数据表 where 条件；

错误语法：就是因为使用=，系统会当做比较符号来处理

正确处理：使用:=




2、	只赋值，不看过程：select 字段1，字段2… from 数据源 where条件 into @变量1，@变量2…

查看变量：select @变量名;

```mysql
select @name := stu_name, @age := stu_age from my_student limit 1;
--2.
select stu_name, stu_age from my_student order by stu_height desc limit 1 into @name,@age;
select @name, @age;
```

### 局部变量  declare

作用范围在begin到end语句块之间。在该语句块里设置的变量，declare语句专门用于定义局部变量。

1、	局部变量是使用declare关键字声明
2、	局部变量declare语句出现的位置一定是在begin和end之间（beginend是在大型语句块中使用：函数/存储过程/触发器）
3、	声明语法：declare 变量名 数据类型 [属性];
流程结构
流程结构：代码的执行顺序

## If分支

基本语法
If在Mysql中有两种基本用法

1、	用在select查询当中，当做一种条件来进行判断
基本语法：if(条件,为真结果,为假结果)

```mysql
select *, if(stu_age > 20, '符合', '不符合') as judge from my_student;
```

2、	用在复杂的语句块中（函数/存储过程/触发器）
基本语法

If  条件表达式  then 
	满足条件要执行的语句;
End  if;
复合语法
复合语法：代码的判断存在两面性，两面都有对应的代码执行。
基本语法：

If  条件表达式  then
	满足条件要执行的语句;
Else
	不满足条件要执行的语句;
//如果还有其他分支（细分），可以在里面再使用if
	If 条件表达式 then
		//满足要执行的语句
	End if;
End  if;

## While循环

基本语法
循环体都是需要在大型代码块中使用
基本语法

While 条件 do
	要循环执行的代码;
End while;

## 结构标识符

结构标识符：为某些特定的结构进行命名，然后为的是在某些地方使用名字

基本语法

标识名字:While 条件 do
循环体
End while [标识名字];

标识符的存在主要是为了循环体中使用循环控制。在mysql中没有continue和break，有自己的关键字替代：
Iterate：迭代，就是以下的代码不执行，重新开始循环（continue）
Leave：离开，整个循环终止（break）

```mysql
标识名字:While 条件 do
	 If 条件判断 then
		循环控制;
		Iterate/leave 标识名字;
	End if;
循环体
End while [标识名字];
```

# 函数

在mysql中，函数分为两类：系统函数（内置函数）和自定义函数
不管是内置函数还是用户自定义函数，都是使用select 函数名(参数列表);

## 内置函数



| 字符串函数      |                                                              |
| --------------- | ------------------------------------------------------------ |
| Char_length()： | 判断字符串的字符数 Length()：判断字符串的字节数（与字符集）  |
| Concat()：      | 连接字符串 Instr()：判断字符在目标字符串中是否存在，存在返回其位置，不存在返回0 |
| Lcase()：       | 全部小写 Left()：从左侧开始截取，直到指定位置（位置如果超过长度，截取所有） |
| Ltrim()：       | 消除左边对应的空格 Mid()：从中间指定位置开始截取，如果不指定截取长度，直接到最后 |

```mysql
select char_length('你好中国'), length('你好中国');
select concat('你好', '中国'), insert('你好中国', '中'), insert('你好中国', '万');
seledct lcass('aBcD'), left('你好中国',2);
select ltrim('   a bdc'), mid('你好中国', 2);

```

| 时间函数                                |                                                              |
| --------------------------------------- | ------------------------------------------------------------ |
| Now()：                                 | 返回当前时间，日期 时间 Curdate()：返回当前日期 Curtime()：返回当前时间 |
| Datediff()：                            | 判断两个日期之间的天数差距，参数日期必须使用字符串格式（用引号） |
| Date_add(日期,interval 时间数字 type)： | 进行时间的增加 	Type:day/hour/minute/second               |
| Unix_timestamp()：                      | 获取时间戳                                                   |
| From_unixtime()                         | ：将指定时间戳转换成对应的日期时间格式                       |
|                                         |                                                              |

```mysql
select now(),curdate(),curtime();
select datediff('2101-10-10', '1990-10-10');
select date_add('2000-10-10', interval 10 day), date_add('2000-10-10', interval 10 year), date_add('2000-10-10', interval 10 second);

select unix_timestamp();
select from_unixtime();

```

### 数学函数

Abs()：绝对值
Ceiling()：向上取整
Floor()：向下取整
Pow()：求指数，谁的多少次方
Rand()：获取一个随机数（0-1之间）
Round()：四舍五入函数

```mysql
select abs(-1),  ceiling(1.1), floor(1.1), pow(2,4), rand(), round(1.5);
```

### 其他函数

Md5()：对数据进行md5加密（mysql中的md5与其他任何地方的md5加密出来的内容是完全相同的）
Version()：获取版本号
Databse()：显示当前所在数据库
UUID()：生成一个唯一标识符（自增长）：自增长是单表唯一，UUID是整库（数据唯一同时空间唯一）

```mysql
select md5('a'), version(), database(), uuid();
```



### 自定义函数

自定义函数：用户自己定义的函数
函数：实现某种功能的语句块（由多条语句组成）

1、	函数内部的每条指令都是一个独立的个体：需要符合语句定义规范：需要语句结束符分号；
2、	函数是一个整体，而且函数是在调用的时候才会被执行，那么当设计函数的时候，意味着整体不能被中断；
3、	Mysql一旦见到语句结束符分号，就会自动开始执行

解决方案：在定义函数之前，尝试修改临时的语句结束符
基本语法：delimiter
修改临时语句结束符：delimiter 新符号[可以使用系统非内置即可$$]
中间为正常SQL指令：使用分号结束（系统不会执行：不认识分号）
使用新符号结束
修改回语句结束符：delimiter ;

### 创建函数

自定义函数包含几个要素：function关键字，函数名，参数（形参和实参[可选]），确认函数返回值类型，函数体，返回值

函数定义基本语法：
修改语句结束符
Create function 函数名(形参) returns 返回值类型
Begin
	//函数体
	Return 返回值数据;	//数据必须与结构中定义的返回值类型一致
End
语句结束符
修改语句结束符（改回来）

```mysql
delimiter $$ --修改语句结束符
create function my_funcl() returns int
begin
return 10;
end
$$--结束
delimiter ;--修改语句结束符（改回来）
```

并不是所有的函数都需要begin和end：如果函数体本身只有一条指令（return），那么可以省略begin和end

```mysql
--最简函数
create function my_func() returns int
return 100;
```

形参：在mysql中需要为函数的形参指定数据类型（形参本身可以有多个）
基本语法：变量名 字段类型

```mysql
create function my_func(int_1 int, int_2 int) returns int
return int_1 * int_2;
```



#### 查看函数

1、	可以通过查看function状态，查看所有的函数
Show function status [like ‘pattern’];

```mysql
show function status \G;
```

2、	查看函数的创建语句：show create function 函数名字;

```mysql
show create function my_func1 \G;
```

#### 调用函数

自定义函数的调用与内置函数的调用是一样的：select 函数名(实参列表)；

```mysql
select my_func1(), my_func2(), my_func(100, 1000);
```



#### 删除函数

删除函数：drop function 函数名;

```mysql
drop function my_func1;
show function status \G;
```

注意事项
1、	自定义函数是属于用户级别的：只有当前客户端对应的数据库中可以使用
2、	可以在不同的数据库下看到对应的函数，但是不可以调用

```mysql
select my_func2();
```

3、	自定义函数：通常是为了将多行代码集合到一起解决一个重复性的问题
4、	函数因为必须规范返回值：那么在函数内部不能使用select指令：select一旦执行就会得到一个结果（result set）：select 字段 into @变量;（唯一可用）

# 函数流程结构案例

需求：从1开始，直到用户传入的对应的值为止，自动求和：凡是5的倍数都不要。

设计：
1、	创建函数
2、	需要一个形参：确定要累加到什么位置

```mysql
delimiter $$
create function my_sum(end_value int) returns int
begin

end
$$
delimiter
```

3、	需要定义一个变量来保存对应的结果：set @变量名;
使用局部变量来操作：此结果是在函数内部使用
Declare 变量名 类型 [= 默认值];

4、	内部需要一个循环来实现迭代累加

```mysql
delimiter $$
create function my_sum(end_value int) returns int
begin
	--声明变量（局部变量）：如果使用 declare 声明变量：必须再函数体其他语句之前
	declare res int default 0;
	declare i int default 1;
	--循环处理
	while i <= end_value do
		--修改变量：累加
		set res = res + i; --mysql中没有++
		set i = i + 1;
	end while;
end
$$
delimiter
```



5、	循环内部需要进行条件判断控制：5的倍数

```mysql
delimiter $$
create function my_sum(end_value int) returns int
begin
	--声明变量（局部变量）：如果使用 declare 声明变量：必须再函数体其他语句之前
	declare res int default 0;
	declare i int default 1;
	--循环处理
	mywhile : while i <= end_value do
		--判断当前数据是否合理
		if i % 5 = 0 then
			--5的倍数不要
			set i = i + 1;
			iterate my while;
		end if;
		--修改变量：累加
		set res = res + i; --mysql中没有++
		set i = i + 1;
	end while mywhile;
	return res; --返回值
end
$$
delimiter
```

6、	函数必须有返回值


定义函数结构完成

调用函数：select 函数名(实参);

```mysql
select my_sum(100), my_sum(-100);
```

## 变量作用域

变量作用域：变量能够使用的区域范围

#### 局部作用域 declare

使用declare关键字声明（在结构体内：函数/存储过程/触发器），而且只能在结构体内部使用

1、	declare关键字声明的变量没有任何符号修饰，就是普通字符串，如果在外部访问该变量，系统会自动认为是字段

### 会话作用域 @

用户定义的，使用@符号定义的变量，使用set关键字

会话作用域：在当前用户当次连接有效，只要在本连接之中，任何地方都可以使用（可以在结构内部，也可以跨库）

会话变量可以在函数内部使用

会话变量可以跨库

```mysql
set @name = '张三';
create function my_func4() returns char(4)
return @name;
```



### 全局作用域 set global

所有的客户端所有的连接都有效：需要使用全局符号来定义
Set global 变量名 = 值;
Set @@global.变量名 = 值;

通常，在SQL编程的时候，不会使用自定义变量来控制全局。一般都是定义会话变量或者在结构中使用局部变量来解决问题。

## 存储过程 Stored Procedure

### 存储过程概念

存储过程（Stored Procedure）是在大型数据库系统中，一组为了完成特定功能的SQL 语句集，存储在数据库中，经过第一次编译后再次调用不需要再次编译（效率比较高），用户通过指定存储过程的名字并给出参数（如果该存储过程带有参数）来执行它。存储过程是数据库中的一个重要对象（针对SQL编程而言）。

存储过程：简称过程

### 与函数的区别

#### 相同点

1、	存储过程和函数目的都是为了可重复地执行操作数据库的sql语句的集合。
2、	存储过程函数都是一次编译，后续执行

#### 不同点

1、标识符不同。函数的标识符为FUNCTION，过程为：PROCEDURE。
2、函数中有返回值，且必须返回，而过程没有返回值。
3、过程无返回值类型，不能将结果直接赋值给变量；函数有返回值类型，调用时，除在select中，必须将返回值赋给变量。
4、函数可以在select语句中直接使用，而过程不能：函数是使用select调用，过程不是。

### 存储过程操作

#### 创建过程

基本语法
Create procedure 过程名字([参数列表])
Begin
	过程体
End
结束符

如果过程体中只有一条指令，那么可以省略begin和end

```mysql
create procedure my_pro1()
select * from my_student;
```

过程基本上也可以完成函数对应的所有功能

```mysql
delimiter $$
create procedure my_pro2()
begin
--求1-100之间的和
declare i int default 1;
--declare sum int default 0;
set @sum = 0;
while i <= 100 do --开始循环获取结果
	set @sum = @sum + i;
	set i = i + 1;
end while;
select @sum;
$$

delimiter ;

```

#### 

#### 查看过程

查看过程与查看函数完全一样：除了关键字

查看全部存储过程：show procedure status [like ‘pattern’];

查看过程创建语句：show create procedure 过程名字;

```mysql
show procedure status \G;
show create procedure my_pro2;

```

#### 调用过程

过程：没有返回值，select不可能调用

调用过程有专门的语法：call 过程名([实参列表]);



```mysql
call my_pro2();
```




#### 删除过程

基本语法：drop procedure 过程名字;



```mysql
drop procedure my_pro2();
show procedure status \G;
```




### 存储过程的形参类型

存储过程也允许提供参数（形参和实参）：存储的参数也和函数一样，需要指定其类型。

但是存储过程对参数还有额外的要求：自己的参数分类

#### in

表示参数从外部传入到里面使用（过程内部使用）：可以是直接数据也可以是保存数据的变量

#### out

表示参数是从过程里面把数据保存到变量中，交给外部使用：传入的必须是变量
如果说传入的out变量本身在外部有数据，那么在进入过程之后，第一件事就是被清空，设为NULL

#### inout

数据可以从外部传入到过程内部使用，同时内部操作之后，又会将数据返还给外部。

参数使用级别语法（形参）
过程类型  变量名  数据类型; //in int_1 int

```mysql
delimiter $$
create procedure my_pro3(in int_1 int, out int_2 int, inout int_3, int)
begin
select int_1, int_2, int_3;--查看三个传入进来的数据值
--修改三个变量的值
set int_1 = 10;
set int_2 = 100;
set int_3 = 1000;
select int_1, int_2, int_3;
select @n1, @n2, @n3; --查看会话变量
set @n1 = 'a';
set @n2 = 'b';
set @n3 = 'c';
select @n1, @n2, @n3;
end 
$$
--Query OK,
delimiter ;
```


分析结果：out类型的数据会被清空，其他正常


在执行过程之后，再次查看会话变量（外部）

# 触发器  trigger  

#### 触发器概念

##### 	基本概念

触发器是一种特殊类型的存储过程，它不同于我们前面介绍过的存储过程。触发器主要是通过事件进行触发而被执行的，而存储过程可以通过存储过程名字而被直接调用。

触发器：trigger，是一种非常接近于js中的事件的知识。提前给某张表的所有记录（行）绑定一段代码，如果改行的操作满足条件（触发），这段提前准备好的代码就会自动执行。

##### 	作用

1、可在写入数据表前，强制检验或转换数据。（保证数据安全）
2、触发器发生错误时，异动的结果会被撤销。（如果触发器执行错误，那么前面用户已经执行成功的操作也会被撤销：事务安全）
3、部分数据库管理系统可以针对数据定义语言（DDL）使用触发器，称为DDL触发器。
4、可依照特定的情况，替换异动的指令 (INSTEAD OF)。（mysql不支持）

#### 	触发器优缺点

##### 优点

1、	触发器可通过数据库中的相关表实现级联更改。（如果某张表的数据改变，可以利用触发器来实现其他表的无痕操作[用户不知道]）
2、	保证数据安全：进行安全校验

##### 缺点

1、	对触发器过分的依赖，势必影响数据库的结构，同时增加了维护的复杂程度。
2、	造成数据在程序层面不可控。（PHP层）
触发器基本语法
创建触发器
基本语法
Create trigger 触发器名字 触发时机 触发事件 on 表 for each row
Begin

End

触发对象：on 表 for each row，触发器绑定实质是表中的所有行，因此当每一行发生指定的改变的时候，就会触发触发器。
触发时机
触发时机：每张表中对应的行都会有不同的状态，当SQL指令发生的时候，都会令行中数据发生改变，每一行总会有两种状态：数据操作前和操作后

Before：在表中数据发生改变前的状态
After：在表中数据已经发生改变后的状态

#### 触发事件

触发事件：mysql中触发器针对的目标是数据发生改变，对应的操作只有写操作（增删改）

Insert：插入操作
Update：更新操作
Delete：删除操作

#### 注意事项

一张表中，每一个触发时机绑定的触发事件对应的触发器类型只能有一个：一张表中只能有一个对应after insert触发器

因此，一张表中最多的触发器只能有6个：before insert，before update，before delete，after insert，after update，after delete

需求：有两张表，一张是商品表，一张是订单表（保留商品ID），每次订单生成，商品表中对应的库存就应该发生变化。

1、	创建两张表：商品表和订单表

2、	创建触发器：如果订单表发生数据插入，对应的商品就应该减少库存
Create trigger 名字  after insert on my_orders for each row

```mysql
delimiter $$
create trigger after_insert_order_t after insert on my_orders for each row
begin
update my_goods set inv = inv -1 where id = 1;
end
$$

delimiter ;
```



### 查看触发器

1、	查看全部触发器
Show triggers;

2、	查看触发器的创建语句
Show create trigger 触发器名字;

```mysql
show triggers \G;
show creater trigger after_insert_order_t \G;
```



#### 触发触发器

想办法让触发器执行：让触发器指定的表中，对应的时机发生对应的操作即可。
1、	表为my_orders
2、	在插入之后
3、	插入操作

#### 删除触发器

基本语法：drop trigger 触发器名字;

```mysql
drop trigger after_insert_order_t;
show triggers;
```



### 触发器应用

#### 	记录关键字：new、old

触发器针对的是数据表中的每条记录（每行），每行在数据操作前后都有一个对应的状态，触发器在执行之前就将对应的状态获取到了，将没有操作之前的状态（数据）都保存到old关键字中，而操作后的状态都放到new中。

在触发器中，可以通过old和new来获取绑定表中对应的记录数据。
基本语法：关键字.字段名

Old和new并不是所有触发器都有：
Insert：插入前全为空，没有old
Delete：清空数据，没有new

#### 	商品自动扣除库存


验证结果


如果库存数量没有商品订单多怎么办？
操作目标：订单表，操作时机：下单前；操作事件：插入

结果验证

[TOC]



