---
title: mariadb
date: 2017-10-25 14:03:59
tags: [database,mysql]
---
>ubuntu install MySql  

```
apt-get install mysql-server mysql-client
```
test success
```
mysql -u root -p
```
[Upstream URL](https://zhuanlan.zhihu.com/p/28102425)  
<!--more-->
---
>archlinux install MariaDb  

```
sudo pacman -S mariadb mariadb-clients
```
init mariadb data file
```
sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
```
start mariadb
```
sudo systemctl start mysqld
```
setup new password for root
```
mysqladmin -u root password '12345678'
```
sigin mariadb
```
mysql -u root -p
```
make mariadb boot up
```
sudo systemctl enable mysqld
```
**pay attention to:** After Mysql was acquired by Oracle archlinux only carry mariadb,mariadb is a branch of mysql and mariadb compatible with mysql   
[Upstream URL](http://blog.csdn.net/u011054333/article/details/53203787)  

---
Login databases
```
mysql -h (hostname) -u (username) -p  
```
```
mysql -u (username) -p ----if login local database
```
Create databases for examp samp_db
```
create databases samp_db character set gbk;
```
When you log into mysql, you need specify the database to operate  
```
use students
```
Make an examp of students table ,there are **id**,**name**,**sex** ,**age**,**tel** **:**  
```
create table students
（
      id int unsigned not null auto_increment primary key,
      name char(8) not null,
      sex char(4) not null,
      age tinyint unsigned not null,
      tel char(13) null default “-“
);  
```
添加用户  
[add user](https://dev.mysql.com/doc/refman/5.7/en/adding-users.html)
---
>对于一些较长的语句在命令提示符下可能容易输错, 因此我们可以通过任何文本编辑器将语句输入好后保存为 createtable.sql 的文件中, 通过命令提示符下的文件重定向执行执行该脚本。

打开命令提示符, 输入: mysql -D samp_db -u root -p < createtable.sql

(提示: 1.如果连接远程主机请加上 -h 指令; 2. createtable.sql 文件若不在当前工作目录下需指定文件的完整路径。)
查询表
show tables
insert

insert [into] 表名 [(列名1, 列名2, 列名3, …)] values (值1, 值2, 值3, …);
insert into students values(NULL, “王刚”, “男”, 20, “13811371377”);
insert into students (name, sex, age) values(“孙丽华”, “女”, 21);
select

select 列名称 from 表名称 [查询条件];
select name, age from students;
select * from students;
where

select 列名称 from 表名称 where 条件;
select from students where sex=”女”;
查询年龄在21岁以上的所有人信息: select from students where age > 21;
查询名字中带有 “王” 字的所有人信息: select from students where name like “%王%”;
查询id小于5且年龄大于20的所有人信息: select from students where id<5 and="" age="">20;
update

将id为5的手机号改为默认的”-“: update students set tel=default where id=5;
将所有人的年龄增加1: update students set age=age+1;
将手机号为 13288097888 的姓名改为 “张伟鹏”, 年龄改为 19: update students set name=”张伟鹏”, age=19 where tel=”13288097888”;
delete

delete from 表名称 where 删除条件;
删除id为2的行: delete from students where id=2;
删除所有年龄小于21岁的数据: delete from students where age<20;
删除表中的所有数据: delete from students;
alter table
alter table 表名 add 列名 列数据类型 [after 插入位置];

在表的最后追加列 address: alter table students add address char(60);
在名为 age 的列后插入列 birthday: alter table students add birthday date after age;
alter table 表名 change 列名称 列新名称 新数据类型;

将表 tel 列改名为 telphone: alter table students change tel telphone char(13) default “-“;
将 name 列的数据类型改为 char(16): alter table students change name name char(16) not null;
alter table 表名 drop 列名称;

删除 birthday 列: alter table students drop birthday;
alter table 表名 rename 新表名;

重命名 students 表为 workmates: alter table students rename workmates;
drop table 表名;

删除 workmates 表: drop table workmates;
drop database 数据库名;

删除 samp_db 数据库: drop database samp_db;
修改 root 用户密码

打开命令提示符界面, 执行命令: mysqladmin -u root -p password 新密码
执行后提示输入旧密码完成密码修改, 当旧密码为空时直接按回车键确认即可。  
**Upstream**  
[21分钟MySQL入门教程](http://www.cnblogs.com/mr-wid/archive/2013/05/09/3068229.html)  
可视化管理工具[MySQL Workbench](https://www.mysql.com/products/workbench/)
