# MySQL

## 视图 :jack_o_lantern:

视图是一个虚拟表（非真实存在），其本质是【根据SQL语句获取动态的数据集，并为其命名】，用户使用时只需使用【名称】即可获取结果集，可以将该结果集当做表来使用。

使用视图我们可以把查询过程中的临时表摘出来，用视图去实现，这样以后再想操作该临时表的数据时就无需重写复杂的sql了，直接去视图中查找即可，但视图有明显地效率问题，并且视图是存放在数据库中的，如果我们程序中使用的sql过分依赖数据库中的视图，即强耦合，那就意味着扩展sql极为不便，因此并不推荐使用

视图的优点：

​	1、简化表之间的联结（把联结写在select中）

​	2、适当的利用视图可以更清晰地表达查询

​	3、过滤不想要的数据（select部分）视图能够对机密数据提供安全保护

​	4、使用视图计算字段值，如汇总这样的值

### 创建视图

```
语法：
	CREATE VIEW 视图名称 AS  SQL语句
如：
	create view 视图名 as select 字段 from 表名 where 条件;
注意：
1. 使用视图以后就无需每次都重写子查询的sql，但是这么效率并不高，还不如我们写子查询的效率高

2. 而且有一个致命的问题：视图是存放到数据库里的，如果我们程序中的sql过分依赖于数据库中存放的视图，那么意味着，一旦sql需要修改且涉及到视图的部分，则必须去数据库中进行修改，而通常在公司中数据库有专门的DBA负责，你要想完成修改，必须付出大量的沟通成本DBA可能才会帮你完成修改，极其地不方便
```

### 使用视图

```
select * from 视图名称
```

### 更新视图数据

```
update 视图名 set 新数据 where 条件;
insert into 视图名 values(数据);
ps：
	新增和修改视图数据，原始表也会跟着被修改
	我们不应该修改视图中的记录，而且在涉及多个表的情况下是根本无法修改视图中的记录的
```

### 修改视图

```
ALTER VIEW 视图名称 AS SQL语句
```

### 删除视图数据

```
DELETE from 视图名 where 条件;
```

### 删除视图

```
drop view 视图名;
```

## 触发器 :jack_o_lantern:

触发器(trigger)：监视某种情况，并触发某种操作

触发器创建语法四要素：1.监视地点(table)

　　　　　　　　　　　2.监视事件(insert/update/delete)

　　　　　　　　　　　3.触发时间(after/before)

　　　　　　　　　　　4.触发事件(insert/update/delete)

使用触发器可以定制用户对表进行【增、删、改】操作时前后的行为，注意：没有查询

### 创建触发器

```
create trigger triggerName  after/before  insert/update/delete
     on 表名 for each row       --这句话是固定的
 
begin
      
     需要执行的sql语句
 
end
 
注意：
	1.after/before: 只能选一个 ,after 表示 后置触发, before 表示前置触发
	2.insert/update/delete:只能选一个
特别：NEW表示即将插入的数据行，OLD表示即将删除的数据行
```

### 使用触发器

触发器无法由用户直接调用，而是由于对表的【增/删/改】操作被动引发的

### 删除触发器

```
drop trigger 触发器名;
```

## 存储过程 :jack_o_lantern:

### 概念

什么是存储过程：类似于函数(方法),简单的说存储过程是为了完成某个数据库中的特定功能而编写的语句集合，该语句集包含了一系列SQL语句（对数据的增删改查）、条件语句和循环语句等，存储过程存放于MySQL中，通过调用它的名字可以执行其内部的一堆sql

使用存储过程的优点：

​	1、存储过程增强了SQL语言灵活性。存储过程可以使用控制语句编写，可以完成复杂的判断和较复杂的运算，有很强的灵活性；
​        2、减少网络流量，降低了网络负载。存储过程在数据库服务器端创建成功后，只需要调用该存储过程即可，而传统的做法是每次都将大量的SQL语句通过网络发送至数据库服务器端然后再执行；
​        3、存储过程只在创造时进行编译，以后每次执行存储过程都不需再重新编译，而一般SQL语句每执行一次就编译一次,所以使用存储过程可提高数据库执行速度。
​        4、系统管理员通过设定某一存储过程的权限实现对相应的数据的访问权限的限制，避免了非授权用户对数据的访问，保证了数据的安全

​	5、用于替代程序写的SQL语句，实现程序与SQL解耦

使用存储过程的缺点：

​	程序员扩展功能不方便

程序与数据库结合使用的三种方式

```
方式一：
    MySQL：存储过程
    程序：调用存储过程

方式二：
    MySQL：
    程序：纯SQL语句

方式三：
    MySQL:
    程序：类和对象，即ORM（本质还是纯SQL语句）
```

### 查看现有存储过程

```
show procedure status;
```

### 删除存储过程

```
drop procedure 存储过程名称;
```
### 创建存储过程

