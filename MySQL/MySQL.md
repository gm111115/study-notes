# MySQL一

## 用户及权限操作:jack_o_lantern:

### 用户操作

```
更新root 用户的密码
set password for ‘root’@’localhost’ = password(‘新密码’)
ps：用SET PASSWORD命令，此种方式适用于当前root用户没有密码的情况
UPDATE user SET Password = PASSWORD('newpass') WHERE user = 'root';
ps：用UPDATE直接编辑user表，此种方式不管有没有密码都可以进行修改
创建一个新用户,mysql授权用户以指定IP登录
create user ‘用户名’@’192.168.1.1’ identified by ‘密码’
ps:指定固定IP访问
create user ‘用户名’@’192.168.1.%’ identified by ‘密码’
ps:前面三位IP符合条件即可以访问
 
create user ‘用户名’@’%’ identified by ‘密码’
ps:没有IP限制,%表示通配所有IP
 
删除用户
drop user '用户名'@'IP'
修改用户
rename user '老用户名'@'IP' to '老用户名'@'IP'

丢失root密码
mysqld_safe --skip-grant-tables&  
ps: 在启动mysql时不启动grant-tables，授权表
mysql -u root mysql
mysql> UPDATE user SET password=PASSWORD("new password") WHERE user='root';
mysql> FLUSH PRIVILEGES;
```

### 用户授权

```
为用户授 指定权限  
grant select,insert,update on 数据库.表名 to '用户名'@'%'; 

为用户授 所有权限,除了root权限
grant all privileges on db1.t1 on 数据库.表名 to '用户名'@'%'; 

刷新授权
FLUSH PRIVILEGES 

去除权限；
12 revoke select on db_name.* from　'用户名'@'IP';　　　
```

## 库操作:jack_o_lantern:

### 系统数据库

information_schema： 虚拟库，不占用磁盘空间，存储的是数据库启动后的一些参数，如用户表信息、列信息、权限信息、字符信息等
performance_schema： MySQL 5.5开始新增一个数据库：主要用于收集数据库服务器性能参数，记录处理查询请求时发生的各种事件、锁等现象 
mysql：授权库，主要存储系统用户的权限信息
test：MySQL数据库系统自动创建的测试数据库

### 创建数据库

#### 数据库命名规则

```
可以由字母、数字、下划线、＠、＃、＄
区分大小写
唯一性
不能使用关键字如 create select
不能单独使用数字
最长128位
```

#### 数据库操作

```
1.查看数据库
show databases;
show create database db1;
select database();
ps: 默认数据库：
　　mysql - 用户权限相关数据
　　test - 用于用户测试数据
　　information_schema - MySQL本身架构相关数据

2.选择数据库
USE 数据库名

3.创建数据库并设置编码集
create database 数据库名 character set ='utf8'

4.删除数据库
DORP DATABASE 数据库名;

5.修改数据库
alter database db1 charset utf8;
```

## 表操作:jack_o_lantern:

### 表介绍

表相当于文件，表中的一条记录就相当于文件的一行内容，不同的是，表中的一条记录有对应的标题，称为表的字段

### 创建表

```
create table 表名(
字段名 类型[约束条件如：not null auto_increment primary key default 0],        -- 非空、递增——唯一性，主键，默认列值
)ENGINE=InnoDB　　　　-- 设置表的存储引擎，一般常用InnoDB和MyISAM；InnoDB可靠，支持事务；MyISAM高效不支持全文检索
DEFAULT charset=utf8;　　-- 设置默认的编码，防止数据库中文乱码
-- 如果有条件的创建数据表还可以使用   
CREATE TABLE IF NOT EXISTS 表名(........
注意：
1. 在同一张表中，字段名是不能相同
2. 宽度和约束条件可选
3. 字段名和类型是必须的
```

### 修改表

```
1. 修改表名
ALTER TABLE 旧表名 RENAME 新表名;
RENAME TABLE 旧表名 TO 新表名;

2. 增加字段
ALTER TABLE 表名 ADD 字段名  数据类型 [完整性约束条件…],
ALTER TABLE 表名 ADD 字段名  数据类型 [完整性约束条件…] FIRST;
ALTER TABLE 表名 ADD 字段名  数据类型 [完整性约束条件…] AFTER 字段名;                        
3. 删除字段
ALTER TABLE 表名 DROP 字段名;

4. 修改字段
ALTER TABLE 表名 MODIFY  字段名 数据类型 [完整性约束条件…];
ALTER TABLE 表名 CHANGE 旧字段名 新字段名 旧数据类型 [完整性约束条件…];
ALTER TABLE 表名 CHANGE 旧字段名 新字段名 新数据类型 [完整性约束条件…];
```

### 复制表

