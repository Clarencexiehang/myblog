---
title: MySQL
date: 2022-06-13 13:43:25
tags:
cover: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fwww.xuekebaba.com%2Fuploads%2F202002%2F24%2F200224124159340.jpg&refer=http%3A%2F%2Fwww.xuekebaba.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1657691780&t=58e101bc5022bf76b2852a6f1da04f9e
---

# MySQL

[TOC]



## 命令

启动

net start mysql80

net stop mysql80



客户端连接

mysql [-h 连接地址] [-p 连接端口] -u root -p

查看表基本结构	DESCRIBLE 表名	（可以缩写为DESC）

查看详细表结构	SHOW CREATE TABLE 表名	\G

ALTER TABLE   旧表名	RENAME	 [TO]	 新表名；



## SQL

#### 1.DDL(Data Definition Language)

SHOW DATABASES

SELECT DATABASE()

CREATE DATABASE [IF NOT EXISTS] NAME [DEFAULT CHARSET] （utf-8mb4）[COLLATE 排序规则]

​	

DROP DATABASE[IF EXISTS] NAME

USE (NAME)



表

CREATE TABLE 表名{

}

SHOW TABELS;

DESC







#### 2.DML(Manipulation)

INSERT INTO    VALUES

UPDATE 表名 SET 字段名1=value,… [WHERE 条件]

DELETE 表名 FROM [WHERE 条件]



#### 3.DQL(Query)

##### 基本查询

SELECT 字段  FROM 表名 

设置别名 SELECT  AS FROM

去除重复记录 SELECT DISTINCT 字段 FROM 表名



##### 条件查询

SELECT   FROM   WHERE 



##### 聚合函数

count 统计数量	max	min	avg	sum

SELECT  聚合函数 FROM 



##### 分组查询

SELECT 字段列表 FROM 表名 [WHERE]  GROUP BY 分组字段名 [HAVING 分组后过滤条件]



##### 排序查询

SELECT 字段列表 FROM 表名 ORDER BY 字段 排序方式

ASC	升序

DESC	降序 



 限制结果集并排序

| 类别     | 详细解示                                                     |
| :------- | :----------------------------------------------------------- |
| 基本语法 | select 字段 from 表 order by 字段 关键词 limit 数量          |
| 示例     | select id,username, balance from money order by balance desc limit 5; |
| 示例说明 | 按照钱来排序，显示前五个最有钱的用户                         |



##### 分页查询

SElECT 字段列表 FROM 表名 LIMIT 起始索引，查询记录数	（0开始） 



DQL编写顺序

<img src="https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202205151616871.png" alt="image-20220515161614816" style="zoom: 50%;" />

DQL的执行顺序

from->where->select->order by->limit 



#### 4.DCL(Control)	数据控制语言

管理用户和控制数据库的访问权限 

查询权限	SHOW GRANTS FOR ‘用户名@主机名“

授予权限	GRANT 权限列表 ON 数据库名.表名 TO ’用户名‘@’主机名‘

撤销权限  REVOKE 权限列表 ON 数据库名.表名 FROM ’用户名‘@’主机名‘





## 函数

1.字符串函数

![image-20220515172802869](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202205151728934.png)

 

2.数值函数

![image-20220516153448830](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202205161534887.png)

随机生成六味验证码

```mysql
select lpad(round(rand()*1000000,0),6,'0');
```



3.日期函数

![image-20220516154315992](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202205161543055.png)

往后推70年

select date_add(now(),INTERVAL 70 YEAR);

查询所有员工的入职天数

```mysql
select name,datediff(curdate(),entrydate) as 'entrydays' from emp order by entrydays desc;
```



4.流程函数

![image-20220516155130511](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202205161551567.png)



## 约束

![image-20220516160544137](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202205161605215.png)

外键 add constraint

drop foreign key 

<img src="https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202205161646127.png" alt="image-20220516164606059" style="zoom:150%;" />



## 多表查询

内连接：

隐式：select 字段列表 from 表1，表2 where 条件；

显示：select 字段列表 from 表1【inner】 join 表2 on 连接条件 ；



外连接：

左外：select 字段列表 from 表1 left 【outer】join 表2 on 条件；

右外：select 字段列表  from 表1 right 【outer】join 表2 on 条件；



自连接：select 字段列表  from 表1 别名A join 表A 别名B on 条件；



联合查询：将多次查询的结果合并起来，all 不用可去重

select 字段列表 from 表1 left 【outer】join 表2 on 条件；

union （all）	

select 字段列表  from 表1 right 【outer】join 表2 on 条件；



子查询：select 字段列表 from 表1 where column=（select column from 表2）；

行子查询 =	<>	IN		NOT IN

表子查询	IN



## 事务

方式一

查看事务提交方式

```sql
SELECT @@autocommit;	//0 手动提交   1 自动提交
SET @@autocommit=0
```

提交事务

```sql
COMMIT;
```

回滚事务（出现异常后）

```sql
ROLLBACK;
```



方式二

开启事务

```sql
START TRANSACTION 或 BEGIN;
```

提交事务

```sql
COMMIT;
```

回滚事务（出现异常后）

```sql
ROLLBACK;
```



四大特性：

* 原子性
* 一致性
* 隔离性:  不受外部并发操作影响的独立环境下运行
* 持久性：事务一旦提交或回滚，对数据库的改变永久



并发事务问题：

* 脏读: 一个事务读取另一事务还没提交的数据
* 不可重复度： 一个事务先后读取同一条记录，但两次读取的数据不同
* 幻读： 一个失误按照条件查询数据时，没有对应的数据行，但是插入数据时又已存在



事务的隔离级别

![image-20220518221738957](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202205182217030.png)

查看事务隔离级别