```
对于存储过程，可以接收参数，其参数有三类：

in          仅用于传入参数用
out         仅用于返回值用
inout       既可以传入又可以当作返回值


create procedure 存储过程名称(
    in/out/inout 参数名 参数类型,
    in/out/inout 参数名 参数类型
)
BEGIN
    
    需要执行的SQL语句
    
END

```

### 调用存储过程

```
call 存储过程名称(参数1 参数类型,参数2 参数类型);
```

## 函数 :jack_o_lantern:

### 自定义函数

```
create FUNCTION 函数名(参数1 参数类型,参数2 参数类型)

returns 参数类型 //设置返回类型

BEGIN

    DECLARE sum int default 0;
    set sum = i1+i2;
    return(sum); //返回结果

end 
```

### 调用函数

```
直接调用自定义函数
select 函数名(参数1,参数2);

在sql语句中使用自定义函数
select 函数名(参数1,参数2),表字段 from 表名
```

### 删除函数

```
drop function 函数名;
```

## 事务 :jack_o_lantern:

### 什么是事务

​	事务是应用程序中一系列严密的操作，所有操作必须成功完成，否则在每个操作中所作的所有更改都会被撤消。也就是事务具有原子性，一个事务中的一系列的操作要么全部成功，要么一个都不做。 
​	事务的结束有两种，当事务中的所以步骤全部成功执行时，事务提交。如果其中一个步骤失败，将发生回滚操作，撤消之前到事务开始时的所以操作。

　　总结:事务就是一组操作,要么全部完成,要么全部失败!

### 事物特性ACID

　　事务具有四个特征：原子性（ Atomicity ）、一致性（ Consistency ）、隔离性（ Isolation ）和持续性（ Durability ）。这四个特性简称为 ACID 特性。 

　　1 、原子性  (事物内的操作,要么全部成功,要么全部失败)
​	事务是数据库的逻辑工作单位，事务中包含的各操作要么都做，要么都不做

　　2 、一致性 (事物之前之后,前后数据的一致性)
​	事务执行的结果必须是使数据库从一个一致性状态变到另一个一致性状态。因此当数据库只包含成功事务提交的结果时，就说数据库处于一致性状态　如果数据库系统 运行中发生故障，有些事务尚未完成就被迫中断，这些未完成事务对数据库所做的修改有一部分已写入物理数据库，这时数据库就处于一种不正确的状态，或者说是 不一致的状态。 

　　3 、隔离性(多个事物时,相互不能干扰) 
​	一个事务的执行不能被其它事务干扰。即一个事务内部的操作及使用的数据对其它并发事务是隔离的，并发执行的各个事务之间不能互相干扰。

　   4 、持续性(一旦事物提交(commit)之后,是不可回滚的) 
​	持续性也称永久性，指一个事务一旦提交，它对数据库中的数据的改变就应该是永久性的。接下来的其它操作或故障不应该对其执行结果有任何影响。 

### 实例操作

​	1.开启事物  start transaction

​	2.提交事物   commit

​	3.回滚事物   rollback

```
create table user(
id int primary key auto_increment,
name char(32),
balance int
);

insert into user(name,balance)
values
('w',1000),
('l',1000),
('y',1000);

#原子操作
start transaction;
update user set balance=900 where name='w'; # w支付100元
update user set balance=1010 where name='l'; # l拿走10元
update user set balance=1090 where name='y'; # y家拿到90元
commit;

#出现异常，回滚到初始状态
start transaction;
update user set balance=900 where name='w'; # w支付100元
update user set balance=1010 where name='l'; # l拿走10元
uppdate user set balance=1090 where name='y'; # y拿到90元,出现异常没有拿到
rollback;
commit;

mysql> select * from user;
+----+------+---------+
| id | name | balance |
+----+------+---------+
|  1 |  w   |    1000 |
|  2 |  l   |    1000 |
|  3 |  y   |    1000 |
+----+------+---------+
3 rows in set (0.00 sec)
```



## 流程控制:jack_o_lantern:

### 条件语句

```
复制代码
delimiter //
CREATE PROCEDURE proc_if ()
BEGIN

    declare i int default 0;
    if i = 1 THEN
        SELECT 1;
    ELSEIF i = 2 THEN
        SELECT 2;
    ELSE
        SELECT 7;
    END IF;

END //
delimiter ;
```

### 循环语句

```
delimiter //
CREATE PROCEDURE proc_while ()
BEGIN

    DECLARE num INT ;
    SET num = 0 ;
    WHILE num < 10 DO
        SELECT
            num ;
        SET num = num + 1 ;
    END WHILE ;

END //
delimiter ;
```

repeat循环

```
delimiter //
CREATE PROCEDURE proc_repeat ()
BEGIN

    DECLARE i INT ;
    SET i = 0 ;
    repeat
        select i;
        set i = i + 1;
        until i >= 5
    end repeat;

END //
delimiter ;
```

loop

```
BEGIN
    
    declare i int default 0;
    loop_label: loop
        
        set i=i+1;
        if i<8 then
            iterate loop_label;
        end if;
        if i>=10 then
            leave loop_label;
        end if;
        select i;
    end loop loop_label;

END
```