```
复制表结构＋记录 （key不会复制: 主键、外键和索引）
create table new_tablename select * from tablename;

或者部分复制：
CREATE TABLE new1_tablename SELECT 字段名 FROM tablename;

只复制表结构
select * from tablename where 1=2;     //条件为假，查不到任何记录
create table new1_tablename select * from tablename where 1=2;  
```

### 查看表

```
SHOW TABALES;
```

### 删除表

```
DROP TABLE 表名;
```

### 清空表

```
truncate table 表名;
```
### 重命名表

```
RENAME TABLE 旧表名 TO 新表名;
 
还可以使用：

ALTER TABLE 旧表名 RENAME 新表名;
```

## 数据操作:jack_o_lantern:

### 新增

```
1. 插入完整数据（顺序插入）
    语法一：
    INSERT INTO 表名(字段1,字段2,字段3…字段n) VALUES(值1,值2,值3…值n);

    语法二：
    INSERT INTO 表名 VALUES (值1,值2,值3…值n);

2. 指定字段插入数据
    语法：
    INSERT INTO 表名(字段1,字段2,字段3…) VALUES (值1,值2,值3…);

3. 插入多条记录
    语法：
    INSERT INTO 表名 VALUES
        (值1,值2,值3…值n),
        (值1,值2,值3…值n),
        (值1,值2,值3…值n);
        
4. 插入查询结果
    语法：
    INSERT INTO 表名(字段1,字段2,字段3…字段n) 
                    SELECT (字段1,字段2,字段3…字段n) FROM 表2
                    WHERE …;
```

### 修改

```
update table_name SET 字段名=更新值  WHERE 条件字段=条件值;
```

### 删除

```
DELETE FROM 表名称 WHERE 条件字段=条件值;
```

### 查询

#### 单表查询

##### 语法

```
SELECT 字段1,字段2... FROM 表名
                  WHERE 条件
                  GROUP BY field
                  HAVING 筛选
                  ORDER BY field
                  LIMIT 限制条数
```

##### 关键字的执行优先级

```
重点中的重点：关键字的执行优先级
from                
where
group by
having
select
distinct
order by
limit
```

**1.找到表:from**

**2.拿着where指定的约束条件，去文件/表中取出一条条记录**

**3.将取出的一条条记录进行分组group by，如果没有group by，则整体作为一组**

**4.将分组的结果进行having过滤**

**5.执行select**

**6.去重**

**7.将结果按条件排序：order by**

**8.限制结果的显示条数**

##### WHERE约束

where字句中可以使用：

1. 比较运算符：> < >= <= <> !=

2. between 10 and 20 值在10到20之间

3. in(10,20,30) 值是10或20或30

4. like 'timo%'

   pattern可以是%或_，

   %表示任意多字符

   _表示一个字符 

5. 逻辑运算符：在多个条件直接可以使用逻辑运算符 and or not

#### 多表查询

##### 外连接语法

```
SELECT 字段列表
    FROM 表1 INNER|LEFT|RIGHT JOIN 表2
    ON 表1.字段 = 表2.字段;
```

##### 交叉连接：不适用任何匹配条件，生成笛卡尔乘积

```
select * from 表1,表2;
```

##### 内连接：只连接匹配的行

```
#找两张表共有的部分，相当于利用条件从笛卡尔积结果中筛选出了正确的结果
```

pass

##### 外链接之左连接：优先显示左表全部记录

```
#以左表为准，匹配所有结果
#本质就是：在内连接的基础上增加左边有右边没有的结果
```

pass

##### 外链接之右连接：优先显示右表全部记录

```
#以右表为准，即找出所有部门信息，包括没有员工的部门
#本质就是：在内连接的基础上增加右边有左边没有的结果
```

pass

##### 全外链接：显示左右两个表全部记录

```
全外连接：在内连接的基础上增加左边有右边没有的和右边有左边没有的结果
注意：
	mysql不支持全外连接 full JOIN
	union与union all的区别：union会去掉相同的纪录
```

pass

#### 子查询

```
1：子查询是将一个查询语句嵌套在另一个查询语句中。
2：内层查询语句的查询结果，可以为外层查询语句提供查询条件。
3：子查询中可以包含：IN、NOT IN、ANY、ALL、EXISTS 和 NOT EXISTS等关键字
4：还可以包含比较运算符：= 、 !=、> 、<等
```

##### 带IN关键字的子查询

```
select 字段名 from 表名
    where 字段 in (select 查询语句);
```

##### 带比较运算符的子查询

```
比较运算符：=、!=、>、>=、<、<=、<>
select 字段名 from 表名 
	where 字段 > (select 查询语句);
```

##### 带EXISTS关键字的子查询

EXISTS关字键字表示存在。在使用EXISTS关键字时，内层查询语句不返回查询的记录。
而是返回一个真假值。True或False
当返回True时，外层查询语句将进行查询；当返回值为False时，外层查询语句不进行查询

```
select * from 表名
         where exists
             (select 查询语句);
```