```SQL
SELECT @@TRANSACTION_ISOLATION
```

设置事务隔离级别

```MYSQL
SET [SESSION|GLOBAL] TRANSACTION ISOLATION LEVEL 
	{READ UNCOMMITTED|READ COMMITTED| REPEATABLE READ| SERIALIZABLE}
```





## 存储引擎

基于表（表类型） 默认InnoBD

```sql
SHOW ENGINES;	//展现当前的引擎
```



InnoBD 

文件：每一个表对应一个xxx.ibd 文件

逻辑存储结构：

* TableSpace
* Segment
* Extent(区   1M)
* Page（16K）
* Row



MyISAM

特点： 

* 不支持事务，不支持外键
* 支持表锁，不支持行锁
* 访问速度快

文件：

* xxx.sdi：存储表结构信息

* xxx.MYD ：存储数据

* xxx.MYI ：存储索引



Memory

作为临时表或者缓存，存放于内存中，断电数据遗失，但是速度快



存储引擎特点对比：

![image-20220521143058764](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202205211430833.png)





## 索引

![image-20220601172820552](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202206011728678.png)



聚集索引：索引叶子结点是数据（存在主键）

二级索引：数据与索引分开

![image-20220602111334372](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202206021113477.png)



SQL执行频率

show global status like ‘Com_______’

show profiles		查看每条SQL的耗时基本情况

show profile for query_id

show profile cpu for query query_id

看执行计划	select前面加explain

type：连接类型，性能由好到差：NULL，system,const,eq_ref,ref,range,index,all



### 普通索引

| 类型     | 详细说明                                   |
| :------- | :----------------------------------------- |
| 基本语法 | alter table 表 add index(字段)             |
| 示例     | ALTER TABLE `money` ADD INDEX(`username`); |
| 示例解释 | 为money表的username字段增加索引            |

### 唯一索引

| 类型     | 详细说明                                 |
| :------- | :--------------------------------------- |
| 基本语法 | alter table 表 add UNIQUE(字段)          |
| 示例     | ALTER TABLE `money` ADD UNIQUE(`email`); |
| 示例解释 | 为money表的email字段增加唯一索引         |

### 全文索引

| 类型     | 详细说明                                     |
| :------- | :------------------------------------------- |
| 基本语法 | alter table 表 add FULLTEXT(字段)            |
| 示例     | ALTER TABLE `money` ADD FULLTEXT(`content`); |
| 示例解释 | 为money表的content字段增加唯一索引           |

### 主键索引

| 类型     | 详细说明                                   |
| :------- | ------------------------------------------ |
| 基本语法 | alter table 表 add PRIMARY KEY(字段)       |
| 示例     | ALTER TABLE `money` ADD PRIMARY KEY(`id`); |
| 示例解释 | 为money表的id字段增加主键索引              |





## JDBC

![image-20220605155055079](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202206051550145.png)



![image-20220606194617253](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202206061946305.png)



```sql
package com.MySQL.jbdc;

import java.sql.*;

public class JDBCDemo {
    public static void main(String[] args) throws Exception {
        //获取连接
        String url="jdbc:mysql://root@localhost:3306/student";
        String username="root@localhost";
        String password="123456";
        Connection conn = DriverManager.getConnection(url, username, password);

        String sql="update dormitory set num=123 where name='LiDongjin'";

        try {
            Statement stmt = conn.createStatement();

            int i = stmt.executeUpdate(sql);
            System.out.println(i);
            stmt.close();
        } catch (SQLException e){
            e.printStackTrace();
        } catch (Exception e){
            e.printStackTrace();
        }
        conn.close();
    }
}

```





### connection

开启事务	setAutoCommit(boolean autoCommit)	true为自动提交，false开启事务，手动提交

提交：commit（)

回滚：rollback();

```sql
        //获取sql对象
        Statement stmt = conn.createStatement();

        String sql1="update dormitory set num=111 where name='LiDongjin'";
        String sql2="update dormitory set num=222 where id=1";

        try {
            //开启事务
            conn.setAutoCommit(false);

            //执行sql
            int count1 = stmt.executeUpdate(sql1);
            int count2 = stmt.executeUpdate(sql2);
            System.out.println(count1+" "+count2);

            //提交事务
            conn.commit();

            //释放资源
            stmt.close();
            conn.close();
        }  catch (Exception e){
            e.printStackTrace();
        }
```



### 查询

ResultSet 封装了DQL的结果   stmt.executeQuery(sql); 返回ResultSet对象

getXXX（参数） ：获取数据

```
//执行sql
ResultSet resultSet = stmt.executeQuery(sql1);

//处理结果
while(resultSet.next()){
//get data
int id = resultSet.getInt(1);
String name = resultSet.getString(2);
int num = resultSet.getInt(3);

System.out.println(id+" "+name+" "+num);

```



### PreparedStatement

需要设置？的值

```
void Pre() throws Exception {
        //获取连接
        String url="jdbc:mysql://root@localhost:3306/student";
        String username="root@localhost";
        String password="123456";
        Connection conn = DriverManager.getConnection(url, username, password);

        String sql1="select * from dormitory where name = ?";

        PreparedStatement preparedStatement = conn.prepareStatement(sql1);

        //set the value of ?
        preparedStatement.setString(1,"LiDongjin");

        //执行sql,不传参
        ResultSet resultSet = preparedStatement.executeQuery();

        //处理结果
        if(resultSet.next()) {
            int id = resultSet.getInt(1);
            String name = resultSet.getString(2);
            int num = resultSet.getInt(3);
            System.out.println(id+" "+name+" "+num);
        }
        //释放资源
        resultSet.close();
        preparedStatement.close();
        conn.close();

    }
```





### 数据库连接池

Druid
