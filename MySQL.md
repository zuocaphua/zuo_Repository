# mysql

## 1.数据库?

存储数据的仓库

## 2.我们测试为什么要学习数据库?

1.我在界面上做了操作,但是这个操作对不对不清楚,就要去数据库验证是否有内容及内容的正确性

2.我们为了'跑'业务,但界面上数据不足以去完成.我们可以手动修改数据库中的数据,然后刷新就可以'跑'

## 3.数据库的地位

是IT人的基础知识.开发,测试,运维,运营支撑都会数据库

他和Linux一样是基础中的基础

对面试而言,数据库主要在笔试中考,面试中可能会现场出题让你做

从培训角度和工作角度出发,我讲授必须掌握的部分

4.数据库的分类

关系型:mysql.oracle,mssql

非关系型:

​	键值对(内存):redis

​	文档:MongoDB

## 4.安装

略

## 5.navicat

连接名:随意取,一般建议取服务器ip的最后一段(知道是哪台机)

ip:服务器的ip,本机是localhost,其他:输入ip地址

端口:3306(默认但可改)

用户名:root

密码:

## 6.库

1.右键----新建数据库

2.数据库名:随意(全英)

   字符集:utf-8

   排序规则:utf8_general_ci



## 7.表

作为测试的你,不需要去建表

实际工作是:开发建,因为功能是他开发,因此他要根据功能决定数据库表如何处理

为了数据库知识的完备性,还是要讲表和表的各种知识



案例:请完成表的创建

### 1.约束

#### 1.非空 not null

#### 2.唯一 unique

#### 3.主键 primary key

主键=非空+唯一

一般是一个表的第一个字段设定成主键且名一般都叫id或xxid

一个表一般都要有主键(中间表除外)

**mysql中主键设定后一般都勾选上"自动递增",原因是:id会从1,2,3....n,自动的每次加1,这样我就不用管id,因为系统触发+1规则保证id的唯一性**

oracle采用的是:序列+触发器完成mysql的自动递增

#### 4.外键 foreign key

1.一个是2表才有外键的概念

**2.一个表的外键一定是另外一个表的主键**

3.外键的引擎要采用InnoDb,否则无法创建外键



### 2.默认值

如果没值,就给默认值;如果有值,替换默认值



### 3.注释

对给定的字段做注释,方便其他人理解字段含义

工作后,建议开发都把每个字段的注释都写上



### 4.无符号

写入的数据不能带符号(-.!@)

主要是针对整数,小数而言,这个字段只能填正整时勾选"无符号"



### 5.填充零

当位数不够时,在前面补充0





## 8.查询(非常重要)

### 1.简单查询

**完整语法:**

select [distinct] 字段,函数

from 表

[where 条件]

[group by 字段]

   [having 条件]

[order by 字段]



#### 1. select

```mysql
#1.查询一个字段
select ename from emp;

#2.查询多个字段
select ename,job,sal,empno from emp;

#3.查询所有字段
select * from emp;

#4.运算
select ename+5 from emp;  #没有意义.mysql不报错,其他数据库会报错
#如下可行,要求运算列为数值
select sal*12 from emp;

#如运算列存在空值,运算结果为空
select sal,comm,sal+comm from emp;
#为了解决空的问题,mysql采用ifnull函数,第一个参数:如果有值 第二个参数:如果没值后取的默认值
select sal,comm,sal+ifnull(comm,0) from emp;

#5.别名  as===alias
#我们的客户想一下子就知道字段的意思,而经过各种运算后的字段特别长,不利于一下子就知道含义,因此用别名
select sal,comm,sal+ifnull(comm,0) as 月薪,(sal+ifnull(comm,0))*12 as 年薪 from emp;

#如上,语法是不错的,但不符合工作.别名要求:as不写(推荐);不写中文;见名知意;
#即:推荐全英命名
#哪个字段上有空值,就在原来的纯字段变成ifnull(字段,0)
select sal,comm,sal+ifnull(comm,0) month_sal,(sal+ifnull(comm,0))*12 year_sal from emp;

#6.distinct---去重
select distinct job from emp;
#注意:如下写法,是说把distinct后面的部分看成一个整体,对整体去重,看成:distinct (job,ename)
select distinct job,ename from emp;
select distinct job,deptno from emp;

```





### 2.子查询





















