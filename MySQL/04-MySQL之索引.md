# MySQL

## 索引 :jack_o_lantern:

### 介绍

索引的目的在于提高查询效率，与我们查阅图书所用的目录是一个道理，先定位到章，然后定位到该章下的一个小节，然后找到页数，可以帮助用户快速的找到需要的内容.

本质：通过不断地缩小想要获取数据的范围来筛选出最终想要的结果，同时把随机的事件变成顺序的事件，也就是说，有了这种索引机制，我们可以总是用同一种查找方式来锁定数据。特别是当数据量非常大，查询涉及多个表时，使用索引往往能使查询速度加快成千上万倍，能够大大提高查询效率

　　索引优点:可以提高查询效率,而且是数据量越大效果越明显.

　　索引缺点:添加数据和删除数据效率低

### 类型

我们可以在创建索引的时候，为其指定索引类型，分两类
​	hash类型的索引：查询单条快，范围查询慢
​	btree类型的索引：b+树，层数越多，数据量指数级增长（我们就用它，因为innodb默认支持它）

　　1、HASH :hash就是一种（key=>value）形式的键值对,允许多个key对应相同的value，但不允许一个key对应多个value,为某一列或几列建立hash索引，就会利用这一列或几列的值通过一定的算法计算出一个hash值，对应一行或几行数据.   hash索引可以一次定位，不需要像树形索引那样逐层查找,因此具有极高的效率

​	假设创建如下一个表：

```
CREATE TABLE testhash (

  　　　　 fname VARCHAR(50) NOT NULL,

   　　　　lname VARCHAR(50) NOT NULL,

   　　　　KEY USING HASH(fname)

　　　　) ENGINE=MEMORY;
　
```

​	包含的数据如下：

　　　　![img](http://images.cnblogs.com/cnblogs_com/hustcat/mysql/mysql02-02.JPG) 

​	假设索引使用hash函数f( )，如下：

```
f('Arjen') = 2323
f('Baron') = 7437
f('Peter') = 8784
f('Vadim') = 2458
```

　　此时，索引的结构大概如下：

　　　![img](http://images.cnblogs.com/cnblogs_com/hustcat/mysql/mysql02-03.JPG)  

Slots是有序的，但是记录不是有序的。当你执行
　　mysql> SELECT lname FROM testhash WHERE fname='Peter';
MySQL会计算’Peter’的hash值，然后通过它来查询索引的行指针。因为f('Peter') = 8784，MySQL会在索引中查找8784，得到指向记录3的指针。
因为索引自己仅仅存储很短的值，所以，索引非常紧凑。Hash值不取决于列的数据类型，一个TINYINT列的索引与一个长字符串列的索引一样大。

​	2、BTREE: 就是一种将索引值按一定的算法，存入一个树形的数据结构中. 如二叉树一样

　　![img](http://images2017.cnblogs.com/blog/1284211/201711/1284211-20171123143758086-565090818.png)

**不同的存储引擎支持的索引类型也不一样**

InnoDB 支持事务，支持行级别锁定，支持 B-tree、Full-text 等索引，不支持 Hash 索引
MyISAM 不支持事务，支持表级别锁定，支持 B-tree、Full-text 等索引，不支持 Hash 索引
Memory 不支持事务，支持表级别锁定，支持 B-tree、Hash 等索引，不支持 Full-text 索引
NDB 支持事务，支持行级别锁定，支持 Hash 索引，不支持 B-tree、Full-text 等索引
Archive 不支持事务，支持表级别锁定，不支持 B-tree、Hash、Full-text 等索引

### 分类

​	1.普通索引

​		INDEX：加速查找

​	2.唯一索引

​		UNIQUE:加速查找+约束（不能重复）

​	3.主键索引

​		PRIMARY KEY：加速查找+约束（不为空、不能重复）

​	4.组合/联合索引

​		PRIMARY KEY(id,name):联合主键索引    

​		UNIQUE(id,name):联合唯一索引    

​		INDEX(id,name):联合普通索引

​	5.FULLTEXT:全文索引

　　　　InnoDB引擎对FULLTEXT索引的支持是MySQL5.6新引入的特性，之前只有MyISAM引擎支持FULLTEXT索引，而且只有 CHAR、VARCHAR ，TEXT 列上可以创建全文索引.

　　　　FULLTEXT索引是按照分词原理建立索引的。西方文字中，大部分为字母文字，分词可以很方便的按照空格进行分割。但很明显，中文不能按照这种方式进行分词。这里介绍一个Mysql的中文分词插件Mysqlcft，有了它，就可以对中文进行分词，想了解的可以查看Mysqlcft，当然还有其他的分词插件可以使用。

## MySQL索引管理 :jack_o_lantern:

### 创建索引

```
方法一：创建表时
    　　CREATE TABLE 表名 (
                字段名1  数据类型 [完整性约束条件…],
                字段名2  数据类型 [完整性约束条件…],
                [UNIQUE | FULLTEXT | SPATIAL ]   INDEX | KEY
                [索引名]  (字段名[(长度)]  [ASC |DESC]) 
                );


方法二：CREATE在已存在的表上创建索引
	   CREATE  [UNIQUE | FULLTEXT | SPATIAL ]  INDEX  索引名 
                     ON 表名 (字段名[(长度)]  [ASC |DESC]) ;


方法三：ALTER TABLE在已存在的表上创建索引
	   ALTER TABLE 表名 ADD  [UNIQUE | FULLTEXT | SPATIAL ] INDEX
                             索引名 (字段名[(长度)]  [ASC |DESC]) ;
```

#### 普通索引

```
CREATE index 索引名 on 表名(添加索引的字段,多个字段以","间隔)
```

#### 唯一索引

```
CREATE UNIQUE index 索引名 on 表名(字段)
```

#### 主键索引

```
alter table 表名 add primary key(字段);
注意:主键索引只能有一个
```

#### 组合/联合索引

联合索引时指对表上的多个列合起来做一个索引。联合索引的创建方法与单个索引的创建方法一样，不同之处在仅在于有多个索引列，如下

```
create index 索引名 on 表名(字段,字段)
```

### 删除索引

```
DROP INDEX 索引名 ON 表名字;
```

