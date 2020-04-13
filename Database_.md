# 数据库

| SQL术语/概念  |MongoDB术语/概念    | 解释/说明   |
|---|---|---|
|database   |database   |数据库   |
|table   |collection   |数据库表/集合   |
|row   |document   |数据记录行/文档   |
|column   |field   |数据字段/域   |
|index   |index   |索引   |
|table joins  | 不支持  |表连接,MongoDB不支持   |
|primary key    |primary key   |主键,MongoDB自动将_id字段设置为主键   |




## 一、 MySQL 数据库

### 1.1、 基本使用

#### 1.1.1、 安装
    a、 安装数据库：
        sudo apt-get install mysql-server 
    b、登陆数据库：
        mysql -uroot -p123123

安装后没有设置密码：

    在安装完成后，会生成/etc/mysql/debian.cnf这个文件，这里面就有初始的用户和随机的密码，用这个就可以登录了，然后再修改密码即可，
    另外，在修改root密码的时候，记得要把plugin这个字段设置为mysql_native_password，不然可能会进不去

修改数据库密码：

    # 数据库中-更新表
    use mysql;
    update user set authentication_string=password("123123") where user="root";     # 更新密码
    update user set plugin="mysql_native_password"; 
    flush privileges;
    quit;
    
    # 数据库外-重启数据库服务
    sudo service mysql restart


#### 1.1.2、 使用数据库

    数据库操作：
        a、查看数据库：
            show databases;
        b、创建数据库：
            create database [if not exists] db_name;
        c、、使用数据库：
            use db_name;
        d、删除库：
            drop database [if exists] db_name;
    
    数据表操作：       
        a、查看数据表：
            show tables;
        b、创建数据库表：
            create table [if not exists]  tb_name
        c、显示创建表的信息：
            show create table tb_name;
        d、删除表：
            drop table tb_name;


​            
​            
#### 1.1.3、 MySQL表操作：
    插入字段：
        a、指定字段插入： 
            INSERT INTO tb_name(field_name)  VALUES (field_values);
        b、全字段插入： 
            INSERT INTO tb_name VALUES (all_values);
        c、多行插入： 
            INSERT INTO tb_name(field_name) VALUES (value_1), (value_2), …;
    
    查询字段：
        a、指定字段查询：
            SELECT field_names FROM tb_name;
        b、全字段查询： 
            SELECT * FROM tb_name;
        c、带条件的查询： 
            SELECT field_names FROM tb_name WHERE conditions; 
    
    更新字段：
        a、修改所有数据：
            UPDATE  tb_name  SET field_1=value_1
        b、修改多个： 
            UPDATE  tb_name  SET field_1=value_1, field_2=value_2 …; 
        c、修改满足条件的数据： 
            UPDATE  tb_name  SET field_1=value_1  WHERE  conditions; 
    
    删除字段：
        a、删除表中所有数据：
            DELETE  FROM  tb_name;
        b、删除表中满足条件的数据： 
            DELETE  FROM  tb_name  WHERE  conditions;


#### 1.1.4、 数据库中使用的类型
###### 1.1.4.1、 数值类型
MySQL支持所有标准SQL数值数据类型。
这些类型包括严格数值数据类型(INTEGER、SMALLINT、DECIMAL和NUMERIC)，以及近似数值数据类型(FLOAT、REAL和DOUBLE PRECISION)。
关键字INT是INTEGER的同义词，关键字DEC是DECIMAL的同义词。
BIT数据类型保存位字段值，并且支持MyISAM、MEMORY、InnoDB和BDB表。
作为SQL标准的扩展，MySQL也支持整数类型TINYINT、MEDIUMINT和BIGINT。下面的表显示了需要的每个整数类型的存储和范围。 

|类型 	    |大小 	|用途|
|:----------| :-------------|:------------|
|TINYINT 	|1 字节 	 |小整数值|
|SMALLINT 	|2 字节 	 |大整数值
|MEDIUMINT 	|3 字节 	 |大整数值
|INT或INTEGER 	|4 字节 	|大整数值
|BIGINT 	|8 字节 		|极大整数值
|FLOAT 	    |4 字节 	|单精度浮点数值
|DOUBLE 	|8 字节 |双精度浮点数值


###### 1.1.4.2、 字符串类型

|类型 	    |大小 	        |用途
|:----------|:--------------|:------------
|CHAR 	    |0-255字节 	    |定长字符串
|VARCHAR 	|0-65535字节 	|变长字符串
|TINYBLOB 	|0-255字节 	    |不超过 255 个字符的二进制字符串
|TINYTEXT 	|0-255字节 	    |短文本字符串
|BLOB 	    |0-65 535字节 	|二进制形式的长文本数据
|TEXT 	    |0-65 535字节 	|长文本数据
|MEDIUMBLOB |0-16 777 215字节 	|二进制形式的中等长度文本数据
|MEDIUMTEXT |0-16 777 215字节 	|中等长度文本数据
|LONGBLOB 	|0-4 294 967 295字节 	|二进制形式的极大文本数据
|LONGTEXT 	|0-4 294 967 295字节 	|极大文本数据 


###### 1.1.4.3、 时间日期类型
|类型 	|大小(字节) 	|范围 	|格式 	|用途
|:----------|:-------------|:----------|:-------------|:-------------
|DATE 	    |3 	|1000-01-01/9999-12-31 	    |YYYY-MM-DD 	|日期值
|TIME 	    |3 	|'-838:59:59'/'838:59:59' 	|HH:MM:SS 	|时间值或持续时间
|YEAR 	    |1 	|1901/2155 	                |YYYY 	    |年份值
|DATETIME 	|8 	|1000-01-01 00:00:00/9999-12-31 23:59:59 	|YYYY-MM-DD HH:MM:SS 	|混合日期和时间值
|TIMESTAMP 	|4 	|1970-01-01 00:00:00/2038 结束时间是第 2147483647 秒，北京时间 2038-1-19 11:14:07，格林尼治时间 2038年1月19日 凌晨 03:14:07 |YYYYMMDD HHMMSS 	|混合日期和时间值，时间戳 


###### 1.1.4.4、 案例：

    create table tb2
    ( id INT,			     
    name VARCHAR(20), 		#指定长度，最多65535个字符。   变长字符串     
    sex  CHAR(4),         		#指定长度，最多255个字符。     定长字符串     
    price DOUBLE(4,2),		#双精度浮点型，m总个数，d小数位     
    detail text,			#可变长度，最多65535个字符      
    dates DATETIME,		        #日期时间类型 YYYY-MM-DD HH:MM:SS     
    ping  ENUM('好评','差评')  	#枚举， 在给出的value中选择
    )
    
    使用案例：
    insert into tb value (1, '裤子', '男', 20.0, '这条裤子超级好！！！', now(), '好评');



#### 1.1.5、 高级使用方法

    a、筛选条件
    b、聚合与分组
    c、子查询
    d、连接查询

###### 1.1.5.1、 筛选条件

![](.Note_images/4e5d73d2.png)

    a、比较运算符：
        等于：    = （ 注意！不是 == ）
        大于等于： >=
        不等于：  != 或 <>
        大于：    >
        小于：    <
        小于等于： <=
        IS NULL
        IS NOT NULL
    b、逻辑运算符：
        and
        or
        not
    c、其他操作：
        1、排序(order by)：
            正序：asc（默认）  
            倒序：desc
            SELECT columns FROM tb_name ORDER BY col [asc/desc];
        2、限制(limit)：
            LIMIT  count;
            LIMIT  start, count;
            SELECT columns FROM tb_name  LIMIT start, count ; 
        3、去重(distinct)：
            SELECT DISTINCT FROM tb_name;
        4、模糊查询  like ‘%’
            1. 任意多个字符： %
            2、任意一个字符： _
        5、范围查询：
            1. 连续范围： BETWEEN a AND b 
                a <= value <= b
            2. 间隔返回： IN
                a in (10, 20, 30 […])



​          


###### 1.1.5.2、 聚合与分组（重点和难点）
    a、常用聚合函数
    b、分组查询(group by)
    c、聚合筛选(having)

![](.Note_images/fa3b795b.png)

    常用聚合函数：
        统计个数：COUNT(column)
        求和：SUM(column)
        最大值：MAX(column)
        最小值：MIN（column）
        平均值：AVG(column)
        列出字段全部值：GROUP_CONCAT(column)
    
    分组查询(group by)：
        Select 字段 from 表 group by 字段;
        Select 字段，count(*) from 表 group by 字段
        在分组的情况下，只能够出现分组字段和聚合字段其他的字段没有意义，会报错！
        
    聚合筛选(having):
        Select 字段1 from 表名 group by 字段1，字段2 having 字段2>=80;
        加having条件表达式，可以对输出的结果做出限制
        
        假如说一个查询语句中同时包含了别名(as)，聚合函数， where, having那么他们的执行顺序是
        先是执行：where
        然后执行：聚合函数和别名
        最后执行：having


​        
​        
###### 1.1.5.3、 子查询（了解）
    将一个查询的结果留下来用于下一次查询 ( select 中嵌套 select 

要求：
1)嵌套在查询内部
2)必须始终出现在圆括号内

    求出学生的平均年龄
        select avg(age) from students;
    查找出大于平均年龄的数据
        select * from student where age > 19.7273;
    将求出的平均年龄的SQL语句用于查找大于平均年龄的语句中
        select * from students where age > (select avg(age) from students);


###### 1.1.5.4、 连接查询（了解）
    a、内连接(inner join)
    b、

内连接(inner join)
    无条件内连接：
        无条件内连接，又名交叉连接/笛卡尔连接第一张表种的每一项会和另一张表的每一项依次组合
        select * from student [inner] join scoren
    有条件内连接：
        在无条件内链接的基础上，加上一个on子句当连接的时候，筛选出那些有实际意义的记录来进行组合
         select * from student inner join scoren  on dept_id = id;

外连接( {left | right} join )
    左外连接： 
        （以左表为基准）两张表做连接的时候，在连接条件不匹配的时候留下左表中的数据，而右表中的数据以NULL填充
         select * from  student  left join  department   on dept_id= d_id;
    右外连接： 
        （以右表为基准）对两张表做连接的时候，在连接条件不匹配的时候留下右表中的数据，而左表中的数据以NULL填充  
         select * from  student right join department  on dept_id= d_id; 
         



#### 1.1.6、 表结构修改

|修改内容   |语法   |
|---|---|
|修改==表名==   |alter table 表名 rename to 新表名;   |
|修改==字段名==   |alter table tb_name change name new_name data_type;    |
|修改==字段类型==   |alter table tb_name modify field_name data_type;   |
|==添加字段==   |alter table tb_name add [COLUMN] field_name data_type;   |
|==删除字段==   |alter table tb_name drop [COLUMN] field_name;   |

#### 1.1.7、 约束条件

    约束是一种限制，通过对表中的数据做出限制，来确保表中数据的完整性，唯一性

|约束类型   |默认   |非空   |唯一   |自增长   |主键  |外键   |
|----|----|---|----|---|---|----|
|关键字   |default   |not null   |unique key   |auto_increment   |primary key  |foreign key   |





==默认约束(default)==

    CREATE TABLE tb(    
    id int default ‘a’ ,    
    name varchar(20)
    );

插入数据的时候，如果没有明确为字段赋值，则自动赋予默认值

在没有设置默认值的情况下，默认值为NULL



==非空约束(not null)==

    CREATE TABLE tb(    
    id int not null,    
    name varchar(20)
    );

限制一个字段的值不能为空，Insert的时候必须为该字段赋值

空字符不等于NULL

==唯一约束(unique key)==

CREATE TABLE tb(    
id int unique key,    
name varchar(20)
);

限制一个字段的值不重复，该字段的数据不能出现重复的

确保字段中值的唯一

==主键约束(primary key)==

CREATE TABLE tb(    
id int primary key,    
name varchar(20)
);

通常每张表都需要一个主键来体现唯一性每张表里面只能有一个主键

主键  =  非空 + 唯一

==自增长约束(auto_increment)==

CREATE TABLE tb(    
id int auto_increment,   
name varchar(20)
);

自动编号，和主键组合使用，一个表里面只能有一个自增长

auto_increment 要求用在主键上

==外键约束(foreign key)==
    

    保持数据的一致性我有的你一定有， 你没有的， 我绝对没有
    
    1. B表中的id_b字段，只能添加 id_a中已有的数据。
    2. A表中id_a  被参照的数据， 不能被修改和删除

CREATE TABLE a(    
id_a int primary key,    
name varchar(20)
);


CREATE TABLE b(    
id_b int primary key,    
name varchar(20),    
foreign key (id_b) references a(id_a)
);




#### 1.1.8、 表关系

选课系统(E-R图)


###### 1.1.8.1、 一对一
一对一关系(学生详情)
      
    举例，学生表中有学号、姓名、学院，但学生还有些比如电话，家庭住址等比较私密的信息，
    这些信息不会放在学生表当中，会新建一个学生的详细信息表来存放。    
    这时的学生表和学生的详细信息表两者的关系就是一对一的关系，因为一个学生只有一条详细信息。
    用主键加主键的方式来实现这种关系。
一对一 ： 用外键的方式，把两个表的主键关联
              
    #建立详细学生表：
    create table student_details(    
    id int primary key,    
    sex varchar(20) not null,    
    age  int,    
    address varchar(20) comment '家庭住址',    
    parents varchar(20),    
    home_num varchar(20),    
    foreign key (id) references student(s_id)
    );

###### 1.1.8.2、 一对多
一对多关系(学生所在学院)
    
    举例，通常情况下，学校中一个学院可以有很多的学生，而一个学生只属于某一个学院。 
         学院与学生之间的关系就是一对多的关系，通过外键关联来实现这种关系。
    
    ##创建学院表
    create table department(    
    d_id int primary key auto_increment,      # 学院
    id   d_name varchar(20) not null    # 学院名
    );
    
    ##创建学生表
    create table student(   
    s_id int primary key auto_increment,      # 学生
    id   s_name varchar(20) not null,         # 学生名字   
    dept_id int not null,		              # 所属学院 
    id    foreign key(dept_id) references department(d_id)   #外键
    );
    
    insert into department values(1,'外语学院'),(2,'计算机学院');
    insert into student values(1,'佳能',2),(2,'lucky',1);

###### 1.1.8.3、 多对多
多对多关系(学生选课)

    举例，学生要报名选修课，一个学生可以报名多门课程，一个课程有很多的学生报名，那么学生表和课程表两者就形成了多对多关系。    
    对于多对多关系，需要创建中间表实现。
    
    #建立课程表：
    create table cours(    
    cours_id int primary key auto_increment,    
    cours_name varchar(20) not null 
    );
    
    # 选课表  (中间表)create table  middle(   
     s_id int,       	 #用来记录学生id    
     cours_id int,  	 #用来记录 课程
     id  primary key(s_id,cours_id),                # 联合主键     
     foreign key(s_id) references student(s_id),       #  关联学生
     id  foreign key(cours_id) references cours(cours_id)  # 关联 课程id
     );


​    
​     insert into cours values (1, ’python编程’),  (2, ’大学英语’),  (3, ‘音乐鉴赏’);
​     insert into `select` values(1,3);   表示学号为一的同学选择了音乐鉴赏这门课程

 


 ![](.MySql_images/03e28229.png)






​    

### 1.2、 Python + MySQL
```python
# 1、 导入包
import pymysql


# 2、 设置数据库配置
db_config = {
    'host': 'localhost',
    'port': 3306,
    'user': 'root',
    'password': '123123',
    'db': 'zx_test',
    'charset': 'utf8'
}

# 3、 连接数据库
conn = pymysql.Connect(**db_config)

# 4、 获取游标
cursor = conn.cursor()

# sql 语句：创建数据库表格 tb1
sql_create_table = "create table if not exists tb1(" \
                   "id INT," \
                   "name VARCHAR(20)," \
                   "sex  CHAR(4)," \
                   "detail text)"

cursor.execute(sql_create_table)

# sql 语句：插入数据
sql_insert_table = "insert into tb1 values(1, 'zx1', 'nan', 1537564916)"
cursor.execute(sql_insert_table)


# 执行SQL，并返回收影响行数
effect_row = cursor.execute("select * from tb7")
  
# 执行SQL，并返回受影响行数
# effect_row = cursor.execute("update tb7 set pass = '123' where nid = %s", (11,))
  
# 执行SQL，并返回受影响行数,执行多次
# effect_row = cursor.executemany("insert into tb7(user,pass,licnese)values(%s,%s,%s)", [("u1","u1pass","11111"),("u2","u2pass","22222")])

# 提交，不然无法保存新建或者修改的数据
conn.commit()
  
# 关闭游标
cursor.close()

# 关闭连接
conn.close()

```

    cursor.fetchone()       # 获取剩余结果的第一行数据
    cursor.fetchmany(n)     # 获取剩余结果前n行数据
    cursor.fetchall()       # 获取剩余结果所有数据
    
    #获取自增id  可以获取到最新自增的ID，也就是最后插入的一条数据ID (有插入记录才行)
    new_id = cursor.lastrowid  
    
    # fetch数据类型：  关于默认获取的数据是元祖类型，如果想要或者字典类型的数据，即：
    cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)


```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-

import pymysql


# 连接数据库
db_config = {
    'host': 'localhost',
    'port': 3306,
    'user': 'root',
    'password': '123123',
    'db': 'zx_test',
    'charset': 'utf8'
}

conn = pymysql.Connect(**db_config)


# 获取游标
cursor = conn.cursor()

# cursor执行sql语句
# sql = "select * from test1;"
# cursor.execute(sql)
# print(cursor.rowcount)


"""
    获取了以后 cursor 里就没有了相关记录
    
fetchall()
fetchone()
fetchmany()
"""
# 获取所有数据
# print(cursor.fetchall())
# 显示一条数据
# print(cursor.fetchone())
# 指定显示几条 记录
# print(cursor.fetchmany(4))


"""
插入数据：
    1、 insert
    2、 提交事务
"""
# sql_insert = "insert into test1 values(1, 'aaa')"
# result_insert = cursor.execute(sql_insert)


sql_create_table = "create table if not exists tb1(" \
                   "id INT," \
                   "name VARCHAR(20)," \
                   "sex  CHAR(4)," \
                   "detail text)"


cursor.execute(sql_create_table)


sql_insert_table = "insert into tb1 values(1, 'zx1', 'nan', 1537564916),(2, 'zx2', 'nv', 123456789)"
cursor.execute(sql_insert_table)


def find_if_exits_in_table(tb_name, key_, value_):
    sql_find_from_table = "select * from %s where %s='%s';" % (tb_name, key_, value_)
    # sql_find_from_table = select * from tb1 where name='zx1';

    cursor.execute(sql_find_from_table)
    if cursor.fetchall():
        print("数据库有记录")
        return 1
    else:
        print("数据库无记录")
        return 0


def insert_into_table(table_name, **values):
    sql_desc_table = "desc %s" % table_name
    cursor.execute(sql_desc_table)
    # print(cursor.fetchall())
    for i in cursor.fetchall():
        print(i[0], i[1])


bool_ = find_if_exits_in_table('tb1', 'name', 'zx1')
insert_into_table('tb1')

conn.commit()


```


### 1.3、 关于pymysql防注入

#### 1、字符串拼接查询，造成注入

正常查询语句：

```python

#! /usr/bin/env python
# -*- coding:utf-8 -*-
# __author__ = "TKQ"
import pymysql
 
conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='', db='tkq1')
cursor = conn.cursor()
user="u1"
passwd="u1pass"
#正常构造语句的情况
sql="select user,pass from tb7 where user='%s' and pass='%s'" % (user,passwd)
#sql=select user,pass from tb7 where user='u1' and pass='u1pass'
row_count = cursor.execute(sql) 
row_1 = cursor.fetchone()
print(row_count,row_1)
 
conn.commit()
cursor.close()
conn.close()

```

其实用户可以这样输入实现免帐号登录：
username： ‘or 1 = 1 –-
password：
如若没有做特殊处理,那么这个非法用户直接登陆进去了.
当输入了上面的用户名和密码，服务端的sql就变成：
sql = "select user,pwd from User where user=‘'or 1 = 1 –-' and pwd='%s'"
因为条件后面username=”or 1=1 用户名等于 ” 或1=1 那么这个条件一定会成功；然后后面加两个-，这意味着注释，它将后面的语句注释，让他们不起作用，这样语句永远都能正确执行，用户轻易骗过系统，获取合法身份。


构造注入语句：

```python

#! /usr/bin/env python
# -*- coding:utf-8 -*-
# __author__ = "TKQ"
import pymysql
 
conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='', db='tkq1')
cursor = conn.cursor()
 
user="u1' or '1'-- "
passwd="u1pass"
sql="select user,pass from tb7 where user='%s' and pass='%s'" % (user,passwd)
 
#拼接语句被构造成下面这样，永真条件，此时就注入成功了。因此要避免这种情况需使用pymysql提供的参数化查询。
#select user,pass from tb7 where user='u1' or '1'-- ' and pass='u1pass'
 
row_count=cursor.execute(sql)
row_1 = cursor.fetchone()
print(row_count,row_1)
 
 
conn.commit()
cursor.close()
conn.close()

```


#### 2、避免注入，使用pymysql提供的参数化语句
    #执行参数化查询
    row_count=cursor.execute("select user,pwd from User where user='%s' and pwd='%s'" ,(username,password))
    #execute()函数本身就有接受SQL语句变量的参数位，只要正确的使用（直白一点就是：使用”逗号”，而不是”百分号”）就可以对传入的值进行correctly转义，从而避免SQL注入的发生。
    
    #内部执行参数化生成的SQL语句，对特殊字符进行了加\转义，避免注入语句生成。
    # sql=cursor.mogrify("select user,pwd from User where user='%s' and pwd='%s'" ,(username,password))
    # print (sql)

正常参数化查询:
```python

#! /usr/bin/env python
# -*- coding:utf-8 -*-
# __author__ = "TKQ"
 
import pymysql
 
conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='', db='tkq1')
cursor = conn.cursor()
user="u1"
passwd="u1pass"
#执行参数化查询
row_count=cursor.execute("select user,pass from tb7 where user=%s and pass=%s",(user,passwd))
row_1 = cursor.fetchone()
print(row_count,row_1)
 
conn.commit()
cursor.close()
conn.close()

```

构造注入，参数化查询注入失败:
```python

#! /usr/bin/env python
# -*- coding:utf-8 -*-
# __author__ = "TKQ"
import pymysql
 
conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='', db='tkq1')
cursor = conn.cursor()
 
user="u1' or '1'-- "
passwd="u1pass"
#执行参数化查询
row_count=cursor.execute("select user,pass from tb7 where user=%s and pass=%s",(user,passwd))
#内部执行参数化生成的SQL语句，对特殊字符进行了加\转义，避免注入语句生成。
# sql=cursor.mogrify("select user,pass from tb7 where user=%s and pass=%s",(user,passwd))
# print sql
#select user,pass from tb7 where user='u1\' or \'1\'-- ' and pass='u1pass'被转义的语句。
 
row_1 = cursor.fetchone()
print(row_count,row_1)
 
conn.commit()
cursor.close()
conn.close()

```

结论：excute执行SQL语句的时候，必须使用参数化的方式，否则必然产生SQL注入漏洞


#### 3、使用存mysql储过程动态执行SQL防注入
使用MYSQL存储过程自动提供防注入，动态传入SQL到存储过程执行语句:









## 二、 Redis 数据库
    Linux下安装：
        sudo apt install redis-server
        sudo apt install redis-tools
    登录：
        redis-cli



### 2.1、 Redis 基础

#### 2.1.1、 Redis 简介
    Redis 是完全开源免费的，遵守BSD协议，是一个高性能的key-value数据库。
    
    Redis 与其他 key - value 缓存产品有以下三个特点：
        1、 Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
        2、 Redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。
        3、 Redis支持数据的备份，即master-slave模式的数据备份。 

#### 2.1.2、 Redis 优势

    1、 性能极高 
            – Redis能读的速度是110000次/s,写的速度是81000次/s。
            
    2、 丰富的数据类型 
            – Redis支持二进制案例的 Strings, Lists, Hashes, Sets 及 Ordered Sets 数据类型操作。
            
    3、 原子 
            – Redis的所有操作都是原子性的，意思就是要么成功执行要么失败完全不执行。单个操作是原子性的。多个操作也支持事务，即原子性，通过MULTI和EXEC指令包起来。
            
    4、 丰富的特性 
            – Redis还支持 publish/subscribe, 通知, key 过期等等特性。

####　2.1.3、 Redis与其他key-value存储的不同

    1、 Redis有着更为复杂的数据结构并且提供对他们的原子性操作，这是一个不同于其他数据库的进化路径。
        Redis的数据类型都是基于基本数据结构的同时对程序员透明，无需进行额外的抽象。
    
    2、 Redis运行在内存中但是可以持久化到磁盘，所以在对不同数据集进行高速读写时需要权衡内存，因为数据量不能大于硬件内存。
        在内存数据库方面的另一个优点是，相比在磁盘上相同的复杂的数据结构，在内存中操作起来非常简单，这样Redis可以做很多内部复杂性很强的事情。
        同时，在磁盘格式方面他们是紧凑的以追加的方式产生的，因为他们并不需要进行随机访问。

#### 2.1.4、 Redis 配置
    查看配置命令：
        config get config_setting_name
        使用 * 号获取所有配置项
    编辑配置命令：
        config set config_setting_name config_setting_value

redis.conf 配置项说明如下：


#### 2.1.5、 Redis 数据类型
    Redis支持五种数据类型：string（字符串），hash（哈希），list（列表），set（集合）及zset(sorted set：有序集合)
    
    1、 String（字符串）
        string 是 redis 最基本的类型，你可以理解成与 Memcached 一模一样的类型，一个 key 对应一个 value。
        string 类型是二进制安全的。意思是 redis 的 string 可以包含任何数据。比如jpg图片或者序列化的对象。
        string 类型是 Redis 最基本的数据类型，string 类型的值最大能存储 512MB
        
    2、 Hash（哈希）
        Redis hash 是一个键值(key=>value)对集合。
        Redis hash 是一个 string 类型的 field 和 value 的映射表，hash 特别适合用于存储对象。
        
    3、 List（列表）
        Redis 列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素到列表的头部（左边）或者尾部（右边）
    
    4、 Set（集合）
        Redis 的 Set 是 string 类型的无序集合。
        集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)
        
        sadd 命令
        添加一个 string 元素到 key 对应的 set 集合中，成功返回 1，如果元素已经在集合中返回 0
    
    5、 zset(sorted set：有序集合)
        Redis zset 和 set 一样也是string类型元素的集合,且不允许重复的成员。
        不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。
        zset的成员是唯一的,但分数(score)却可以重复。
        
        zadd 命令
        添加元素到集合，元素在集合中存在则更新对应score
        zadd key score member 


​    
​    

### 2.2、 Redis 命令
    Redis 命令用于在 redis 服务上执行操作。
    要在 redis 服务上执行命令需要一个 redis 客户端。Redis 客户端在我们之前下载的的 redis 的安装包中。
    
    语法
        Redis 客户端的基本语法为：
            redis-cli
        在远程服务上执行命令：
            redis-cli -h host -p port -a password
    
    有时候会有中文乱码。
        要在 redis-cli 后面加上 --raw     就可以避免中文乱码了。
            redis-cli --raw

#### 2.2.1、 Redis 键(key)
    Redis 键命令用于管理 redis 的键。
    
    Redis 键命令的基本语法如下：


Redis keys 命令:
| 命令  |解释   |
|---|---|
|set key value   |设置/添加键值对  |
|get key   |查看对应key的值   |
|del key   | 该命令用于在 key 存在时删除 key  |
|dump key   | 序列化给定 key ，并返回被序列化的值  |
|exists key   | 检查给定 key 是否存在  |
|expire key  seconds |  为给定 key 设置过期时间，以秒计 |
|expireat key   | EXPIREAT 的作用和 EXPIRE 类似，都用于为 key 设置过期时间。 不同在于 EXPIREAT 命令接受的时间参数是 UNIX 时间戳(unix timestamp)  |
|pexpire key milliseconds  |设置 key 的过期时间以毫秒计   |
|pexpireat key   | milliseconds-timestamp  |
|keys pattern   | 查找所有符合给定模式( pattern)的 key  |
|move key db  | 将当前数据库的 key 移动到给定的数据库 db 当中  |
|persist key   | 移除 key 的过期时间，key 将持久保持  |
|pttl key   |以毫秒为单位返回 key 的剩余的过期时间   |
|ttl key   |以秒为单位，返回给定 key 的剩余生存时间(TTL, time to live)   |
|randomkey   |从当前数据库中随机返回一个 key    |
|rename key newkey   |修改 key 的名称   |
|renamenx key newkey    |仅当 newkey 不存在时，将 key 改名为 newkey   |
|type key|返回 key 所储存的值的类型 |



#### 2.2.2、 Redis 字符串(String)
    Redis 字符串数据类型的相关命令用于管理 redis 字符串值，基本语法如下：

Redis 字符串命令：
| 命令  |解释   |
|---|---|
|set key value   |设置指定 key 的值  |
|get key   |查看对应key的值   |
|getrange key start end   | 返回 key 中字符串值的子字符  |
|getset key value   |将给定 key 的值设为 value ，并返回 key 的旧值(old value)   |
|getbit key offset   |对 key 所储存的字符串值，获取指定偏移量上的位(bit)   |
|mget key1 [key2] [key3] ...   |获取所有(一个或多个)给定 key 的值   |
|setbit key offset value   | 对 key 所储存的字符串值，设置或清除指定偏移量上的位(bit)  |
|setex key seconds value   |将值 value 关联到 key ，并将 key 的过期时间设为 seconds (以秒为单位)   |
|setnx key value   |只有在 key 不存在时设置 key 的值   |
|setrange key offset value   | 用 value 参数覆写给定 key 所储存的字符串值，从偏移量 offset 开始  |
|strlen key   |返回 key 所储存的字符串值的长度   |
|mset key value [key value ...]   |同时设置一个或多个 key-value 对   |
|msetnx key value [key value ...]    |同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在   |
|psetex key milliseconds value   |这个命令和 SETEX 命令相似，但它以毫秒为单位设置 key 的生存时间，而不是像 SETEX 命令那样，以秒为单位   |
|incr key   |将 key 中储存的数字值增一   |
|incrby key increment   |将 key 所储存的值加上给定的增量值（increment）   |
|incrbyfloat key increment   |将 key 所储存的值加上给定的浮点增量值（increment）   |
|decr key   |将 key 中储存的数字值减一   |
|decrby key decrement   | key 所储存的值减去给定的减量值（decrement）  |
|append key value   |如果 key 已经存在并且是一个字符串， APPEND 命令将指定的 value 追加到该 key 原来值（value）的末尾   |



#### 2.2.3、 Redis 哈希(Hash)
    Redis hash 是一个 string 类型的 field 和 value 的映射表，hash 特别适合用于存储对象。
    Redis 中每个 hash 可以存储 232 - 1 键值对（40多亿）

Redis hash 命令：
| 命令  |解释   |
|---|---|
|hset key field value   |将哈希表 key 中的字段 field 的值设为 value   |
|hmset key field1 value1 [field2 value2 ]   |同时将多个 field-value (域-值)对设置到哈希表 key 中   |
|hmget key field1 [field2]   |获取所有给定字段的值   |
|hkeys key   |获取所有哈希表中的字段   |
|hvals key  |获取哈希表中所有值   |
|hlen key  |获取哈希表中字段的数量   |
|hdel key field1 [field2]  |删除一个或多个哈希表字段   |
|hexists key field |  查看哈希表 key 中，指定的字段是否存在   |
|hget key field   |获取存储在哈希表中指定字段的值   |
|hgetall key   |获取在哈希表中指定 key 的所有字段和值   |
|hincrby key field increment   |为哈希表 key 中的指定字段的整数值加上增量 increment   |
|hincrbyfloat key field increment   | 为哈希表 key 中的指定字段的浮点数值加上增量 increment   |
|hsetnx key field value   |只有在字段 field 不存在时，设置哈希表字段的值   |
|mscan key cursor [match pattern] [COUNT count]   | 迭代哈希表中的键值对  |



#### 2.2.4、 Redis 列表(List)
    Redis列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素到列表的头部（左边）或者尾部（右边）
    一个列表最多可以包含 232 - 1 个元素 (4294967295, 每个列表超过40亿个元素)
    
    L: 左边插入(表头)
    R: 右边插入(表尾)

Redis 列表命令：
| 命令  |解释   |
|---|---|
|lpush key value1 [value2]   |将一个或多个值插入到列表头部   |
|lpushx key value1 [value2]    |将一个值插入到已存在的列表头部   |
|lset key index value   |通过索引设置列表元素的值   |
|blpop key1 [key2 ] timeout   |移出并获取列表的第一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止   |
|brpop key1 [key2 ] timeout   |移出并获取列表的最后一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止   |
|brpoplpush source destination timeout   |从列表中弹出一个值，将弹出的元素插入到另外一个列表中并返回它； 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止   |
|lindex key index   |通过索引获取列表中的元素   |
|linsert  key before/after pivot value   |在列表的元素前/者后插入元素   |
|llen key   |获取列表长度   |
|lpop key   |移出并获取列表的第一个元素   |
|lrange key start stop   |获取列表指定范围内的元素   |
|lrem key count value   |移除列表元素   |
|ltrim key start stop   |对一个列表进行修剪(trim)，就是说，让列表只保留指定区间内的元素，不在指定区间之内的元素都将被删除   |
|rpop key   |移除列表的最后一个元素，返回值为移除的元素   |
|rpoplpush source destination   |移除列表的最后一个元素，并将该元素添加到另一个列表并返回   |
|rpush key value1 [value2]   |在列表中添加一个或多个值   |
|rpushx key value   |为已存在的列表添加值   |



#### 2.2.5、 Redis 集合(Set)
    Redis 的 Set 是 String 类型的无序集合。集合成员是唯一的，这就意味着集合中不能出现重复的数据。
    Redis 中集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)。
    集合中最大的成员数为 232 - 1 (4294967295, 每个集合可存储40多亿个成员)

Redis 集合命令:
| 命令  |解释   |
|---|---|
|sadd key member1 [member2]   |向集合添加一个或多个成员   |
|scard key   |获取集合的成员数   |
|sdiff key1 [key2]   |返回给定所有集合的差集   |
|sdiffstore destination key1 [key2]   |返回给定所有集合的差集并存储在 destination 中   |
|sinter key1 [key2]   |返回给定所有集合的交集   |
|sinterstore destination key1 [key2]   |返回给定所有集合的交集并存储在 destination 中   |
|sismember key member   |判断 member 元素是否是集合 key 的成员   |
|smembers key   |返回集合中的所有成员   |
|smove source destination member   |将 member 元素从 source 集合移动到 destination 集合   |
|spop key   |移除并返回集合中的一个随机元素   |
|srandmember key [count]   |返回集合中一个或多个随机数   |
|srem key member1 [member2]   |移除集合中一个或多个成员   |
|sunion key1 [key2]   |返回所有给定集合的并集   |
|sunionstore destination key1 [key2]   |所有给定集合的并集存储在 destination 集合中   |
|sscan key cursor [MATCH pattern] [COUNT count]   |迭代集合中的元素   |




#### 2.2.6、 Redis 有序集合(sorted set)
    Redis 有序集合和集合一样也是string类型元素的集合,且不允许重复的成员。
    不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。
    有序集合的成员是唯一的,但分数(score)却可以重复。
    集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是O(1)。 集
    合中最大的成员数为 232 - 1 (4294967295, 每个集合可存储40多亿个成员)。 

```shell script
redis 127.0.0.1:6379> ZADD runoobkey 1 redis
(integer) 1
redis 127.0.0.1:6379> ZADD runoobkey 2 mongodb
(integer) 1
redis 127.0.0.1:6379> ZADD runoobkey 3 mysql
(integer) 1
redis 127.0.0.1:6379> ZADD runoobkey 3 mysql
(integer) 0
redis 127.0.0.1:6379> ZADD runoobkey 4 mysql
(integer) 0
redis 127.0.0.1:6379> ZRANGE runoobkey 0 10 WITHSCORES
1) "redis"
2) "1"
3) "mongodb"
4) "2"
5) "mysql"
6) "4"
```

Redis 有序集合命令:
| 命令  |解释   |
|---|---|
|zadd key score1 member1 [score2 member2]   |向有序集合添加一个或多个成员，或者更新已存在成员的分数   |
|zcard key   |获取有序集合的成员数   |
|zcount key min max   |计算在有序集合中指定区间分数的成员数   |
|zincrby key increment member   |有序集合中对指定成员的分数加上增量 increment   |
|zinterstore destination numkeys key [key ...]   |计算给定的一个或多个有序集的交集并将结果集存储在新的有序集合 key 中   |
|zlexcount key min max   |在有序集合中计算指定字典区间内成员数量   |
|zrange key start stop [WITHSCORES]   |通过索引区间返回有序集合指定区间内的成员   |
|zrangebylex key min max [LIMIT offset count]   |通过字典区间返回有序集合的成员   |
|zrangebyscore key min max [WITHSCORES] [LIMIT]   |通过分数返回有序集合指定区间内的成员   |
|zrank key member   |返回有序集合中指定成员的索引   |
|zrem key member [member ...]   |移除有序集合中的一个或多个成员   |
|zremrangebylex key min max   |移除有序集合中给定的字典区间的所有成员   |
|zremrangebyrank key start stop   |移除有序集合中给定的排名区间的所有成员   |
|zremrangebyscore key min max   |移除有序集合中给定的分数区间的所有成员   |
|zrevrange key start stop [WITHSCORES]   |返回有序集中指定区间内的成员，通过索引，分数从高到低   |
|zrevrangebyscore key max min [WITHSCORES]   |返回有序集中指定分数区间内的成员，分数从高到低排序   |
|zrevrank key member   |返回有序集合中指定成员的排名，有序集成员按分数值递减(从大到小)排序   |
|zscore key member   |返回有序集中，成员的分数值   |
|zunionstore destination numkeys key [key ...]   |计算给定的一个或多个有序集的并集，并存储在新的 key 中   |
|zscan key cursor [MATCH pattern] [COUNT count]   |迭代有序集合中的元素（包括元素成员和元素分值）   |




#### 2.2.7、 Redis HyperLogLog
    Redis 在 2.8.9 版本添加了 HyperLogLog 结构。
    Redis HyperLogLog 是用来做基数统计的算法，HyperLogLog 的优点是，在输入元素的数量或者体积非常非常大时，计算基数所需的空间总是固定的、并且是很小的。
    在 Redis 里面，每个 HyperLogLog 键只需要花费 12 KB 内存，就可以计算接近 2^64 个不同元素的基 数。这和计算基数时，元素越多耗费内存就越多的集合形成鲜明对比。
    但是，因为 HyperLogLog 只会根据输入元素来计算基数，而不会储存输入元素本身，所以 HyperLogLog 不能像集合那样，返回输入的各个元素。 


什么是基数?
    
    比如数据集 {1, 3, 5, 7, 5, 7, 8}， 那么这个数据集的基数集为 {1, 3, 5 ,7, 8}, 基数(不重复元素)为5。 基数估计就是在误差可接受的范围内，快速计算基数。 

```shell script
redis 127.0.0.1:6379> PFADD runoobkey "redis"
1) (integer) 1

redis 127.0.0.1:6379> PFADD runoobkey "mongodb"
1) (integer) 1

redis 127.0.0.1:6379> PFADD runoobkey "mysql"
1) (integer) 1

redis 127.0.0.1:6379> PFCOUNT runoobkey
(integer) 3
```

Redis HyperLogLog 命令：
| 命令  |解释   |
|---|---|
|pfadd key element [element ...]   |添加指定元素到 HyperLogLog 中   |
|pfcount key [key ...]   |返回给定 HyperLogLog 的基数估算值   |
|pfmerge destkey sourcekey [sourcekey ...]   |将多个 HyperLogLog 合并为一个 HyperLogLog    |




#### 2.2.8、 Redis 发布订阅
    Redis 发布订阅(pub/sub)是一种消息通信模式：发送者(pub)发送消息，订阅者(sub)接收消息。
    Redis 客户端可以订阅任意数量的频道。
    
    假设有 频道 channel1 ， 以及订阅这个频道的三个客户端 —— client2 、 client5 和 client1 ，
    当有新消息通过 PUBLISH 命令发送给频道 channel1 时， 这个消息就会被发送给订阅它的三个客户端

```shell script
# 终端一：  建了订阅频道名为 redisChat:
redis 127.0.0.1:6379> SUBSCRIBE redisChat
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "redisChat"
3) (integer) 1

# 终端二：  重新开启个 redis 客户端，然后在同一个频道 redisChat 发布两次消息，订阅者就能接收到消息
redis 127.0.0.1:6379> PUBLISH redisChat "Redis is a great caching technique"
(integer) 1

redis 127.0.0.1:6379> PUBLISH redisChat "Learn redis by runoob.com"
(integer) 1

# 接受消息后的 终端一
127.0.0.1:6379> SUBSCRIBE redisChat
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "redisChat"
3) (integer) 1
1) "message"
2) "redisChat"
3) "Redis is a great caching technique"
1) "message"
2) "redisChat"
3) "Learn redis by runoob.com"
```

Redis 发布订阅命令：
| 命令  |解释   |
|---|---|
|psubscribe pattern [pattern ...]   |订阅一个或多个符合给定模式的频道   |
|pubsub subcommand [argument [argument ...]]   |查看订阅与发布系统状态   |
|publish channel message   |将信息发送到指定的频道   |
|punsubscribe [pattern [pattern ...]]   |退订所有给定模式的频道   |
|subscribe channel [channel ...]   |订阅给定的一个或多个频道的信息   |
|unsubscribe [channel [channel ...]]   |指退订给定的频道   |


#### 2.2.9、 Redis 事务

Redis 事务可以一次执行多个命令， 并且带有以下三个重要的保证：

    批量操作在发送 EXEC 命令前被放入队列缓存。
    收到 EXEC 命令后进入事务执行，事务中任意命令执行失败，其余的命令依然被执行。
    在事务执行过程，其他客户端提交的命令请求不会插入到事务执行命令序列中。

一个事务从开始到执行会经历以下三个阶段：

    开始事务。
    命令入队。
    执行事务。

单个 Redis 命令的执行是原子性的，但 Redis 没有在事务上增加任何维持原子性的机制，所以 Redis 事务的执行并不是原子性的。
事务可以理解为一个打包的批量执行脚本，但批量指令并非原子化的操作，中间某条指令的失败不会导致前面已做指令的回滚，也不会造成后续的指令不做。
比如：
```shell script
redis 127.0.0.1:7000> multi
OK
redis 127.0.0.1:7000> set a aaa
QUEUED
redis 127.0.0.1:7000> set b bbb
QUEUED
redis 127.0.0.1:7000> set c ccc
QUEUED
redis 127.0.0.1:7000> exec
1) OK
2) OK
3) OK
```
如果在 set b bbb 处失败，set a 已成功不会回滚，set c 还会继续执行。



Redis 事务命令：
| 命令  |解释   |
|---|---|
|multi   |标记一个事务块的开始   |
|discard   |取消事务，放弃执行事务块内的所有命令   |
|exec   |执行所有事务块内的命令   |
|unwatch   |取消 WATCH 命令对所有 key 的监视   |
|watch key [key ...]  |监视一个(或多个) key ，如果在事务执行之前这个(或这些) key 被其他命令所改动，那么事务将被打断   |




#### 2.2.10、 Redis 脚本
    Redis 脚本使用 Lua 解释器来执行脚本。 
    Redis 2.6 版本通过内嵌支持 Lua 环境。执行脚本的常用命令为 EVAL
    
     Eval 命令的基本语法如下：
        redis 127.0.0.1:6379> EVAL script numkeys key [key ...] arg [arg ...]

以下实例演示了 redis 脚本工作过程：
```shell script
redis 127.0.0.1:6379> EVAL "return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}" 2 key1 key2 first second
1) "key1"
2) "key2"
3) "first"
4) "second"
```

Redis 脚本命令：
| 命令  |解释   |
|---|---|
|EVAL script numkeys key [key ...] arg [arg ...]   |执行 Lua 脚本   |
|EVALSHA sha1 numkeys key [key ...] arg [arg ...]   |执行 Lua 脚本   |
|SCRIPT LOAD script   |将脚本 script 添加到脚本缓存中，但并不立即执行这个脚本   |
|SCRIPT EXISTS script [script ...]   |查看指定的脚本是否已经被保存在缓存当中   |
|SCRIPT FLUSH   |从脚本缓存中移除所有脚本   |
|SCRIPT KILL   |杀死当前正在运行的 Lua 脚本   |


#### 2.2.11、 Redis 连接
    Redis 连接命令主要是用于连接 redis 服务

以下实例演示了客户端如何通过密码验证连接到 redis 服务，并检测服务是否在运行：
```shell script
redis 127.0.0.1:6379> AUTH "password"
OK
redis 127.0.0.1:6379> PING
PONG
```

Redis 连接命令：
| 命令  |解释   |
|---|---|
|AUTH password   |验证密码是否正确   |
|ECHO message   |打印字符串   |
|PING   |查看服务是否运行   |
|QUIT   |关闭当前连接   |
|SELECT index   |切换到指定的数据库   |



#### 2.2.12、 Redis 服务器
    Redis 服务器命令主要是用于管理 redis 服务。

Redis 服务器命令：
| 命令  |解释   |
|---|---|
|INFO [section]   |获取 Redis 服务器的各种信息和统计数值   |
|client list   |获取连接到服务器的客户端连接列表   |
|client getname   |获取连接的名称   |
|client setname connection-name|设置当前连接的名称   |
|client kill [ip:port] [ID client-id]   |关闭客户端连接   |
|client pause timeout   |在指定时间内终止运行来自客户端的命令   |
|command   |获取 Redis 命令详情数组   |
|command count   |获取 Redis 命令总数   |
|command getkeys   |获取给定命令的所有键   |
|command info command-name [command-name ...]   |获取指定 Redis 命令描述的数组   |
|time   |返回当前服务器时间   |
|bgsave   |在后台异步保存当前数据库的数据到磁盘   |
|bgrewriteaof   |异步执行一个 AOF（AppendOnly File） 文件重写操作   |
|CONFIG get parameter   |获取指定配置参数的值   |
|CONFIG rewrite   |对启动 Redis 服务器时所指定的 redis.conf 配置文件进行改写   |
|CONFIG set parameter value   |修改 redis 配置参数，无需重启   |
|CONFIG resetstat   |重置 INFO 命令中的某些统计数据   |
|CLUSTER SLOTS   |获取集群节点的映射数组   |
|DBSIZE   |返回当前数据库的 key 的数量   |
|DEBUG OBJECT key   |获取 key 的调试信息   |
|DEBUG SEGFAULT   |让 Redis 服务崩溃   |
|FLUSHALL   |删除所有数据库的所有key   |
|FLUSHDB   |删除当前数据库的所有key   |
|LASTSAVE   |返回最近一次 Redis 成功将数据保存到磁盘上的时间，以 UNIX 时间戳格式表示   |
|MONITOR   |实时打印出 Redis 服务器接收到的命令，调试用   |
|ROLE   |返回主从实例所属的角色   |
|SAVE   |同步保存数据到硬盘   |
|SHUTDOWN [NOSAVE] [SAVE]   |异步保存数据到硬盘，并关闭服务器   |
|SLAVEOF host port   |将当前服务器转变为指定服务器的从属服务器(slave server)   |
|SLOWLOG subcommand [argument]   |管理 redis 的慢日志   |
|SYNC   |用于复制功能(replication)的内部命令   |

### 2.3、 Redis 高级















##  三、 MongoDB 数据库
    sudo apt install mongodb-server
    sudo apt install mongodb-clients

### 3.1、 MongoDB 基础

#### 3.1.1、 MongoDB 数据库操作

    连接数据库：
        mongo
    
    创建数据库：
        use batabase_name: 创建并使用数据库
    
    MongoDB 删除数据库：
        db.dropDatabase()    # 删除当前数据库，默认为 test，你可以使用 db 命令查看当前数据库名
    
    查看当前数据库：    
        db: 查看当前数据库
    
    查看所有数据库：
        show dbs 

可以看到，我们刚创建的数据库 runoob 并不在数据库的列表中， 要显示它，我们需要向 runoob 数据库插入一些数据
MongoDB 中默认的数据库为 test，如果你没有创建新的数据库，集合将存放在 test 数据库中

注意: 在 MongoDB 中，集合只有在内容插入后才会创建! 就是说，创建集合(数据表)后要再插入一个文档(记录)，集合才会真正创建

```shell script
> use zx_test
switched to db zx_test
> 
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
>
> db
zx_test
>
> db.zx_test.insert({name: "菜鸟教程"})
WriteResult({ "nInserted" : 1 })
> 
> show dbs
admin    0.000GB
config   0.000GB
local    0.000GB
zx_test  0.000GB
```


#### 3.1.2、 MongoDB 集合操作

    创建集合：
        db.createCollection(name, options)
        参数说明：    
            name: 要创建的集合名称
            options: 可选参数, 指定有关内存大小及索引的选项
    
    在 MongoDB 中，你不需要创建集合。当你插入一些文档时，MongoDB 会自动创建集合
    
    查看已有集合：
        show collections 
        show tables
    
    删除集合：
        db.collection_name.drop()
        如果成功删除选定集合，则 drop() 方法返回 true，否则返回 false


|字段 |	类型| 	描述|
|-----|-----|------|
|capped 	|布尔 	|（可选）如果为 true，则创建固定集合。固定集合是指有着固定大小的集合，当达到最大值时，它会自动覆盖最早的文档。当该值为 true 时，必须指定 size 参数。|
|autoIndexId 	|布尔 	|（可选）如为 true，自动在 _id 字段创建索引。默认为 false。|
|size 	|数值 	|（可选）为固定集合指定一个最大值，以千字节计（KB）。如果 capped 为 true，也需要指定该字段。|
|max 	|数值 	|（可选）指定固定集合中包含文档的最大数量。|


```shell script
# 查看有哪些集合
>use mydb
switched to db mydb
>
>show collections
mycol2
>

# 接着删除集合 mycol2 :
>db.mycol2.drop()
true
>
```


#### 3.1.3、 MongoDB 文档操作
    如何将数据插入到 MongoDB 的集合中。
    
    文档的数据结构和 JSON 基本一样。  
    所有存储在集合中的数据都是 BSON 格式。
    BSON 是一种类似 JSON 的二进制形式的存储格式，是 Binary JSON 的简称。
    
    插入文档： 
        MongoDB 使用 insert() 或 save() 方法向集合中插入文档，语法如下：
        db.COLLECTION_NAME.insert(document)
        db.COLLECTION_NAME.save(document)    # 如果不指定 _id 字段 save() 方法类似于 insert() 方法。如果指定 _id 字段，则会更新该 _id 的数据。 

##### 3.1.3.1、 文档插入：
```shell script
# 定义变量
document=({title: 'MongoDB 教程', 
    description: 'MongoDB 是一个 Nosql 数据库',
    by: '菜鸟教程',
    url: 'http://www.runoob.com',
    tags: ['mongodb', 'database', 'NoSQL'],
    likes: 100
});

# 执行后显示(定义变量后回车显示的)
{
        "title" : "MongoDB 教程",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb",
                "database",
                "NoSQL"
        ],
        "likes" : 100
}

# 插入变量
> db.col.insert(document)
WriteResult({ "nInserted" : 1 })
> 
```

##### 3.1.3.2、 文档更新：
MongoDB 使用 update() 和 save() 方法来更新集合中的文档。接下来让我们详细来看下两个函数的应用及其区别。

    update() 方法用于更新已存在的文档。语法格式如下：
    
    db.collection.update(
        <query>,
        <update>,
        {
            upsert: <boolean>,
            multi: <boolean>,
            writeConcern: <document>
        }
    )
    
    参数说明：
        query : update的查询条件，类似sql update查询内where后面的。
        update : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
        upsert : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
        multi : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
        writeConcern :可选，抛出异常的级别

```shell script
#　我们在集合 col 中插入如下数据：

>db.col.insert({
    title: 'MongoDB 教程', 
    description: 'MongoDB 是一个 Nosql 数据库',
    by: '菜鸟教程',
    url: 'http://www.runoob.com',
    tags: ['mongodb', 'database', 'NoSQL'],
    likes: 100
})

# 接着我们通过 update() 方法来更新标题(title):

>db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })   # 输出信息
> db.col.find().pretty()
{
        "_id" : ObjectId("56064f89ade2f21f36b03136"),
        "title" : "MongoDB",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb",
                "database",
                "NoSQL"
        ],
        "likes" : 100
}
>

#　以上语句只会修改第一条发现的文档，如果你要修改多条相同的文档，则需要设置 multi 参数为 true。
>db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}},{multi:true})
>
```
可以看到标题(title)由原来的 "MongoDB 教程" 更新为了 "MongoDB"。


    save() 方法
    save() 方法通过传入的文档来替换已有文档。语法格式如下：
    
    db.collection.save(
        <document>,
        {
            writeConcern: <document>
        }
    )
    
    参数说明：
        document : 文档数据。
        writeConcern :可选，抛出异常的级别。

```shell script
# 以下实例中我们替换了 _id 为 56064f89ade2f21f36b03136 的文档数据：

>db.col.save({
    "_id" : ObjectId("56064f89ade2f21f36b03136"),
    "title" : "MongoDB",
    "description" : "MongoDB 是一个 Nosql 数据库",
    "by" : "Runoob",
    "url" : "http://www.runoob.com",
    "tags" : [
            "mongodb",
            "NoSQL"
    ],
    "likes" : 110
})

# 替换成功后，我们可以通过 find() 命令来查看替换后的数据
>db.col.find().pretty()
{
        "_id" : ObjectId("56064f89ade2f21f36b03136"),
        "title" : "MongoDB",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "Runoob",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb",
                "NoSQL"
        ],
        "likes" : 110
}
> 
```

```shell script
# 更多实例

# 只更新第一条记录：
db.col.update( { "count" : { $gt : 1 } } , { $set : { "test2" : "OK"} } );

# 全部更新：
db.col.update( { "count" : { $gt : 3 } } , { $set : { "test2" : "OK"} },false,true );

# 只添加第一条：
db.col.update( { "count" : { $gt : 4 } } , { $set : { "test5" : "OK"} },true,false );

# 全部添加进去:
db.col.update( { "count" : { $gt : 5 } } , { $set : { "test5" : "OK"} },true,true );

# 全部更新：
db.col.update( { "count" : { $gt : 15 } } , { $inc : { "count" : 1} },false,true );

# 只更新第一条记录：
db.col.update( { "count" : { $gt : 10 } } , { $inc : { "count" : 1} },false,false );
```

##### 3.1.3.3、 文档删除：
    在执行remove()函数前先执行find()命令来判断执行的条件是否正确，这是一个比较好的习惯。
    
    remove() 方法的基本语法格式如下所示：
    db.collection.remove(
        <query>,
        {
            justOne: <boolean>,
            writeConcern: <document>
        }
    )
    
    参数说明：
        query :（可选）删除的文档的条件。
        justOne : （可选）如果设为 true 或 1，则只删除一个文档，如果不设置该参数，或使用默认值 false，则删除所有匹配条件的文档。
        writeConcern :（可选）抛出异常的级别。

```shell script
# 以下文档我们执行两次插入操作：

>db.col.insert({title: 'MongoDB 教程', 
    description: 'MongoDB 是一个 Nosql 数据库',
    by: '菜鸟教程',
    url: 'http://www.runoob.com',
    tags: ['mongodb', 'database', 'NoSQL'],
    likes: 100
})

# 使用 find() 函数查询数据：
> db.col.find()
{ "_id" : ObjectId("56066169ade2f21f36b03137"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb", "database", "NoSQL" ], "likes" : 100 }
{ "_id" : ObjectId("5606616dade2f21f36b03138"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb", "database", "NoSQL" ], "likes" : 100 }

# 接下来我们移除 title 为 'MongoDB 教程' 的文档：
>db.col.remove({'title':'MongoDB 教程'})
WriteResult({ "nRemoved" : 2 })           # 删除了两条数据
>db.col.find()                                               
>                                         # 没有数据
> 

# 如果你只想删除第一条找到的记录可以设置 justOne 为 1，如下所示：
>db.COLLECTION_NAME.remove(DELETION_CRITERIA,1)

# 如果你想删除所有数据，可以使用以下方式（类似常规 SQL 的 truncate 命令）：
>db.col.remove({})
>db.col.find()
>
```

##### 3.1.3.4、 文档查询：
    MongoDB 查询数据的语法格式如下：
        db.collection.find(query, projection)
    参数：
        query ：可选，使用查询操作符指定查询条件
        projection ：可选，使用投影操作符指定返回的键。查询时返回文档中所有键值， 只需省略该参数即可（默认省略）。
    
    如果你需要以易读的方式来读取数据，可以使用 pretty() 方法，语法格式如下：
        db.col.find().pretty()
    参数：
        pretty() 方法以格式化的方式来显示所有文档。
    
    除了 find() 方法之外，还有一个 findOne() 方法，它只返回一个文档


MongoDB 与 RDBMS Where 语句比较
如果你熟悉常规的 SQL 数据，通过下表可以更好的理解 MongoDB 的条件语句查询：
|操作 	|格式 	|范例 	|RDBMS中的类似语句|
|-------|-------|-------|---------------|
|等于 	|{<key>:<value>} 	|db.col.find({"by":"菜鸟教程"}).pretty() 	|where by = '菜鸟教程'|
|小于 	|{<key>:{$lt:<value>}} 	|db.col.find({"likes":{$lt:50}}).pretty() 	|where likes < 50|
|小于或等于 	|{<key>:{$lte:<value>}} 	|db.col.find({"likes":{$lte:50}}).pretty() 	|where likes <= 50|
|大于 	|{<key>:{$gt:<value>}} 	|db.col.find({"likes":{$gt:50}}).pretty() 	|where likes > 50|
|大于或等于 	|{<key>:{$gte:<value>}} 	|db.col.find({"likes":{$gte:50}}).pretty() 	|where likes >= 50|
|不等于 	|{<key>:{$ne:<value>}} 	|db.col.find({"likes":{$ne:50}}).pretty() 	|where likes != 50|


###### MongoDB AND 条件
    MongoDB 的 find() 方法可以传入多个键(key)，每个键(key)以逗号隔开，即常规 SQL 的 AND 条件。
    
    语法格式如下：
        db.col.find({key1:value1, key2:value2}).pretty()

```shell script
# 以下实例通过 by 和 title 键来查询 菜鸟教程 中 MongoDB 教程 的数据

> db.col.find({"by":"菜鸟教程", "title":"MongoDB 教程"}).pretty()
{
        "_id" : ObjectId("56063f17ade2f21f36b03133"),
        "title" : "MongoDB 教程",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb",
                "database",
                "NoSQL"
        ],
        "likes" : 100
}

# 以上实例中类似于 WHERE 语句：WHERE by='菜鸟教程' AND title='MongoDB 教程'
```

###### MongoDB OR 条件
    MongoDB OR 条件语句使用了关键字 $or,语法格式如下：
    
    db.col.find(
        {
            $or: [
                {key1: value1}, {key2:value2}
            ]
        }
    ).pretty()

```shell script
# 以下实例中，我们演示了查询键 by 值为 菜鸟教程 或键 title 值为 MongoDB 教程 的文档。
>db.col.find({$or:[{"by":"菜鸟教程"},{"title": "MongoDB 教程"}]}).pretty()
{
        "_id" : ObjectId("56063f17ade2f21f36b03133"),
        "title" : "MongoDB 教程",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb",
                "database",
                "NoSQL"
        ],
        "likes" : 100
}
>
```

###### AND 和 OR 联合使用
```shell script
# 以下实例演示了 AND 和 OR 联合使用，类似常规 SQL 语句为： 'where likes>50 AND (by = '菜鸟教程' OR title = 'MongoDB 教程')'
>db.col.find({"likes": {$gt:50}, $or: [{"by": "菜鸟教程"},{"title": "MongoDB 教程"}]}).pretty()
{
        "_id" : ObjectId("56063f17ade2f21f36b03133"),
        "title" : "MongoDB 教程",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb",
                "database",
                "NoSQL"
        ],
        "likes" : 100
}
```


#### 3.1.4、 MongoDB 条件操作符
    描述：
        条件操作符用于比较两个表达式并从mongoDB集合中获取数据。
        在本章节中，我们将讨论如何在MongoDB中使用条件操作符。
    
    MongoDB中条件操作符有：
        (>) 大于 - $gt
        (<) 小于 - $lt
        (>=) 大于等于 - $gte
        (<= ) 小于等于 - $lte

条件操作符：
|符号   |含义   |
|---|---|
|$gt   | >  |
|$gte  | >= |
|$lt   | <  |
|$lte  | <= |
|$ne   | != |
|$eq   | =  |


    模糊查询：
        查询 title 包含"教"字的文档：
            db.col.find({title:/教/})
            
        查询 title 字段以"教"字开头的文档：
            db.col.find({title:/^教/})
            
        查询 titl e字段以"教"字结尾的文档：
            db.col.find({title:/教$/})


##### 3.1.4.1、 MongoDB $type 操作符
    描述
        在本章节中，我们将继续讨论MongoDB中条件操作符 $type。
        $type操作符是基于BSON类型来检索集合中匹配的数据类型，并返回结果。

MongoDB 中可以使用的类型如下表所示：
|类型 	|数字 	|备注|
|-------|-------|---|
|Double |	1 |
|String |	2 |
|Object |	3 |
|Array 	|4 	 |
|Binary data 	|5|
|Undefined 	|6| 	已废弃|
|Object id 	|7 	 |
|Boolean 	|8 	 |
|Date 	|9 	 |
|Null 	|10 |
|Regular Expression |	11 |
|JavaScript |	13 	 |
|Symbol 	|14 	 |
|JavaScript (with scope) |	15|
|32-bit integer |	16 	 |
|Timestamp 	|17 	 |
|64-bit integer |	18|
|Min key 	|255 	Query with -1.|
|Max key 	|127 	 |

MongoDB 操作符 - $type 实例:
```shell script
# 简单的集合"col"：

>db.col.insert({
    title: 'PHP 教程', 
    description: 'PHP 是一种创建动态交互性站点的强有力的服务器端脚本语言。',
    by: '菜鸟教程',
    url: 'http://www.runoob.com',
    tags: ['php'],
    likes: 200
})


>db.col.insert({title: 'Java 教程', 
    description: 'Java 是由Sun Microsystems公司于1995年5月推出的高级程序设计语言。',
    by: '菜鸟教程',
    url: 'http://www.runoob.com',
    tags: ['java'],
    likes: 150
})


>db.col.insert({title: 'MongoDB 教程', 
    description: 'MongoDB 是一个 Nosql 数据库',
    by: '菜鸟教程',
    url: 'http://www.runoob.com',
    tags: ['mongodb'],
    likes: 100
})

# 使用find()命令查看数据：
> db.col.find()
{ "_id" : ObjectId("56066542ade2f21f36b0313a"), "title" : "PHP 教程", "description" : "PHP 是一种创建动态交互性站点的强有力的服务器端脚本语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "php" ], "likes" : 200 }
{ "_id" : ObjectId("56066549ade2f21f36b0313b"), "title" : "Java 教程", "description" : "Java 是由Sun Microsystems公司于1995年5月推出的高级程序设计语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "java" ], "likes" : 150 }
{ "_id" : ObjectId("5606654fade2f21f36b0313c"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb" ], "likes" : 100 }


# MongoDB 操作符 - $type 实例
# 如果想获取 "col" 集合中 title 为 String 的数据，你可以使用以下命令：

db.col.find({"title" : {$type : 2}})
# 或
db.col.find({"title" : {$type : 'string'}})

# 输出结果为：

{ "_id" : ObjectId("56066542ade2f21f36b0313a"), "title" : "PHP 教程", "description" : "PHP 是一种创建动态交互性站点的强有力的服务器端脚本语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "php" ], "likes" : 200 }
{ "_id" : ObjectId("56066549ade2f21f36b0313b"), "title" : "Java 教程", "description" : "Java 是由Sun Microsystems公司于1995年5月推出的高级程序设计语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "java" ], "likes" : 150 }
{ "_id" : ObjectId("5606654fade2f21f36b0313c"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb" ], "likes" : 100 }
```


##### 3.1.4.2、 MongoDB Limit与Skip方法
    MongoDB Limit() 方法
    如果你需要在MongoDB中读取指定数量的数据记录，可以使用MongoDB的Limit方法，limit()方法接受一个数字参数，该参数指定从MongoDB中读取的记录条数。
    注：如果你们没有指定limit()方法中的参数则显示集合中的所有数据。
    
    limit()方法基本语法如下所示：
        >db.COLLECTION_NAME.find().limit(NUMBER)


    MongoDB Skip() 方法
    我们除了可以使用limit()方法来读取指定数量的数据外，还可以使用skip()方法来跳过指定数量的数据，skip方法同样接受一个数字参数作为跳过的记录条数。
    注:skip()方法默认参数为 0 
    
    skip() 方法脚本语法格式如下：
        >db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER)


```shell script
# 总共有 3 条记录

# 以下实例为显示查询文档中的两条记录：
> db.col.find({},{"title":1,_id:0}).limit(2)
{ "title" : "PHP 教程" }
{ "title" : "Java 教程" }
>

# 以下实例只会显示第二条文档数据
>db.col.find({},{"title":1,_id:0}).limit(1).skip(1)
{ "title" : "Java 教程" }
>
```


#### 3.1.5、 MongoDB 排序

    在 MongoDB 中使用 sort() 方法对数据进行排序，
    sort() 方法可以通过参数指定排序的字段，并使用 1 和 -1 来指定排序的方式，其中 1 为升序排列，而 -1 是用于降序排列。
    
    sort()方法基本语法如下所示：
        db.COLLECTION_NAME.find().sort({KEY:1})

实例：
```shell script
# col 集合中的数据如下：
{ "_id" : ObjectId("56066542ade2f21f36b0313a"), "title" : "PHP 教程", "description" : "PHP 是一种创建动态交互性站点的强有力的服务器端脚本语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "php" ], "likes" : 200 }
{ "_id" : ObjectId("56066549ade2f21f36b0313b"), "title" : "Java 教程", "description" : "Java 是由Sun Microsystems公司于1995年5月推出的高级程序设计语言。", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "java" ], "likes" : 150 }
{ "_id" : ObjectId("5606654fade2f21f36b0313c"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库", "by" : "菜鸟教程", "url" : "http://www.runoob.com", "tags" : [ "mongodb" ], "likes" : 100 }

# 以下实例演示了 col 集合中的数据按字段 likes 的降序排列：
>db.col.find({},{"title":1,_id:0}).sort({"likes":-1})
{ "title" : "PHP 教程" }
{ "title" : "Java 教程" }
{ "title" : "MongoDB 教程" }
```


#### 3.1.6、 MongoDB 索引
    索引通常能够极大的提高查询的效率
    索引是特殊的数据结构，索引存储在一个易于遍历读取的数据集合中，索引是对数据库表中一列或多列的值进行排序的一种结构 
    
    createIndex()方法基本语法格式如下所示：
        db.collection.createIndex(keys, options)
    语法中 Key 值为你要创建的索引字段，1 为指定按升序创建索引，如果你想按降序来创建索引指定为 -1 即可

索引操作：  
|索引操作   |命令   |
|---|---|
|查看集合索引 | db.col.getIndexes()|
|查看集合索引大小 | db.col.totalIndexSize()|
|删除集合所有索引 | db.col.dropIndexes()|
|删除集合指定索引 | db.col.dropIndex("索引名称")|

实例：
```shell script
>db.col.createIndex({"title":1})
>
# createIndex() 方法中你也可以设置使用多个字段创建索引（关系型数据库中称作复合索引）
>db.col.createIndex({"title":1,"description":-1})
>
```

createIndex() 接收可选参数，可选参数列表如下：


|Parameter	|Type	|Description|
|-----------|-------|-----------|
|background	|Boolean	|建索引过程会阻塞其它数据库操作，background可指定以后台方式创建索引，即增加 "background" 可选参数。 "background" 默认值为false。|
|unique	    |Boolean	|建立的索引是否唯一。指定为true创建唯一索引。默认值为false.|
|name	    |string	    |索引的名称。如果未指定，MongoDB的通过连接索引的字段名和排序顺序生成一个索引名称。|
|dropDups	|Boolean	|3.0+版本已废弃。在建立唯一索引时是否删除重复记录,指定 true 创建唯一索引。默认值为 false.|
|sparse	    |Boolean	|对文档中不存在的字段数据不启用索引；这个参数需要特别注意，如果设置为true的话，在索引字段中不会查询出不包含对应字段的文档.。默认值为 false.|
|expireAfterSeconds	|integer	|指定一个以秒为单位的数值，完成 TTL设定，设定集合的生存时间。|
|v	        |index version	|索引的版本号。默认的索引版本取决于mongod创建索引时运行的版本。|
|weights	|document	|索引权重值，数值在 1 到 99,999 之间，表示该索引相对于其他索引字段的得分权重。|
|default_language	|string	|对于文本索引，该参数决定了停用词及词干和词器的规则的列表。 默认为英语|
|language_override	|string	|对于文本索引，该参数指定了包含在文档中的字段名，语言覆盖默认的language，默认值为 language.|


实例: 在后台创建索引 
```shell script
# 通过在创建索引时加 background:true 的选项，让创建工作在后台执行
>db.values.createIndex({open: 1, close: 1}, {background: true})
```


#### 3.1.7、 MongoDB 聚合
    MongoDB中聚合(aggregate)主要用于处理数据(诸如统计平均值,求和等)，并返回计算后的数据结果。有点类似sql语句中的 count(*)
    
    aggregate() 方法的基本语法格式如下所示：
        db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)

```shell script
# 向集合中插入三个数据

>db.writer.insert({
   _id: ObjectId('7df78ad8902c7df78ad8902c'),
   title: 'MongoDB Overview', 
   description: 'MongoDB is no sql database',
   by_user: 'runoob.com',
   url: 'http://www.runoob.com',
   tags: ['mongodb', 'database', 'NoSQL'],
   likes: 100
})
WriteResult({ "nInserted" : 1 })
> 
>db.writer.insert({
   _id: ObjectId('7df78ad8902d7df78ad8902d'),
   title: 'NoSQL Overview', 
   description: 'No sql database is very fast',
   by_user: 'runoob.com',
   url: 'http://www.runoob.com',
   tags: ['mongodb', 'database', 'NoSQL'],
   likes: 10
})
WriteResult({ "nInserted" : 1 })
>
>db.writer.insert({
   _id: ObjectId('7df78ad8902e7df78ad8902e'),
   title: 'Neo4j Overview', 
   description: 'Neo4j is no sql database',
   by_user: 'Neo4j',
   url: 'http://www.neo4j.com',
   tags: ['neo4j', 'database', 'NoSQL'],
   likes: 750
})
WriteResult({ "nInserted" : 1 })
>

# 通过以上集合计算每个作者所写的文章数，使用aggregate()计算结果如下：
# 按照 $by_user 分类统计， 计算不同的 $by_user 各有多少个
> db.writer.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : 1}}}])
# 输出：
{ "_id" : "Neo4j", 
  "num_tutorial" : 1 
}
{ "_id" : "runoob.com", 
  "num_tutorial" : 2 
}
> 

```
注意：
    1、：ObjectId的参数应该是字符串应该加 “”
    2、：_id对字符串似乎对长度有要求，24位如：5ce742df49b868781061e446，多一个或者少一个不能执行通过，

以上实例类似sql语句：
    select by_user, count(*) from mycol group by by_user

在上面的例子中，我们通过字段 by_user 字段对数据进行分组，并计算 by_user 字段相同值的总和。
下表展示了一些聚合的表达式:

|表达式	|描述	|实例|
|-------|-------|----|
|$sum	|计算总和。	|db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : "$likes"}}}])|
|$avg	|计算平均值	|db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$avg : "$likes"}}}])|
|$min	|获取集合中所有文档对应值得最小值。	|db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$min : "$likes"}}}])|
|$max	|获取集合中所有文档对应值得最大值。	|db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$max : "$likes"}}}])|
|$push	|在结果文档中插入值到一个数组中。	|db.mycol.aggregate([{$group : {_id : "$by_user", url : {$push: "$url"}}}])|
|$addToSet	|在结果文档中插入值到一个数组中，但不创建副本。	|db.mycol.aggregate([{$group : {_id : "$by_user", url : {$addToSet : "$url"}}}])|
|$first	|根据资源文档的排序获取第一个文档数据。	|db.mycol.aggregate([{$group : {_id : "$by_user", first_url : {$first : "$url"}}}])|
|$last	|根据资源文档的排序获取最后一个文档数据	|db.mycol.aggregate([{$group : {_id : "$by_user", last_url : {$last : "$url"}}}])|



##### ==管道的概念==

管道在Unix和Linux中一般用于将当前命令的输出结果作为下一个命令的参数。

MongoDB的聚合管道将MongoDB文档在一个管道处理完毕后将结果传递给下一个管道处理。管道操作是可以重复的。

表达式：处理输入文档并输出。表达式是无状态的，只能用于计算当前聚合管道的文档，不能处理其它的文档。

这里我们介绍一下聚合框架中常用的几个操作：

|表达式	|描述	|
|-------|-------|
|$project|修改输入文档的结构。可以用来重命名、增加或删除域，也可以用于创建计算结果以及嵌套文档|
|$match|用于过滤数据，只输出符合条件的文档。$match使用MongoDB的标准查询操作|
|$limit|用来限制MongoDB聚合管道返回的文档数|
|$skip|在聚合管道中跳过指定数量的文档，并返回余下的文档|
|$unwind|将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值|
|$group|将集合中的文档分组，可用于统计结果|
|$sort|将输入文档排序后输出|
|$geoNear|输出接近某一地理位置的有序文档|

管道操作符实例：
```shell script
# 1、$project实例
db.article.aggregate(
    { $project : {
        title : 1 ,
        author : 1 ,
    }}
 );

# 这样的话结果中就只还有_id,tilte和author三个字段了，默认情况下_id字段是被包含的，如果要想不包含_id话可以这样:
db.article.aggregate(
    { $project : {
        _id : 0 ,
        title : 1 ,
        author : 1
    }});

# 2.$match实例
db.articles.aggregate( [
                        { $match : { score : { $gt : 70, $lte : 90 } } },
                        { $group: { _id: null, count: { $sum: 1 } } }
                       ] );
# $match用于获取分数大于70小于或等于90记录，然后将符合条件的记录送到下一阶段$group管道操作符进行处理。

# 3.$skip实例
db.article.aggregate(
    { $skip : 5 });

# 经过$skip管道操作符处理后，前五个文档被"过滤"掉。 
```


#### 3.1.8、 MongoDB 复制(副本集)
    MongoDB复制是将数据同步在多个服务器的过程。
    复制提供了数据的冗余备份，并在多个服务器上存储数据副本，提高了数据的可用性， 并可以保证数据的安全性。
    复制还允许您从硬件故障和服务中断中恢复数据。

什么是复制?

    保障数据的安全性
    数据高可用性 (24*7)
    灾难恢复
    无需停机维护（如备份，重建索引，压缩）
    分布式读取数据

MongoDB复制原理

mongodb的复制至少需要两个节点。其中一个是主节点，负责处理客户端请求，其余的都是从节点，负责复制主节点上的数据。
mongodb各个节点常见的搭配方式为：一主一从、一主多从。
主节点记录在其上的所有操作oplog，从节点定期轮询主节点获取这些操作，然后对自己的数据副本执行这些操作，从而保证从节点的数据与主节点一致。 
MongoDB复制结构图如下所示：
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAfQAAAGZCAYAAAB/vMMOAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALKgAACyoBLWtHxwAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAACAASURBVHic7N13fBR1/sfx12ySTQIkECD0XqRspCgoIrqEIgkICCioZ++e5531cDn9IbZgQT3PghXsigVBJaEILAiCipUFFKR3CCUkpJDs/P6YZElIJ2XJ8n4+HkB25jszn92EfOZbxzBNExEREanZbP4OQERERCpOCV1ERCQAKKGLiIgEACV0ERGRAKCELiIiEgCU0EVERAKAErqIiEgACPZ3AFJ94uMG9QKeBqL8HYuIVIqNwF2JSQu2+jsQ8T8l9NNEfNygBsB36HsuEki6Az2Adv4ORPxPTe6nj1iUzEUCUdv4uEEd/B2E+J8S+unjXH8HICJVRv+/RQn9NBLi7wBEpMro/7cooYuIiAQCJXQREZEAoIQuIiISAJTQpcoZhoHdbvd3GCIiAU3TmKTS2e2h9O8fS+/evenStSt169YjODiYI0eOsGfPbnbv3s2PP/zA8uXfcuTIkQLHdujQkbvvuReAaW+9yY8//uCPt1CtwsLCeP2NtwgPr8Xrr73K3LmJ/g6pWC+9NBUM+HbpUj788H1/hyMi+SihS6UaPnwkV1z5N6KiCi9GFxERQUREBB06dKRfvwv4x53/5Jdffua116aybau10FVYeDjt2rUHoE6diALHN2nalHN6n8vSpUs4ePBA1b+ZajJw4GAaNowGYMyYS5k3LwnTNP0cVdHatmuHYRj8sW5dge21a9emf+wAPKtXs3nzJj9FV7Lg4GBiYweye/cufv/9N3+HI1LplNClUoSHh3PPvffTr98FBbZnZWWydetWdu3aSYP6DWneogV169YFrF+wvXr1Zu7cJF9CL05QUBBPPvkMjRo1ou/55/PA+Pur7L1Ut+EjRvi+btmqFb16ncMPP6z0Y0Tl9487/0n//gNIS0vj6quuJD39qL9DKuTSy8Zx7bXXYZomt956U6k/cyI1jRK6VFhQUBD/efD/OPvsXr5tv/76C6+9OpVNmzYWqm3WqRPB+ef345JRo2nTpk2ZruH1ejFNLwA52dmVFru/de/Rk9at2xTYNnrMmBqX0HNycgAwTS9eb46foylaXowA3pxTM0aRilBClwq7/oYbfck8IyODV6e+QlLSnGLLp6YeYe7cRObOTaRHj54cPny41GuYpsn4f99Pz55nsXz5t5UWe0X16tW7Qv38I0eMBKz3t2fPHpo0aUKPHj1p27YdmzZtrKwwq9zLL73I77/9jsezmszMTL/FUdL3Y+bnn7J/31527trFjh07qjkykaqnUe5SIc2bt+CSS0b7Xk995eUSk/mJfvnl5zInrj17dpOUNIeUlJRyx1kVRo4cxc233HrSxzdu3IQ+5/UFrM/hnben+faNHj2mwvFVp6NHjzJ3biLbt2/zWwxjx13ONddcV+z+7OxsFi1ayB/r1lZfUCLVSAldKuTSSy8jKCgIgO+WL6vSEdohISHY7XaCg0tuWKpduzYxZ3ajTZu2vtiKEhwcjN1uJyTk+KqZISEhdO3qIDo6usRrjB59Kbfd/ncMw4bdbvf9yX+u0lw8fDiGYQDw1ZdfsmSJm/379wHQP3YAUVH1iz02bypg/j82W9n+O+e975OJubRzlnYum81Gy5YtOevsXrRp06bE8rVq1SIm5kw6d+5CREREseUArrjib1x//Y0YNqPY92azHf9elYVhGGX6TPN/L/KXr1+/PjExZ1bK5ytSFmpyl5NmGAa9zzn+TIi33nqzSq83bfo7NGjQkJUrV/DwxIcK7e/UqTN33X0PrVu38SXKrKxMFiyYz6tTp5KVVbAp+LHHE+jevQd79+7l5ptu4I47/kHsgIG+X8CbN2/ipZdeZPUJI6IvvXQsN950MwAtW7Zk1uyvffsyMzO5ZOTFpb4Xuz2UIUPiAdi/fx8rVizH6/Uye9YsbrjxJoKDgxk+YgTvvD29yONjYs7kqaenFNjm9XrZt28vu3ftYt0f6/jkkxmkpaYWOnbSI49x1llnF9iWlpbG7t272LVrF3OTEsvdjXDPPfcRO2Ag6enpjB41otD+OnUi+Pvf7+D8fv2w20N929PTj7J82TJeeeUl0tLSAOjSpSv/uutuWrVq7fs+mqbJ/PlzefONN0hJKdhF87erruGqq64GrGmP+b8fKSmHGTf2UgDGjr2ca6+7HoBrrr6Sffv2FYqzUaPGXHHFlbRv34FWrVtjs9nYtm0rmzZu5OOPP2TbtsItEK1bt+aVqa8D8Mbrr7Has5p777mPlq1aAdbPxPLly3j+uSlkZWWV8RMVKT/V0OWkRUdH06BBA8D6xbxjx3a/xRI/dBjPTHmONm3aYhiGbwCU3R7K0KEX898XXqR2nTpFHlurVjjP//cFLhoSR3Z2ti8JtmnTlkmTHqVDh46+smPHXe5L5hUxYMBAX61zztdf4/VaA/7mJH5Neno6AMOGDS+Q/Epjs9lo3LgJ3Xv0ZNy4K3jrrbe5aEhcmY6tXbs27dt3oF+/C3j0sSd49NHHfVPpKqpDh45MffU1YgcMLPR+wsNrMXDQYOrWrQfAuef24elnni1wUwbWzeNFF8Xx6GOPF2ihufqaa33JvKIuuWQ0r772BnHxQ+l4xhmEhoYSEhJCu3btGThoMC+9/CqXX35lgbhOdH6/fjzzzLO0bNWKgwcPkJOTQ2hoKLGxA3BN+E+JLUYiFaUaupy0Bg0a+r7etHGT3+ZON2rUmNtuu53g4GBfrXrd2jXY7XYGDb6Im266hTZt2jBu7LgiWxHq1IkgJ8fLQw9O4JdffiY7O5tzz+3Dgw9NpFatWvzjzn9y17/uBOCvDRt46MEJXHvd9XTo0JG9e/fyvxee950rLzGXZsRIazBcdnY2SUnHuynSUlOZP28uI0ZeQmRkJIMGDWbOnK9KPNfcuYl4VnsIDw+nRcsWtGzZim7duhMZGcldd93D3j17+OWXnwsdl5aayquvTsUwDKIbNaJlyxZ06tSFJk2a0Kv3OTzgmsD9991Toe9rUFAQ9953v+9n5eeff2L2rFns3LmDRo0a0a1bNy4efrxG37RpM4KCgljj8eB2L2bt2jW0b9+B4SNG0K5de844oxO9e5/Dd98tx2azsXbNGh56cAI333IrrVq1ZseOHUx95SXf+Y6VcUbE0KEXc+ttt/s+ly+/ms1ff/1FcFAwHc/oyLBhwwkNDeXa664nKyuLzz//tMjzdOnSlSXuxUyb/ha7d+0iNDSUe++7nwsucNKnT18udPZn0cJvTvbjFCmRErqctPw1paNH0/wWx3XX34DdHkpaaioP/mcCycn7AStZzp71BbVr1eaaa69j5CWj+eyzTwuNqs/IyODf99/L1q1bfNtWrlzB8uXLuPBCJ2ec0YlatWpx9OhRVq36EYBRuYPWMjLSy908HXNmN9q2bQfA8mXfFlokZ+YXnzN8xEgMw2DU6NEkJn5dYlL1rPYwf/7cAtv6XXAh48e7CA4O5t777ueWm2/01fx97zszs9Bx4eHhPDzpUbp1647DEcPoMZfx2aczyvX+8ht28XDatGkLwLy5STz//LO+97J16xZ+/PEHPvlkBseOHQOspvVPZnzEtGlv+cqtX/8nycnJPPLoYwC0bdee776zuijyPvsrrvgbAEfT0sr9/WjevAW33HqbL6YJrgd8P0MAixcv5MvZs3js8ck0b96ca6+7nh9//KHAz0ue5cu/ZfLkJ3yxZ2Zm8urUV+jX70IMw6BHjx5K6FJl1OQuJ23Pnt2+r9vmru7mD2efbfUHL126pMAv4jxLliwGwG63+xJpfikpKUX+ct6wfj1gNfcWtfLdycqbqgZW3/WwYcML/Dn7rF7s2W19ti1atKR373PKfY1vly7hww8/AKBhw2g6depcpuPS09N56MH/cPSotTBMv379yn3t/M49tw9gfcavvTa1yBuTI0eOkJGRAcC8eUm89dabhcr9/PMqXzdKWFjZuyHKIi4+ntDQUEzTZMozTxf5M7R7926efvpJTNPEbrdz8fDhRZ5rjWdNodiTk5M5cMC6aatfv0Glxi6Sn2roctL27dvHsWPHCAkJoUGDBtSrV49Dhw5VawyRkXWJjLRWnju3z3m8fuaZhcrk7/Ns2qxZkc3PRclfk68TEQlUfO5ydHQ05/U93/c6fuiwUo8ZPXoM339f/oVmfvnlJ66++hrAWrK1rO87KyuTNWs89OrV29eXfbLN7nmL5qxbt9Y36K0kJ7Yi2O12evc+hwud/X0jyCt71Hj79h0A2L17F3/++Uex5f5Yt5bt27bRslUr2ua2OpTV4cOHaNCgARHFjOMQqQxK6HLSTNPku+XLuNDZH4DBF8XxyYyPqjWGRo0a+b5OSTlc5MhlgF27dgGQlVn2UcY5+VY8s5UwEKo8hl08vNwDo7r36Em79u3Z+Ndf5Touf/lmzZqV+9hevXoTHh5OVFSUr4ZZHna73Tdoct++veU6tnnz5lx62Viczv6Eh9fC41mNaZolDkg7WS1btgSO/4yUZOu2rbRs1YqWrVqX6xp5rQs2mwbFSdVRQpcK+eqrL30J/ZprruWH71dW68M58k9hWrHiO6ZPe6varl1edrud+PihgBX3Xf/6Z4mD6M7s1o1777XWrB89agzPPPNUua6Xf5T6nt17yndstDWILSsrk4MHD5br2DxZWVkcOnSIevXq0bhR4zIfFxc/lDvuuJPg4GCWLHHzztvT2LFjB7Nmf10lj+Hdu2cvDRtG06RJk1LL5t1A5q0XIHIqUR+6VMjvv//GTz+tAqxBcuMfcBWoNZcmOjqabt26n/T1k5OTfY9g7d37nDIvrlJRx3LnE5entu10xvq6BxIT57Br10727Nld7J9vFsz3LVHq7B9L/frFLzRTlPxzzctzkxUSEkJMjNV1sWXLlgqNct+Se93OXbr43ntJujoc/POfdxEcHMyUKU+T8MRjZVqm9dix8n8/8mz4yxor0bRpsxKfLdCsWXPfGIy/Nmwo93VEqpoSulTYU08m+AYStWnTlldfe5Mxl44t8Zdr8+YtuPvue3lr2jucc+65xZYrTU5Ojm/UcLt27bnm2uuKbJY1DIPBg4fQuXOXk75Wfqlp1lz1Zs2aExkZWaZj8qaqeb1evv7qy1LLm6bJzM8/A8hdaGZkKUccV79+fa7K7T8/cOAAHo+nzMdeceXfaJRbo166dGmZjyvKDz9YI87r1IngrrvuLraGnfc9i40dgGEYZGVllms0+JHctQNatW5NeHh4uWJc4nb7mvPvu398kd/P2rVrc++99/tmdixZ4i7XNUSqg5rcpcIOHz7MwxP/j4cnPUKDBg0JCwvjpptuZsyYMfz1119s2bKZ3bt2Ex0dbfU/tmxJ8+YtKq0/9MMP3+dCZ3/q1avHuHFX4HDEsGjhQnbs3EH9+vVp0aIFffv2o02bNjz88P9VyjXz+uoNw+C22+9g5uefYQsKsvqdw0J5443XC5Tv2tXhW6Bm+fJlxfb1n2j+/Hlcc+21REbWZdiw4Xz04QeFHn5yfr9+pKcfxeNZnVu77sbNt9zqW7jm5Zf+V+TjTGvXrs2YMZexevXvbN26lZYtWzJi5EgGDhwMwKZNG5lZzHzrsvrii88ZOGgQbdu247y+5zP11df54ouZbNu6lZycHFq2bMV5ffuyatWPzPz8M4KDrF9JdnsonTp3Zk3ujYjDEeNLpna7HcMwqFcvyjflL68JPDg4mNv/fgezvvgCu93OOeecgwnFrrgH4PGs5tNPPuaysZfTvn0HXnv9LT779BP+2vgX3pwc2rZrx5gxl/rm0iclzvFNXxQ5lSihS6XYsGE9d/z9NsY/MIGePc8CICqqPr161adXr97FHnfo0CE2rK9Y8+WhQ4d4/PFHmTTpUd/633lNxvnlXwWuohbMn8eoUWN8q4DFxg7w7Zs3N6lQ+bzaOcDsWV+U+TpZWZl89eVsrvzb1URERDBo8EWFavfnntvHNz0sP9M0+fijD1i2rOin04WFhXHTzbcUuW/Hju089WQC2RV8VG1OTg5PP/UkDz70fzRr1pymTZtx++13FCr388/WCPwVK1cQlzvOYPLkp1m5cgW1atWiR4+evu6UAQMG0b17D+bNm8uMj61BmHOTkhg2bDghISEMHjyEwYOH+M49e3bpn/c777xNvagoBg8eQt26dbnhxpuKLPftt0t57bWp5fsQRKqJmtyl0hw+fJgJrvHcddc/c5+KVvixqDk5Ob61yx955GGuvuoKFi9eWOFrr/79N+66604WL15YIAmZpklycjKzZ33BjTdcy+rVv1f4WgA7duxg/Pj7Wb/+zxO2b2fFyhUFtjVo0IDzz78AsPqyfz9hbfjSzJ49y7cG+KhRowu1bGzbtq3AKPS8aWf33Xc3b5dQM83KymLDhvUFPq99+/Yx8/PPuOPvt7F58+ZyxVmcTZs2cvtttzDj44/Yu3dPgT75nJwcPJ7VbMj9HFeu+I5p0970TYc877y+BNls3HP3v5g3z7pRCgsL4/Chw3y/8vhUvs2bNzHBNb7Qk/u2bt3ia/YvSXZ2Ns9OeYb/THiAdevWFmgFSU9PZ43Hw4P/cfH4Y48Umloncqow/LVcp1Sv+LhBzwP/qu7r2u126tevT63atTl08CAHDx6s8iVibTYbUVH1CQsLZe/evb5VyKpKZGRdGjZsyMGDBzl0qOrfH8CZZ3bzPZzl2SnPMH/+XKKioqhVqzY7d+4oMYbHn5jMWWedTXJyMlf97XKCg4Np1qw5Bw4cIDX1SJXHHhoaStOmzcjIzOBAcnKRDywJCQkhOroR+/YV/P5FR0djmiWPMq9Xrx716zfg4MEDJz1C3zAMmjZtRnZ2Nvv27fXbssblcH1i0oLp/g5C/EtN7lKlsrKy2L17d+kFK5HX6y1yta+qkpJyuMjWiOp2MPeGqbyys7OLXCmvqmRmZpY66v7YsWPs3Fl4dHtZxh4cOnSowgscmaZZ5PVFTmVqchcREQkASugiIiIBQAldREQkACihi4iIBAANihOpgQ4dPsQS92LAekpYefz+22+kHjniWzJXRAKDErpIDbRt61YSEh4/qWM/+uiDSo5GRE4FanIXEREJAEroIiIiAUBN7qeJhg0bhBm6fxMJSF7TG+rvGMT/lNBPEwMHDGrfrHkLf4chIlVg48YN7fwdg/ifEvpp4uMZH3uAQf6OQ0SqxNrbbr/T3zGIn6kNVkREJAAooYuIiAQAJXQREZEAoIQuIiISAJTQRUREAoASuoiISABQQhcREQkASugiIiIBQAldREQkAGilOJFK8Px//0dIiL3QdtP0kpqayuFDhzh46CA7d+5kxXfL2bt3rx+iFJFApoQuUgnatm2H3V44oRfl9tvv4I8/1vHRhx+wYsV3lRZDu3bt6Ny5K273ItLS0irtvCJSMyihi1SijIwMPJ7VvteGYRAeHk6tWrWIiqpPZGQkAJ06dWbiw4+QlDiHqVNfJjMzs0LXjYiI4NnnXiA0NJQzOp3B8889W6HziUjNo4QuUon279/Hg/9xFbnPMAy6dnUw7OLhxMYOACAufih169bl0UcnYZrmSV/X6/X6js/Ozjnp84hIzaWELlJNTNPE41mNx7Oab5cu4Z5776d27dqc1/d8xo69nI8//vCkz52Wlsbdd/2Tjh078u23SysxahGpKTTKXcQPli9fxv9e+K/v9VVXX0NUVFSFzrl58ybmz59Henp6RcMTkRpICV3ET9zuRSxa+A0AwcHBxMUNLbDfZrNht9ux2+0YhuHbXr9+fTp27IjNVvC/b17ZoKCgEo8/UXBwsK9cUQzDoGnTZnTv0aPUm46QkBDsdjvBwccb//K6GiIiIko8VkQqRk3uIn708ccfETtgIACDBl/Ehx++79sXP3QY//jHPwH4++23smPHDu6+51769buA4OBgkpP3M+WZp/n5558IDg5m1uyvAZg1ayZTX3mZM87oxHPPvwDA1199yYsvvlDo+nZ7KO+9/yERERFs/Osv7rjjNt8+m83G3/52NZeMGk2tWrV82/fu3cOL/3uBH374vtD5ZnzyOWFhYSxc+A1PPzWZCy64kJtuvoVGjRpjmiZzvv6K1157laysig0CFJHCVEMX8aNt27aSlZUFQNOmTQvUbPMzDLj33vvo3z/WV6ZBg4bcdfc9vhr5idatW8vatWsA62ahTp06hcrExg7w1ZxnzZrp2x4WFsbTTz/LlX+7ypfMs7OzAWjUqDGTHnmMyy4bV+J76+pw8O/xLho1apz7HgyGXTycvn37lniciJwcJXQRP/J6vWzZsgWwEl6jRo2KLDdu3BV07tKVp5+azP3338Ps2bMwTZNXp75CTk7xo9pnfv4ZAKGhocTHDyu0f8TISwA4fPgwixYtLHC9rg6H7xx/u3IcI4YP5Zabb+CnVaswDINrrr2Oxo0bF3ndhg0b8uCDE5nz9Vfcd+/dPPfcFHbv2sUajwe3e3HpH4yIlJua3EX8LChfX3hoaFiRZc7u1Ztbb7mJ5OT9AKz+/Xfmzk1k419/lXjuZcu+Ze/ePTRq1JjhI0by+eef+m4AYmLOpF27dgB8/fWXHDt2DICGDaMZPeZSAObNTeK116b6zrdt2zYeeWQir73+Jo0aNebKv13Nc88+U+i63bp157333uH9994F8I3sj4yMrND0PBEpnmroIn5ks9lo0bKl7/WBA8lFlpv1xUxfMs9TWjIHqwVg1hdfABAdHc355/fz7curnWdnZ/P1V1/6tsfExPgGyM2c+Vmhc2ZmZrJixQoAOnfuXOR1U1JS+GTGjALbjh49yu7du0uNWUROjmroIn7UtGkzX/Lcv38fhw8fLrLcmjWek75GUtIcrrr6asLDa3HJqNEsWeKmQYOG9O17PgBLl7g5cOCAr3yr1q19X//nwf8r8pwREdaKd02aNMEwjEK17o0b/9LAN5FqpoQu4keXjR3r+3rlypXFljt48ECx+0pz9OhR5iYlccmo0XTp0pVOnTrTp895vsF0X3wxs0D5RtFWP75pmuzZs6fIc+bfHh4eztGjRwvsz3+DICLVQwldxE/OOvtshgyJByAnJ4dZX3xebNmKdjvPmjWTESMvwWazMXbc5TgcMQCsXbuGP//8o0DZwylWK4FhGEx55ukK3UyISPVRH7qIH7Rr14577rnP9/rL2bPYtm1blV1v9+7dLF++DIC+fc+nbt26QOHaOcDmTZt8X5/bp0+VxSQilUsJXaQaRUdHc/kVV/Lc8y/QoEFDwBqx/uabr1f5tfOmsOXZv38fy4pY9/3bb5f6lo+96aZbaNmqVZHna9CgIVdddU3lByoiJ0VN7iKVqF69KG697e++1zbDICIyknr16hEVVZ/WrVsXWIb1xx++Z/LkJ3yLtlSlNWs8/PHHOjp1skamf/Xll0XOYU9PT+edt6dx621/p3bt2rz00lS+/HIWa9eu5ejRNFo0b0Hbtu0YMHAgBw4c5L333qny2EWkdEroIpWoTp06XHLJqFLLHThwgE8++ZhZX8ys1nnZn3/+GS7Xf8jKyiQx8etiy82a9QVt2rZlyJB4QkJCGD360iLLHT58qKpCFZFyUkIXqQTHsrKKfACK1+slKyuLrKxMMjIyWb/+T777bjkrvlvuW/K1Oi37din79u1j1aofSUlJKbacaZo8/9yzrF2zllGjR9O6dRvfvqysLLZs2cKsWTNZnG91ORHxL0OrNp0e4uMGPQ/8y99xiP81bdqMtLTUEhP6icLCwmjQoCFHjx7l0KGDWu3t1HN9YtKC6f4OQvxLNXSR08yuXTvLfUxGRgY7dmyvgmhEpLJolLuIiEgAUEIXEREJAEroIiIiAUAJXUREJAAooZ8+qn7lEhHxF/3/FiX008j3/g5ARKqM/n+LEvppZCHg9XcQIlLptiYmLfjT30GI/2ke+mkiMWnB/vi4QRcAU4Aof8cjIpViI3Cnv4OQU4NWihMREQkAanIXEREJAEroIiIiAUAJXUREJAAooYuIiAQAJXQREZEAoIQuIiISAJTQRUREAoASuoiISABQQhcREQkASugiIiIBQGu5yykrZvKiMabXOBPY4JnQ/72SyjomL+lper3jDMNm5gQFPbHu3+cfKa5sr9dWhaQnp042DDMox7C9uXb8hb9XevABbOhFF51vBpmD814bpuk1DXYYhm3D3r0Hlv/444/H/BlffrGxscFhYcEPAmRn89z8+fMP+zsmkaqihC6nLm9QKIY5ETja/skFX/41flDxv4xNc4JhGJeCiS0neyvwSnFFM5KPjATjHtM0Uk1b0ENlCcUAo+sT7jiCvFs942M95X4vgcSW0w/TmJj30sz9yzS9RDest2nokEH/njN3waf+C7CAYExzIoDdbk4DlNAlYKnJXU5ZmRFpn2GyH6gVbgZfXVy5M5/4pjEwMu+1AbeWdF4vxs0AJnxYUk0+v5jJSwZjMAevbXmvSatqle0dBLw0Ex4xMV8BZplwCGhrGnwcHz+4v59jEzntKKHLKWv9nfGZGMZ0ANM0ik3SphF0PRACpORu6u5IWHRuUWW7TF7cxoDB1nHeV8sai4l3Iyb7Mflt1cSz00/cb0w6/f4vGZCalLRgYlLSN39PTFpwiWHk9DRgPWDDNJ/1d3wip5vT7peQ1CxmDq9hterGnPn4kr4n7jfAMH01bvNp4Gdrh+22os4XZNputA7jp7UPxK4qaxyrH+i/IbxhnWaeCc4LzNxW5jwxTyzu0dW++J6ynitQJSYu2myaxlu5L88cOnRoqF8DEjnNKKHLKW3NgxeuB2MhgBlkFqqlx0xeMhhoB2RjBr1pGMZUAMNkXM9Ji+vlL2t88kmQiXkDgGEYJdbOO/4vsVAy+vGWswsN9ur6xNKzTMP4BmyNy/J+uj8zr3ZZynV+allETaz1G5CW+2WwzXak1K6JESNGlFrGMAwjNja2TnniKGv5Xr16hZQlBpGawDBNs/RSIn7kmOy+DJMZBqTbjKDmvz3QNeOk4AAAIABJREFU76Bv3xNLPsUwxxgmM1dPcI6OmbS4jmk3dgIRmPzTM8H5v7yyMY+7h5s2ZgOpRpbZdPXE/qkAjgT3W8AA0zAfCwnO+jA7O/RFw2ScCfuBiR6Xc9qZTyzt5jW8s4Fkj8t5NkDMZHdv02QeUA+ruf8ggAHe1S5nO991rZieAIZh3XwkGyZLsoOD/7Hu3+fvzP9eYxLc95gwHmgEZAG/mhivrnFd+Gblf7InZ2jcwPEmxmQD9sxJWtAkb/vYsX3DjxyutRCDPgZsnZO0oHVRx8fFDXAY2J4BzgHqY7ARr/lBRN0GD8+YMSMnr9ywIQPOzTFsTxnQA4gEdmGar2ZkeZ9ctGhRxonnHTZsYGuv13gGk/OBpkAyprkaw3AC2ILMNl9//c0WK4aB5xgYU4A+WIODt5kYH9hsIVPmzJmzr9I+LJFqVONqAHL6Ca9f5wtgjwnh2V7vNXnbY55e3ATDzB0MZ/WHr57YPxXTeB8Ao+DgODOIm60v+CAvmQMYhtEIaG2Y1Ms+Fjodk+tMCAdaAlN6Tlpcz7R5Q4HWmLQCOPPxxb0wmY+VzMFKOK2B1qb1L2AN2DPtxs/AnVjJfAsQZRqMCs7J/uXMxxa2972fyUtuMWEKVjLfijXIrLeB+XqFPsAq4oXQuLhBcUPjBl8TP2TgxNSU2ksx6AOAaUwu6pihQwYON0zbD0AcUBfYhkk7DOPBIykHvjYMwwCIjx90ntewLTXgQqzPNgdoimE8HBoa9NKJ542Pv2igN8f4HZNLgcYmrAUy85J5fsOGxTYxsCUB/YBM4E+guYE5npysQuVFagoldDnl/XjL2ccweQvAMMxb8rab2cYNQLABmzwTYuflbTeCcqbmfumIeXJxP4BOjy9sbpgMBTCxFdPcbtyKaYTkBAU3t5nZTUzMlwzTeOjnif0PHS+CAZCazeqQLLONifm2dU7zJXuWGWXPMqMybMfq5xX3GsEJQAcDvjNMs6fH5WwTHGS2Bj4wIdobFJTgez+mOcq6BO96XM7WHpezsdfw9gJmnfynV3UMqGdAoon5NobxsIl5NibpBuYDc+bOLzRtcOTIfhGmYUzFINzEeP5YNs0Tkxa0MmzGebmD6YbExQ243CptNjEhzcS8wRaU0/RYNo0NeCr3uteMio2tl/+8mN5pQASY3+R4bS2TkhZ0TUxa0ByD7ifG4fUG9QczCoyDhs3eLDFpQSeT4GhM8zGvQeqJ5UVqCs1Dlxohx2u8HhRkjge6OhLcF6zJci5z2LnJBEyD1/MPVFs9PvZXx2T3Ckz6mF5uA74NstmuNyHIhB/XTLjgp2IuE3b0mPfyTRMuzGvO/UcRZQyATRP7ZwAZXRPcWdZGI/Pnic5D+Qt2f2Z5I+A6AK/NeGDNeOcvAL/+u//2ro8vnGDYgi4HLuuYsDR6veuCfQbGjyZmnAm9Y55c1mr1+PO35g7cG3WSH1tVywb+ANoDYQDYjKXpGTn/LapwZmbYNQY0w2RHZN2o8TNmzMgCmDNn/or4+EFTMZmCafwd+NA02eL12s6ZN2/e+rzjR8XGJmSEBt0NhGTVCmqE1YKRd96WBuw5lmMbM3/+PN9c84yMnD/DQoMKxOH1Bv1iM3IAs55pZvQHZiclJR0AyrQmgcipSgldaoR1D164yZHgngfEgXmrI2RRLRNbW+CYzZv91onlDdOYamL2AePSjglL77Zj3Ahgg9dKuMznuYm6JEZZY87Jzo7JLZ9m85rDYia7LzZNwwDTRlCQgclBoEGoLacTsC/H8L5pM42bgM6mN3t1TIL7YU+W83lzIt6yXrM6GZA8J2lBzNixY4NSUpKvNDCmYpoXhYUGJfbq1euiwivGmQ4wwMaulJSDj8TFDT5+LpOGGGBAR4CkpG8K3HSNHds3PNNeaxBwDAgBwzdo0TDoZt3OGTPLshLc3Llz18XFDUo0IB7TNis+bvC7hi3kXvWdS02nJnepMUzM3KZy41LTsI3P3Tzr9wkD95xY9nBYyAysQWqhdrzvAG2AI2SZHxZ7fpPtlRmvF287AAOyvXCOadILzLPA6G6YnGnCKjDmYtrsAGsf6L85C1s3YA4QYcKUrnb31yeO1j/VzJgxIycp6Zt3TRiD1dfdv2HDqIknljNMmzW2wCTKwDw3/x8M2gOLTVgbGxvrq2jEx8e2iY8b/M6RlFp7TYPHyf2d5fWax2+svEYLANMwt5Y15sjI+sNN+D8gG8yrTW/WT/Hxg847qQ9A5BShGrrUGI2z+GqvnZ1AMyAWwDTMIvvDt919XnrM5MXvmKbxL6wBWGAa76+e6Cy2j9TAKEtNuMw1dJtp22taVcfUNS5nbFmOsZreubhrgvtOIAGIy7Iby4xJnHmq1tTzJCUtSIqPH/RvTKYYmA/ExQ2cnZT0zffHS5gHrH/4OnHugn+Vdr64uEH3GmbQoxjmnybGqKSk+Qvi4wbtIa95//h5N1v/GvVPPEdxckfTPzp06OD5ppd3weyAiXvoRRfFzpk3b1lZzyNyKlENXWqMRRP7ZwNv5Nu0Ye0D/b8prrzNZGrBDSU2t5eJcUJCN+CI9a9Zt1BZ89hKINuE5o4n3PHFnS9m0ho7HF9tzgTT43K+YBhmdyAV6OoIXXxRRWOvDn36XPA88AMQZMDbsbGxvuRrGuZKAAxGDR06NLKo48eOHWsHGDJkSEsDnsJgf0ZmTq+kpPkLirumgbEawDC9cZMmTSr1d1r+MnPmzF8RYg/vDuY3QIhpK7zWgUhNoYQuNYrNa7xhWM26mBQcDHei31z91xkY7tyXP3geuPDnil7fPLGGbrDf2m4Mjpm0uA5YT37r+uSSC3+fMHAPBu/klnvX8cSSscYnnwSBtXBMzOPu4V0T3D95Q5JjALrY3bNinlhyZV5iD8uM2EnecrZeo0tFY68OEydO9GJwB9ZH1TnMHvRI3r7sbONDYBfQ0vRmfTF06EDflL3hwwc2Hzpk4H1HUg4sBjCM7GGADcPcumjRomyAsWPHBgEFR7gBdeqmTQc2mRgx3323ZGppi8qsXL7knvj4wU9ffPEFUQCzZ88+CsY6rKDPqNgnIOI/SuhSo/z+nwu3eSERyDqGbVpp5b2mdyqASckrw50s02ubC3iBVqbd2OVIcG/GNH8yvNb8eCMz+nZgIdAAw/y464ZGqY4E946gnOyU3EVuetjIyWtKb2Ua5vsOu/tATMKSxekhqVuwuheOZnu9c6oi/qqQmLjgBwzzeQAM7hk2ZMC5AAsWLEjGIA7riWexptfYEB83aE9c3KCD2ceM7aZhPA00ADAMbxLgxTTOj48b9OLQuIHjU1MObMzbb5r8Kz5u0IsAM2YsTzdstuuBAwbGzWGhQSnxcYP2xccN+iMsNOjXIkIMxTTvy8kO3Rs/ZNB38XGDfgLuALCZ3lPlKXEi5aaELjWP6Z1qYM5c77qg1FHJtmONPgc2hIRkfFRJVy9QQ18z4YKfTMO4EtgD1MFaVGa7DWMZwOqJXbOyssJGGSZvGJCO1f/bLPfrBV68/VdP6P8LgGHz/h8Y35gQYWI6MWgIrDMMY/i6B2P/qKT4q0VERIMHAA8Q5DVs7+c1sScmLvjNZnqHAEtzizYyrMV59mPysi3IvMgqt2izYZrjMdkB3GFi3GUaPAnGJwAGjMNgY9715syZ5zYJjsHkTUxWYy1GcwZF1LhNm/mpgTENk2O5C+H0BFJNeCRx3sIpVfahiFQxLf0qNY4BRof/JdrX3xmfWZbysZMWB+f2v1dpTJ0nL25t2kKy/vj3+buK6gowJmHrFL6sSajNyP71vr57iztXx/8lhoamhbcMCranlFSupouNjQ0LC6OJ12vfN3fu3LSiyowdOzbowIEDDRcsWOCbyTB48OBWUVFp+2bMWF7oqXflvH5wcHBws1AIrhUVtSX/srMiNZESukgxHAnutsC4fJu2elzOD/wVz+koPm7QCKBrvk1fJyYt+N1f8YicyjRtTaR4nbCmjuVxA0ro1etKCt5U7QaU0EWKoD50ERGRAKCELiIiEgCU0EVERAKAErqIiEgAUEIXEREJAEroIiIiAUAJXUREJAAooYuIiAQAJXQREZEAoIQuIiISAJTQRUREAoASuoiISABQQhcREQkASugiIiIBQAldREQkACihi4iIBAAldBERkQCghC4iIhIAlNBFREQCgBK6iIhIAFBCFxERCQBK6CIiIgFACV1ERCQAKKGLiIgEACV0ERGRAKCELiIiEgCU0EVERAKAErqIiEgAUEIXEREJAEroIiIiAUAJXUREJAAooYuIiAQAJXQREZEAoIQuIiISAJTQRUREAoASuoiISABQQhcREQkASugiIiIBQAldREQkACihi4iIBAAldBERkQCghC4iIhIAlNBFREQCgBK6iIhIAFBCFxERCQBK6CIiIgFACV1ERCQAKKGLiIgEACV0ERGRAKCELiIiEgCU0EVERAKAErqIiEgAUEIXEREJAIZpmv6OQcTvHAnuLkD3EzZ3Bx7I93ot8MgJZbI8LufnVRnb6SI+btBQIPKEzf8Ezsv3eirgPqHMH4lJC36uythEaoJgfwcgcoqoC3xYSpkuRZSZCSihV44RwK2llLkt909+IwEldDntqcldBPC4nCuAP0/i0LcqO5bT2DsnccweYE5lByJSEymhixxX3oSyG0iqikBOR4lJC5YDG8p52HuJSQuyqyIekZpGCV3kuHcAbznKv+9xOZVMKtf0Ki4vErCU0EVyeVzObcA35ThkehWFcjorz03VqsSkBaurMhiRmkQJXaSg6WUst8rjciqZVLLEpAXluamaXoWhiNQ4SugiBc0EDpeh3PQqjuN0Nq0MZbKAD6o6EJGaRAldJB+Py5kOfFRKsSxKn+ImJ68sN1VfJiYtOFAdwYjUFEroIoVNL2X/lx6XM7k6AjkdJSYtyKD0m6rp1RCKSI2ihC5ygtw56etKKDK9mkI5nZXU7L4HTRcUKUQJXaRo04vZrmRSDRKTFqzEWmq3KJp7LlIEJXSRor0D5BSx/T3NPa8208u5XeS0poQuUgSPy7kLmFvErunVHMrp7F0K31Rp7rlIMZTQRYo3/YTXmntejRKTFhR1UzXdD6GI1AhK6CLFmw0czPd6up/iOJ1Nz/e1pguKlEAJXaQYHpczk+PTp5RM/GM2cCj36y8TkxZouqBIMZTQRUr2du6/szX3vPolJi3If1M13Y+hiJzylNBFSuBxOVcCf6Bk4k/voEfVipTKME3T3zGIiIhIBamGLiIiEgCC/R2ASHk5EtyRQFsg3N+xSEDKBrZ6XM69/g5EpDzU5C6nPEeCOxy4BxgBtAMa+jciOU2kAn8BS4EEj8u508/xiJRINXSpCe4EHvN3EHLaqQN0z/3THBjt33BESqY+dKkJ6vs7ADnt6WdQTnlK6CIiIgFACV1ERCQAKKGLiIgEACV0ERGRAKCELiIiEgCU0EVERAKAErqIiEgAUEIXEREJAEroIiIiAUAJXUREJAAooYuIiAQAJXQREZEAoKetiZSTzYD6texF7kvLyiH9WE41RyQiooQuUm7RdUJZ+I8+xe7fm5rFhn1pvP7dVr7fcqgaIxOR05ma3EUqWaM6dvq2jWLald2ZPLwzRgXOdbGjEc+O6oqjaUSlxScigUk1dJEK2HwgnY9/2mm9MKBhbTtdGtehb9soAIbHNGb1riO89+OOcp87MiyYx4Z1JiTIoEFtO9e+90tlhi4iAUYJXaQCdqVk8M4P2wttH3hGQ/47xoEB3N2/HR/9tJNsr1muc6dkZLNhfxpdGtfhx61quheRkimhi1SBb/7czw9bDnFO63qEhdho37A2f+xNLfd5xk37iaZ1Q9l+KKMKohSRQKI+dJEqsvlAuu/r9g1rndQ5ckxTyVxEykQ1dJEq0qZ+uO/r5LQswOpj79y4DgC/7UwhJSMbmwEXdmhA+wa1WLbpIOv2HK/J920bhc0w2Hskkz/3pfm2d2sWSWRYMKmZ2fyyI4WQIIOeLepyVou6bD5wlBWbD3Eo/ZivvM2AM5tF0rdtFEezclix+VCxLQahwTa6Nomgc+PaRNcJZdvBdFZsPsiulMwiy3duXIeGte0cy/GyMndUf0RYMMMdjcnMzmHxhgOkZBzj3NbWuIL0Yzms2na4yHM1iQylQ8PaAGw5mM62g+lFlhORwpTQRarAhe3r07t1PcBKYGtyk/Q5revx9MguAFz3/q9sTD7KO1f18CX/u2Ph3e+3M2XRRrK9Jv8bE0NYiI3Zq/fg+nKd7/z3D2zHWS3q4tl9hAdmr+PZUV3pGF3btz/Ha3LX52tYuH4/TSNDeXnsmZyRb7/XhDe+28p/3ZsKxO1oGsEzI7vQKiq8wPbMbC8vf7uFN77bWui93tK3FUM6R3M4PZu+zy8jtmMDnhnZlbAQqwEwJSObh+b8wfXntKRHi0hMYMRrP7Ax+Wihc/3fkI44OzQA4LJpq8r2YYsIoIQuUiHRdexc0q2J73X9WiHENI3gos7RvulqH6zayZGM7ELHhgQZvDDGQZv64WRmewkNtmEA57WNwlxUtuu3rBfOjOvPIjPby4I/9xMaZOPcNvWwB9mYMqoLUxZu5Oa+rahfy45n1xGOHsuhe/NI7EE2bunbCs/uIyz4Yz8A4SFBfHBNT4JtVuTHckxMTOxBNkKDbdzdvy27UzL4yrO32Hg6RtfmqRFdCAkyyDFNggyDyLBgHE0ieGXZFl4ddyYGcNN5rZjw1boCx7ZvWIsLc5P58k0HWbO7/GMORE5nSugiFdChYW0eH9ap2P2L1icXqgXnuX9Ae1Kzshnyykp2pWRyftso/i/uDB5JWk9OGUfER4YFM/+PfTwwex0Z2V4AerSI5L2re2IPsuEa3IGNyUe56t1ffM3XjiYRvHt1D0KDbdzRr40vodsMCLYZ/Lz9MC9/u4Wfth/GZhgM6RzNY7nv8fKzmhWb0O3BBi9eGsO7P+7grRVbMQyDy3s2Y1S3Jry6bAsZ2V5W7zpCTNMILnY04sWlm9l5+Pj4gBvObem7CSqqJUBESqZBcSKVLDUzh283HuD+WWv5x6eri03O9WuHcPNHv7H9UAY5XpMlfx1g2Kvf89P2ovuXi7Ix+Sh3f77Gl8wBftmewq87Unyvr3//1wJ90Z7dR5izxkrK7aNrEWQcX/rmo592ct37v7J800Eyjnk5mpXDzN92sz63/75pZFixsYSHBPHj1kO84N5EamYORzKyef27rYx680dffC9/uwWAIJvBDX1a+o5tVMfOMEdjAFbvOuLrixeRslMNXaQCftmewoNz/gCsvvIjGdmkZZVtLfcPV+0k45i3wLbMbG8xpYuWfiyHom4XthxIp0fzSACOFrG2fF6CDjIMGtaxs+dIJmlZOTw6d32R1/l1Zwodo2sTHhJUYjxvrthWaFv+9+TekMzaPal0aVyH0d2a8Mq3W0hOy+Lq3i0ICbJuLF5X7VzkpKiGLlIB6dk5bEo+yqbko+xOySxzMgf4c29a6YVO0uF8I9yLkpp5vE8/Mqzo+/rGEaFcc04LPry2J5d2bwpAcFDxC9lme022HCh9VPrU3Fp6aLCNa89pQZ3QIMb2bAbApuSjLPxzf6nnEJHCVEMX8ZMjmYUHylWWHLN8q9Ll16Fhbe50tmHgGQ3JyvbyzZ/7ycz20rtVvRKPS8vMKdN1v/lzP3/uS+OM6NpcflYzvKZJnVCr5j9t5TbKuaCeiORSDV1EfJwdGvDxdWcx8IyGzP59D3GvrOT+WWvZsL/wFLOTZQKvLrNq6bXtQdx8XisA9hzJZPbqPZV2HZHTjRK6iABWcn3i4k6Ehdj49JddTPhqHXtTs6rkWvPW7Ss0D/2dH7ZzLEfVc5GTpYQuIoC14lu98BAAfipmJbfK4jWP19LBWnxmxs+7qvSaIoFOCV1EAAosfjO6exNfcu/RIhJn+/oA2INsRNexM6BjwwpfL8h2fIDdB6t2cLQcAwpFpDANihMRADbsT+On7Yc5q0Vdereqx+I7z+NQ+jEa1LazL9Vaxz0kyGDBHX3YcSiDhetPfjS6AdzYx+o7z8j28v5JPC9eRApSQhcpp2M5Xn7IfT75H3vKN/UsOS3Ld2xKEcvBnmjVtkPYg21sPGFQ2trdqeR4zQJPdMtv28EM33W8RQwb35d6PI703HnqXhPu/NTD3f3b0qdNFBnZOazZncq0Fds4eiyHJ4d3oVX9cH7ZcZiXlx5vLv9r/1F+2HqI1Myy17D7d2zgewLd57/u4sDRkqfZiUjpDLMC01tEqoMjwT0ZGO/vOKTyvH9NT3o0jyTHaxI/9Xt2HD7lHxHr9ric/f0dhEhJ1IcuItXq7JZ1favYJa7dVxOSuUiNoIQuItXqptx55ybwppZ5Fak0SugiUm3OiK7Nhbkj5pdsSObPfVW3/K3I6UYJXUSqzY25tXOAN74r/CAXETl5SugiUi2a1Q0jvks0AD9vP1yux8SKSOk0bU1EqkUdexCPz9sAWAldRCqXErqIVIs/96Wpz1ykCqnJXUREJAAooYuIiAQAJXQREZEAoIQuIiISAJTQRUREAoASuoiISABQQpeaINnfAchpTz+DcsrTPHSpCV4E7MAIoB3Q0L/hyGkiFfgLWAok+DkWkVLpeehS4zgS3JFAWyDc37FIQMoGtnpczr3+DkSkPJTQRUREAoD60EXktOdIcIc4Etwd/R2HSEUooYuIwCvAj44Ed5y/AxE5WUroInJacyS47wVuBCKBrxwJ7jv8HJLISVFCF5HTliPBPRx4CsgAxgB/Ai86EtzX+jUwkZOgQXESEBwJbgMYC1wBHACe8bica/wblZzKHAnubsAyoA5whcfl/MiR4G6au6050Nzjcu73Z4wi5aEaugSKB4CPgGHA9cByR4J7kH9DklOVI8HdGPgSK5k/7HE5PwLwuJy7gGlY6x6M9l+EIuWnhC41miPBHeZIcDcEHsz90wC4BusX8leOBPd5/oxPTj2OBHcY8AXQCmvO+bcnFGme+29IdcYlUlFqcpcaK3eBmXlAFJDjcTm75tvnBOZjNb+f43E5t/onSjnVOBLc7wNXAh6spF4HeA14F+gHPAIYQFePy7nBX3GKlJdq6FKTHQG2AWcAh/Lv8LicbuB2oDHwpSPBXaf6w5NTjSPB/RBWMt8ODMYacwFwK1ZNfTKQA9yhZC41jRK61Fgel9MErgVWAec5Etz3nLD/TWAK0A14vfojlOrmSHAX+3wKR4L7MmASkAYM97icuzwu59fAWqyWnLuA/wA9PC6nfl6kxlGTu9QojgR3FNAeyPC4nKtztzUHvgeaACNyf0nnlbdhNae+4nE5V+XbHgP8G7jR43Ieq8a3IFXEkeCuBSwCPvK4nM+dsK8NsAYIBUZ5XM7Z+fbNAy4EanlcTm+1BSxSyZTQpUbIbTKfBNzJ8cFK24BrPC7nYkeCuxewBGuQU9+8ZF/MuYZijYiPAF73uJy3VGnwUuVypy1+gjWXHKwWmTvy36w5Etx3ATaPy/nsCccuAAYAdo/LmV1NIYtUOiV0OeU5EtwhwFwgFvgUK3F3BG4GgoCLcpP6ZcDHwBasgXD7ijjXXVjN8Pm7m+7yuJz/rdp3IVXJkeB+HJhwwuZFwKUel/NAKcduAOp6XM7oE7YbwHlYMyc2eFzOtZUYskilUx+6nBIcCe5wR4L77GJ2P4CVzG/wuJyXeVzO/3lczn8C/bFGIz/nSHAbHpfzE+BhoA1wyQnnD3YkuF8FnqPwz/0UR4J7SKW9GalWjgT31RRO5mD9zKxwJLjPKOHYMKxH8e45YftZwEasRWZmAx5HgnuaI8Ftr7TARSqZErqcKh7GejjGBUXsuwz4xeNyTsu/0eNyrgQ+A3pg1aLwuJyPALH5BzXl9rvPBYprWg8CPnYkuDtX9E1I9cpNvCUNYOuIldQHFrO/Odbvwe35zukA3FgzJJ4BBgJTgeuA5ysetUjVUEKXU8VM4C3g5yL2tSjhuF25/9bN2+BxORfnfZ1bO1uJ1UdakgPo/0NNtBr4sJQyUUCSI8F9axH7Guf+uznftsew5qYfAY54XM6FHpfz78DnwI25tXqRU4760OWUkvvL8gngibx1tB0J7t+AM4HOHpfzj3xlQ4FfgHCPy9mmiHMNwOpzjyrlssuwRj4X6nOXmsGR4B6P9XNT2k3Zf4F7PS5nTr5jXUCIx+V8xJHg7gCsx/q5GoG1POwa4AbgfqxFZ9p6XM7Nlf4mRCpINRI51VwK3A3MzNdfmTcFaaojwR0N4EhwN8Ia1dwZePLEk+TWxuZSejJ/BxigZF6zeVzOJ7FGuKeVUvRfWAsNReY7NgHIG/metwDRfI/LuQ1r5bjaWAPsrsZawGgLgCPBfW4JTfki1U4JXfwmdxRx3tdtHAnuNh6X8z2seeP9ON43+jZW4u0P7MwdlbwNGA4863E5X8l3niBHgvt5rD7PYhcZAUzA5XE5r/W4nFmV+LbETzwu5xdYPzfbSykaj/Xwnrb5jk3N/fIg1s/GJY4Ed0ju9lHAUqz++Cc8LqfpSHC3AmZhNeXfVslvReSkqMld/MaR4I7DmlOegtU0vtHjcp6bu9rXXKx+b5fH5ZycW/5yrAFyLYFNwEsel3NJvvNFYs0vjy/l0mnA1R6Xc2YlvyU5BTgS3E2wku05pRTdh9XVsuyE46cA92C1/Pwnr3nekeAeCXwFhGN103QDtmKtB/+wx+WcVJnvQ6S8lNDFbxwJ7hux+jTtwE5gpMfl/DV3XxSwAqtWNKa05Ju7EthXgKOUy27HWk2uqMF3EiAcCe5wrMegjiulaBZws8flfCffsXash/44gd+BD4DPPC7n+tyVB2cBFwMvYq02+DkQB9xS1JKxjgR3BPAo8JDH5TxS0fcmUhw1uYs/NcXqnwzGWlv717wdHpfzIFaT+iHgPUeCu2dxJ3EkuM/HWvq1tGT+A9aCM0rmAc7jcqZjPXjkvif2AAAgAElEQVSltFqzHXjbkeBOyOsCyu2CGYDV354D3Ig1CwLgKaxkPhdrQaJ0rFaj34DHTlxLPvcG4IPcc91RCW9NpFhK6OJPTbGmqRnA6ydOB/K4nH9iDZKzYw1kanDiCXIXFfkGiD5x3wlmAE6Py7mrlHISIDwup+lxOR/GSuwZpRR/APjMkeCunXus1+NyvuBxOXsCnTwuZ7IjwX0TcC/Ww1zG5TXF5/azfwI0AvqccN68G4Ak4OnKeWciRVNCF396x+NynoU1CO5crHnoPo4E9whgOVbN5jWPy5mcb5/hSHA/gTVYLrSU6zwCXJ5bm5LTjMfl/AhrQOXuUoqOApY6EtwF1j3wuJxeR4K7P/AykAlc7HE5D59wbN7Npu/GIbdL6V6s566Py9cXbyBSBdSHLtXGkeAeBowF0oFn8p43nbtWexJWM+djHpfzIUeCuyXW/N9nPa7/b+++w6Oq0geOfyeNEEihh5CEGtqld0S8iiiKYFcEwQYuupZVd3X3qtjXUddV159dsLEWXFEBRVQUrop0pN1AgAChhBaSQAqQNr8/zs0wSSYZIANJhvfzPPsAt55xZ+57T3uP/ni560QA04GrfdzyKCpdrK/EI+IsYH+n5gA9fRy6BzWeY7l9XhJqPEdje/9tnlkLNafZHtXkng0kWYaerznN84D59rYBpfPWNaf5pX3/rpahH/PXZxMCJKCLM0Rzms+jBhCV2g8M8QjqjYDfgK6ozG5tUE3tPSxD90zL2QqVW7uPj1vuQz2Ul/rrM4i6z16172NU0piqHAFuRgXlJUBH4E7gItQsihdQ6WG7AVNQXT7jLEP/VHOa7VBjOhqichz87nH/l1Gpii+UpVqFv0lAF6ed5jRHoWpGPwB/A0YC/0RNPRtYuhqWPd1oLqoG8xOqtu45La0faoRxnI9brkENstvp548iAoA9UO05VOa3qrhQ39F2wCuWod9vj1ifimppKnUENVL+Y81pRgOLgS6oqZH/te95EbDWMvQyi8AI4U8S0MVppznNt1D9k50sQ8+202suRTVhLkAtf1pkH+sAosr3UdpLo36ImgNcldnAjR6JQoTwSnOat6ISEPlaQS0d6GgZujsLneY0u6Fak44B8y1Dz9OcZjBq6uQlwD8tQ3/UPrYfasnfjUBfy9DloStOCwno4rSw+7nPtwx9ruY0LwAmWoY+3t43DzWYTUetgDYNSAV+twzd9HKtR1ED23wNJvoX8A9pyhQnyu7r/pLjg9oqswS4sqoatuY0/wPci0qSdL2dUa4Vqvm9GXCRt++3EP4iAV34nV2bfhP1kHzEMvRnNafZ2DL0THvN8285voLa70B/oAToZRn6Oo/r1EONfB/n45YFwB3ll1cV4kTYfd7foJrJq7ID1ZWz1ss1JqNq+yuA8yxDP2K/1P4G9Ea90L5X/jwh/EkCuvArzWlejOoH34Xqa/zIMvQdHvudqIFCA+05vymobHFrLEP/weO4FsDXVJzXW95B4GrPvnYhTpbd9/05cLGPQ3NRg9/meJzrQHUdtUeNaN9jb5uJ6mp60TL0B+0m+dtRuRUiUNPZnrEMPc3vH0iclSSgi5NmrzE+CnjDMvSj5falAm1Ro9PXezn3H4ATtYZ1PLDTMvQbyx3TAzWILtFHUTag5gRvPdXPIkQpO+C+Atzt49AS4O+Wob/ocW49IN4y9FT7305UsprZqKBeD7XOwOWowXbFqAyJR1HN83MQopoksYw4FX8B/o2afuNmz8dtB8zzFsxtH6EGCI1BNZXfU+4ao1ALX/gK5t8DgyWYC3+xDL3YMvR7UImMiqo4NAj4l+Y0p9o5FLAM/ZhHML8JFczXoAZolqBeYi9H9cUPQvWp34BamOjT8slshDgVEtCFT/a6z4vtNchBTTmbACwtl/WqdGR6m0qucw3QwDJ0HWhsGfrw0ilr9v6/oqalNfR2vofXgMu8ZOsSotosQ38DNbXS1/drIvCjl5TEBcB2VH97rt1Hfzeqif1cy9CXWYaebRn6DFRuhgaolduEqBYJ6OJEDEDVKr7SnGY9y9DT7fm1HYGVmtPsCWAZegbqodVFc5oDPS9gP9TeQ6XPxDMYa04zVHOaU4EXqfo7WQTcZRn6PaVpNIU4HSxD/xH1nU/1caiOerHt7HHuZ6gpmqV5EHoCwcB0L9/bj1BpYedqTjPRzmYnxCmRgC58sgz9/1AjeM9BDXQrlQB0Ry2cEmtvK21Cn605zevth9T1qIxbIZTNFofmNBujEs5M9FGMbGCkXXsS4rSzDH0jao0BX1PN2gOL7eQxpecWeOwvtP8ss/iQfZzLMvTPNac5GNgE7NCc5k+a0+xUvdKLs5EEdHGi7kEF5fGa03wYwDL0+ah5twnA15rTDLcMfQFwK9AImAGk2X/GoEYHu5cutR9aS1ELZ1RlC6q//Ee/fiIhfLAXBLqIcgsHeREDzNWc5p+97JuPar6frDnNyrIc5qP62P+Nahn42eMlWYgTIqPcxQnTnGYMx/NaX2cZ+kx7+6uogP+ZZehj7W3dUMtWtkLVPN6xm+RLrzUcteRkjI/bmqhpaZk+jhPitNKc5t+A5/FdEXoNtVa6u3ndXphoFrATNUDuw8oWZ7FfCl4HHrMM/Wl/lF2cHSSgi5PikbY1HJVAY6U93edbYATwhGXoT/q4xp3Aq6gm+KpMA+60DL3Qx3FCnBGa0xwNfILvgZvfo/rGPceKXAq8DHRCDSr9HLgDtcDLBmCuZegp9ij5D1ErDf7V/59CBCoJ6OKk2WtD/4BaMW2AZejpmtOMQi1K0RW19vgML+cFox5o95TfV04J8JBl6P/2a8GF8IPq5EnQnGYIcIFl6D/aK6/dhwr+O1CDT3NQ+RniUAsXrfY4NxJoDmTbXQFClCEBXVTJzth2Luoh85tl6Cvt7ZOAd4GVqJp6vuY026LyVocBbSxDz/K4TjSqL32Ej1vmAmMtQ//G7x9GCD/xRyZDzWmuRQXolnbe91BUKuR+qJapt+wXgM9QiZzqAetQyw7n+O/TiEAhg+KEV5rTDNac5gOoaTtfoDJordCc5n/tqWtTgZeAvsCHmtN0WIa+DZUV6/Jywbwd6kHlK5inAedIMBe1nb1IywWojIdVaYKaq36rl30fAE2BkXbgfg0VzF+3DP0t+z5FqHUR6tnn7EK1YLlpTnOY5jRvO8WPIgKIBHRRgV2bnosacbsFlXv6WmA5cCOqbxvUetLf2vueBrAM/TfPFaU0pzkU1efe1cdtF6Oa79f5OE6IWsEy9KOWoY8DHkelc61MGPCe5jSft9diL/UqKuuiAexFrTz4I6oZHgDNabZB9dkfA95BLc36W7nMcs8C79pN8uIsJgFdlKE5zdaokewXo4J0X8vQZ9oj2ocAC4EbNac5yE5pORbVDFhhaVPNad6CmrLT1MdtP0b1K+731+cQ4kyxDP0pVBrXIz4OfQj40l6UCMvQiyxDf90y9HNRq72BmtpZBO4+8zmoZvnbLUOfjEqZXB8o9Hg5uAW4RJrhhQR0UZ5nussdnlNv7NHmpSPYh9rbclCDdx4pPU5zmkGa03weeB9VO6mMC5hiGfr4yqbwCFEXWIb+OSpr3B4fh14BLPKSEe51YDWq2b3UR6gR8C9Yhj7dvs//7G0ZqORNUyxD3yg5GgTIoDjhhb3IylIgCrjYMvSFHvuSUPPKn7YM/TEv5zZA1biv8HGbfOBmy9C/8Fe5hahpdlP4bNQa6FXZC1xhGfqySq5zM6qP/QfgUrs1zHP/K6jm+s9Rs0rkQS6khn6205ymQ3Oa12pO09Cc5lh7wFsqcI19yEx77nmpq+w/vY3aTQB+w3cwT0eNjJdgLgKKZei7UK1XX/k4NBYwNad5QyX7h9l/PuMlmE9GBfPlwC0SzEUpqaGfxey54z+g8lWXSketZLZac5oTUbnbU1Aj1Mehmtx/QI1kL/G41gBUJixf6SpX2efu9tsHEaKWsVchfBa1jKovTwJPegZmezDpL8B/gQcsQz9gb78QmIeq4Q+wDN1XE784i0hAP4tpTvNz1Aj1e1BNd9cB/0Et/djVMvRCzWm+CPwV1d/tAqYD93gOwNGc5hhU82CFxSfKmQncZBl6vn8/iRC1k5317V2qHksCKkfDLZahH/U49znUb68YlXTmKGrAahhqGdbV9uJGD6Fq9C5UMptnLEPf4u/PImo/CehnKc1pNgSygP9ahn6r5jTDUYPYuqBq0DvszG4uVM17FDDTMvRry13ncdS0nQqj3Mt5FnhUmgfF2UZzmucCXwLNfBy6DNWvvtfj3DaoYD4fFcw7oBLVfG2PdfkBaIdajXADaqnWEOBWy9A/8e8nEbWdBPQAZPd5T0LN/d4IvGIZenq5YzqimtJfQKVj/Ro1Qne8Zeh5mtPUUOlXb7anzyxCLZV6j2Xor3m8AFTWB1jqGDDJXj9diLOSnUVxDqD5OHQn6oV6tedGjwWQ/mEZ+vP2tjmoF+3XgcctQz9or+b2JdALVYtf4d9PImozCegBRnOafweeoGzzd+kgtFSP44JReaPTgVBU8oqHS2vQmtP8BPWwaGkH+NaoGkQTVHKZB1A1h6rsB66yDP13P3w0Ieo0e8zKZ8ClPg7NA260DH2Wx7n1gQmWob9j/zsBlf/9G8vQR5e7TwKq22yaZeh/8t8nELWdjHIPEJrTDNec5qfAc6gf+iVAH9QUmjjKDc6x55e/BLRHBd5X7HzSEZrTfAqVMOZty9Dz7OPTgCtR/Xmf4DuYr0cN2pFgLgRgGfphYDQqQ1xVGqAS0Dzkce6R0mBua2X/+ZOX++xEtcz5yjMvAowE9ABgj6j9HtX8/SPQyzL07y1D/wNVm85GZZgq71nUA6EfsNVuwtsHTEH1zT1S7vjmqD51X9+bb1E52dNO7RMJEZgsQy+2DP0vwJ1AURWHBgHPa07zfc1pehtQt9P+s3P5HZrTrAe0QP3uS7eF2jkkRACTgB4A7Gby0rf3Qahad+m+XFStOtnLefmoFK9PoDLEjUINlLsXNTinoPRYu7bwJccXiajMy6g+QElDKUQl7MVXLkH93qpyCzBfc5pl0ifb0z5/A261p7h5ehZ7URiPbW+iFlfqX51yi9pN+tADiOY0n0HVqtNQzd377VHoTwBrUMkudgHzvM0Dt0e+H7NTvJZuCwPeArytFuWpEPizvQqbEOIE2INTvwF81Z63AqMtQ3e/mGtOMxGV0bEZatppMmoFuGGoVRJ72Msa/xV4ETVA9WFgjWXoFZrqRd0nAT2A2E3vpXPLF6NWTHu6ksPXoB4ks4Hl3qaT2bWCL7HztlchE7jWMvQFp1h0Ic5a9lzyL1DBuCqHgDGWoX/vcW4C8Dyqu82BWlr1R9QAugOa0xyNmsGyH/VbjkWNhfkO9YIgASCASEAPMJrTjEBlmOprb9qCSk5hAfFAf1T61sEcnzv+Myo7nGdSiy6ogN/Oxy1TgFGSyEKIU6c5zVDU9LPbfRxaDNxvGfr/lTu/AdARSLMMPdPe1gM13TQINctlpb19CvAUcJtl6O/79YOIGiUBPQDZc1GXoUbCPmEZ+pNejokFRqIG1Tzhmb1Nc5ojUJmron3caj5wnWXo2T6OE0KcAM1p3o9qHvc1vulN4N7SpVa9XKcF6hmQgPqNzvTYNwDVVP+cZeiGXwouagUJ6AFKc5p9UTX1+sA1lqH7Wiyi9Ly7gVeAYB+HVvlAEUKcGs1pXgZ8CkT6ONTrC7Wd9GkBaoDsI5ahP1tu/0zgamCsZeif+a3gosZJQA9gmtO8BvgfaqnSc8tnnyp3bAgqj/uffVzWa5OfEMJ/NKfZDdXl1drHoRW6vDSn2RVYiBr8elO5696Aeln4xTJ03a+FFjVOpq0FMLuZ7VFUooo5djN7BZrTjEENoPMVzA+jHh4SzIU4jSxDX49K3uQrMVMnYKnmNM/3ODcZNYamTH+85jQHodI1Z6FSQ4sAIzX0s4DmNKcD44EPLUO/pdy+9qiaQIUEFeVUmDYjhDi97CQxU1G/36oUAndahj6tkuskovrUGwMjZEZKYJIa+tlhEmpqyz2eGzWnqaMGx/gK5r8CAyWYC3FmWYZ+zDL0CaiWtqpqX6HAVM1pvqg5zTLPdTuXxDeo7HF/9gzm9lRXESCkhh5ANKd5I7DWMvR1J3DsRNTAtlAfh34ATPbMGieEOPPsMTEfARE+Dv0GNeAt1+PcO4HWlqH/w2PbUNQiMHecjvKKM08CeoCwlzjdjMoGNcAy9H2VHBeEqq3/zcclSwDDMvQX/FpQIcQps2evlC64VJV1qPEuOyq5TltU61xToH/pHHVRt0mTe+D4B6pJLRH42p66Uoad2vVrfAfzPOBqCeZC1C524O0P+ArA3YFl9kC4MuyX/9molLEO1OwWEQAkoAcAe8DLAx6bBgHveTlmEWr5xqrsRE1xm+XjOCFEDbAMPR04D5jp49AWwELNaY4r3WC30H0KdPM4bojmNL2txijqGGlyDwCa0/wYGOdl12OWoT9tv6V/jfqBV2UZapW1vf4uoxDCv+wBbU9TcZljb54BHkNloXvAy/40oLNn+mdR90hAr+M0pzkQtRCLt9GqLuBVYDJQoQm+nM+AW+UHLUTdojnN8aipbb6WNl4B9Kti/8OWoTv9VjBxxklAr+M0p/k7aqGVU+UCnvSW710IUTdoTvMc1PLIzatxmRwgqbIBtaL2kz70OsxO41idYH4UNb1FgrkQdZhl6L+jMsutr8ZlIql8uWVRB0gNvY6yR7FvxHeu58rsRfWXL/NfqYQQNckewf4pcNkpXqIY6H0iuSxE7SM19Lrrfk49mK9GzT2VYC5EALEMPQe4HHj5FC8RDLzkvxKJM0lq6HWQvdbxZnwvr+jNRqCfZeh5/i2VEKI20ZzmAuD8Uzx9lGXo3/qxOOIMkBp63fQMpxbMQa3ONMqPZRFC1DKa07ybUw/mAC/aSyqLOkQCeh2jOc2ewG3VuIQDeF9zmv39VCQhRC2iOc2LgVeqeZnOgOR4r2MkoNc9L1H9/9/qA7M0pxnvh/IIIWoJzWl2AT5H9YVX1xOa04zxw3XEGSIBvQ7RnOblwDA/Xa4lMEdzmg38dD0hRA3SnGZT1Epr0X66ZBNgip+uJc4AGRRXR2hOMxSwgCQ/X3oWaiGWEj9fVwhxhtj93QuAc/186QKgq2XoqX6+rjgNpIZed9yF/4P5EmA+vtPCCiFqMcvQi1Apnp8Btvjx0mGArLpYR0gNvQ7QnGZj1I+0kR8utwn4GPjEMnR//vCFELWEPeh1LHADqnutunTL0H/xw3XEaSQBvQ7QnOarwD3VuMQe1OIrn1iGvsI/pRJC1Hb2cqnDgBuBq4GoU7zUSlQyKgkYtZgE9FpOc5qdUPmZT3ZO6CHUesmfAAukj1yIs5udLnoUKriPRDWnn4ybLUP/yO8FE34jAb2W05zmbGD0CR5+FPgW1aQ+1zL0Y6etYEKIOktzmo2Aa4FxgI735ZfL2w10tAw9/3SWTZw6Cei1mOY0hwE/+TisGDW69WPgS8vQD5/2ggkhAoadj2Isqube08fhj1uG/tTpL5U4FRLQaym772sVlf/AlqGa02dYhr73jBVMCBGwNKepoWrt44A2Xg7JQ62ZvudMlkucGAnotZTmNG8DppXbLCPUhRCnneY0HcA5qJr79UAzj93vW4ZenfTT4jSRgF4L2dnbNqOmm5SOUP/YMvSVNVowIcRZx05aMxxVa78KiAD6Woa+ukYLJiqQ1XRqpzuAeajauIxQF0LUGDtpzTxgnuY066MG6eqABPRaRmrotZDmNIMkiAshhDgZEtCFEEKIACC53IUQQogAIAFdCCGECAAS0IUQQogAIAFdCCGECAAS0IUQQogAIAFdCCGECAAS0IUQQogA4JdMcRNm9KkPdAfaA+2A1pz8WrtCnIhjwDZgK5AKrJs+ZlVBzRZJBIIJM/qEUfY51haoV6OFEoGqAEij7HPsSHUvWu3EMhNm9BkJfAg0rW5hhDgFu4Hrpo9ZtbimCyLqrgkz+gwG/ge0qumyiLNSBnDz9DGr5lbnIv5ocr8dCeai5rQCbqrpQog67yYkmIua0xQVS6vFHwHd4YdrCFEd8h0U1SXfIVHTqv0dlEFxQgghRACQgC6EEEIEAAnoQgghRACQgC6EEEIEAAnoQgghRACQgC6EEEIEAAnoQgghRACQgC6EEEIEAAnoQgghRACQgC6EEEIEAAnoQgghRACQgC6EEEIEAL+sh346tW3clYToDrRomMDhY5nszdlByoE/OFqUX9NFq5WaRMTSplFnADbsX0l+YU4Nl0gIkRCTROuYTsRGJpJXcJi9OTvYlLGavILDNV20Wik6vAkdmnQHYPPBtRw+mlnDJaobam1Aj4tqw4TeD9EtdmCFffmFOfy4eQZzNnzAsaJqrwkfULq1GMikAY8B8PiPN7E106rhEglx9mraII4bez1Av/gLKuw7WpTPgtQvmZU8TQJ7Oe2bdOO+c/8NwIu/3MuaPYtquER1Q61scm9UvxmPDpvmNZgDRIRGckXXScRGJp7hkgkhxIlpEBbFIxe84zWYA4SHRHBpp/G0bdzlDJdMBKpaWUOf2H8KkfViAPh1+zcs3fEDmzPW0qxhHO0aa4xIuoFW0e1ruJRCCFG58b3/StMGLQFYtnM+v6d9R8qBVTSq35x2jTWGdbiGdo21Gi6lCCS1LqAHO4Lp2rw/ADuzN/Pu0idw4QIgLSuFtKwUft32Ddf3uAuXy1WTRRVCiEp1jz0HgIy8Pby55FGKSgoByC04zM5DW/ht+zdc3nUiJSXFNVlMEUBqXUBvEZlAaHAYAKv3LHIHc09FJQV8svrlM100IYQ4IZH1YogObwzA+n1L3cHcU7GrmK+sd8500UQAq3V96J6DQwYmDK/BkgghxKk5UphHiasEgL6tzic4qNbVnUQAqnXfskNHM9l1KJX46PY0bxjPvUNe4N1lT3KkMO+Er5EQ3YG+8efTOqYzEaEN2Z6dgrVvKWv3/F7lefHR7enTSichOommDWLJOnKAbZnJLNnxIwfydns9JyQolMSYjrSKbkeLhglk5u9j16EtbM9KoaD4qNdzBiWOoHVMR4pdxXyx7g2aNmjJ4MRL6NSsN7kFh1iTvoiVuxdWej5AWHA457UdTZtGnYmP7sDhY1lsz9pAdHiTyv+7xCTRt5VO65hORIU3Zl/OTlbuXsjK3Qu9Hj+0zSjiotqSX5jLnA3v48BB95aDuaDd1RwtyuPX7d+wJWMtV2q348BBXmEO32z4wOu1tBYD6NZCDXJcsXsBqQfXV1pOIeq6opJCUg78QZfmfYmsF8Pfhr7KG0seIedY1glfIzYykf7xF9KmUWeiwhuRlrWJjQdWsmLXgirPa9EwgX7xw0iM6UjzhnFkHznIjuxNLNnxPXty0ryeE+wIJj6mA/HRHWgZmUj2kQx2HUolLTul0mdv77jz6Ni0JwAz179Ng7BIhrQZSedmfSgoPsaa9N9YsXtBlc/ukKBQzm1zGW0bdyUxJon8gly2ZW0gNLheFf9dWtM/fhitG3WiUf3mHMjdxdq9i1mcNs9ri+6AhOG0bdTF/bwF6NK8L8PaX4uLEhanzWPNnkVcpU0mJCiEwpICvlr/jtdrdWjSg76tdADW7V1M8v4VlZazJtS6gA4wY+2rPHDuyzgcQfSPv5DEmI68ueRRn0HAgYMRncYxpsc9hASFurd3bdGfkZ3GY26bxUcrX6gQKB2OIEZ1vomru91R5jyA/vEXcn2Pe7hvzmUczN9bZl/nZn2Z2P8RYiNbVyhL9pEMPlz1nNcfX59W5zE48RKKSgrZcnAtdwx8mgZhUe79Q1qPJHnfcv71y70UlRRUOL9Dkx5MHvhkhVH+veOGVvrf5dLO47m++91lagodm/ZiaNvRrNpt8uqiByl2le3L658wnN5xQ8k6sp85G95nTM97uazzTcfL2eYyvlj3Bi0j27hH8m7OWEPKgT8q3P+mPn8nLqoNBcXHmJvyX6/lFCKQfLHudYwL3iYkKJRusQN55uKPeXvZ4yTvW+7zXL3dldzU50HCgsPd2zo368uIjmNZvusnpi572muOiQs7XMu4XveXOQ+gX/wFXN1tMlN+uJHtWRvL7GvbuCuT+k8hMaZjhevlFhzm4z/+zW/bv6mwr1vsQC5OugGAlIw/mNT/sTIVioEJF3FR5hieXTDZa96QhJgk7hj4VIX79mh5jrf/JABc0P5qxvf+a5nP17FpT4a0uYwL2l/Fv8x7KCg+Vuacni2HcF7byykqKeSLdW9wWeebuaHnve79gxMv4buU/xIe2oAL2l0FwI7sTV6f3eN63UdS056UuEpYsPWrSstZU2pdkzvA6vTfeHvZE+5g1qJhAo8P/4BJHqPfvbm0043c2OsBQoJCycjbw7yUj/ly/dts2L8SAL3tFYzv87cK593Q8y9cb78EuFwlpGWlsGznfFIPrnd/OYIcwWXOuaLrRB4e9rY7mOcWHGJbZrL7RxZTvyl/GfIiN/V5qNLyhgSF8sDQV8jI38NX1jt8uOp5rH1LAfUSMqn/oxXOiY9uz6PD3nUH800Za5iz4QO+XP8WyftXeH0BiAxvxNie9xEcFEJRSSEbD6xiy8F17jfQPq10Lul0Y6XlBPWScWmn8Ww5uI607BRcuHDgYG/ODr5Oftd93OVdbqtwbu9WOnFRbQD4Zeusk6qlCFFXbcpYw6uLHnLnymgc0QLj/Le4a7CTRvWbV3re0DajmNR/CmHB4Rw6epAfNn3GzPVvuudi94+/kNsHPF7hvFFdbuGWvgZhweG4cLEzezPLds5nc8Yad0At/xy7sMO1PDH8Q3dQzS/MYVtmMjnHsgFoGBbF5IFPctfgZ6v8rA+c+zJ5BYeZnfweH6x0smq3CaiXhbvPea7C8U0iYnnswvfc992WmczcjdP5Yt0brNu7xGvrpAMHtxu/kagAABLmSURBVPV7hLDgcIpdxWw5uJaNB1a5uzY6N+vL1d0mV1nOni2HcF2Pu9ietZHUTAuXfe7+3F3MSX7fXanx9hzr2LQnSXaLxLKd89mfu6vKe9WEWllDB1i0/Vt2ZG/izoFPkxCThAMHersr6RU3lLeXPsa6vUvKHB8d3pgrtT8BYO1bxku/3ucOxl9Z73CV9ieu7jYZve0VzEv5mPTD2wBoFd2eER3HApB15ABvLH6YjQdWua/bMCyakZ1vKjOopXOzPlzT7Q4cONiXu5N3lz1ZplbatUV/JvZ7lOYN47koaQzWvmWVNmsv3fEjby151P1F+mnLFzx24TQ6NOnBwMSL+WDlc+4fo8MRxMT+jxIcFIILFx+tfJ75W/53/GLWu+jtrmRS/ykV7uPCxezkacxOft/9Y4mLastzl/4PBw4GJAzn240feS1jg7BoxvW6n+cX3uluYurcrC9D245i2c75APyR/iu944bSo+U5tGnUuUwtoLRWX+wq5tuU6V7vIUQg+iP9Fx75fix3DHranflsUOLFdI8dxLTlz7B8109ljg8PiWCMXXvclpmMc+EdZZqshyddz819/k6/+AtIatqTzRlrAGgS0YIru04CVK36rSWPlknGUj+0ASM6ji2TiCshJonxvf9KkCOIzPx9TFvxTJluyQ5NunNb/0dJiO7AoMQRWPuWsXDr114/5/p9S3n5twcoLFYVip+2fMEDQ1+hd9xQerYcQqP6zck6st99/C19DcJDIgD4Yt0bzE5+z6OJexp9Wp3P/XZimfJ+3DyDz9e+5n4uNqrfnJdGzSIkKIwBCcP5bM2rXs8LdgRz+4AneHXRQ6yyn8dtG3dlZKfx/JQ6E5erhN+3z2Vo29G0bdyVbrEDWb93qft8z9bJbzZ+4PUeNa1W1tBL7czezJQfx/PZmv+4v4jR4U14UH+NQYkXlzn2/HZXUz+0AS5cTF3+dIVml1nJUzl0NJMgRxDntR3t3j66yy0E22+tby2dUiaYg6p5f772/8p8GW8f8AQORxD5hbn88+c/VWhiTt63nKd/nkiuPcDvtn6PEBIUVuHzFZcU8eaSR8o0dbtcJSzZ8QOgavAtPZrzOzfrTYcmPQD1wlMmmB+/QIVNRcWFvLroQb5Y92aZN9/0w9tIPbgOgIZhlbd8hAXX49uUj8r0F208sJJ3lz3p/vcs63gtfXSXW91/T2ra093PtnTHD2TkpVd6HyEC0b7cnTz10218sNLpbsFrEBbFvUNeYHiH68oce07rke5m6/dXPFuh/3n+5s9JP7wdAL3dFe7tl3QaT72Q+gB8sOLZCpnVjhTm8bU1ld2Ht7q3Tew/hZCgMAqLC3hu4Z0VxhhtObiOZ36ayMH8fQDc2PuvNPToGvT0+uKH3cG81JId37v/Hu+RNyQ+uj294s4FYM2eRcxKnualv9r7lOR3lj3BR6teKNOEn3VkP2v3LAaqfo45HEH8tn2OO5iDeml6ffHD7pr6rORp7hr/5V0muo+Li2pDb4++87SslErvU5NqdUAHFfS+3fgR/5h3PTsPbQFU08vkgU+VCXalX5jsIxl0aNKdQYkjyvxvQMJF7qbe5g3j3ee1jukEQOrB9SfUt9UkogXNG7YC4LuU6WUCvafsIxnMTp4GQFR4Y1pFta1wjAuX+8vjKevIAfffG9aL9viMHdx/n7fpE59lLZVfmOO1P6hBWBRHCtUPo15IeIX9nsyts6rcn5ppsW6v+lH1jx/m/v9mlOdbbSUD5oQIdC5XCT9t+YKH5l7NloNr3dtv6vOQu+YOkGA/x44W5dMiMrHCc2xQ4gjyC1VFoUXDBPd5pc+x/bm7WLrzR5/lqRdSn3aNVIa6BVu/rHSwXH5hrnsgWXhIBK0bec9qV1xSVGFbZv7xZ2Nkpc+xj32WtZQLF79um1Nhe3hIBIV2V2OYj+dYZS0Mpfbl7mTxjnmAGjhXWoEa2WkCDhwAzNnw/gmX+UyrtU3u5WXkpfPU/Fu5d8i/6B47iJCgUC7pNI73VzgB3AGzUf1mPvt7SgN6sCPY3Re9y35Z8KW1vfAJ4PMtbVPGavff42M6kJZ9Ym91nm/lpW/doJrIS+3N2XFC1yovLLge/ROGMyhBNfuVDpIr/bJ6k1tw+IRyTX9lvUv32ME4HEGM7nIrcza8736rXZ3+m/uFTIiz1aGjmTy7YDJ3DHyaAQnDcTiCuLTTeP7v978Dx3/j4SERvp9jDVq5/x4f3Q448edYQnQSDoeqz5UfJFee53MsMSbJPc7Hl6NFHs+xYO/PsT2Hvb9I+BIcFEK/VhcwKPFierY81527JMhReR3V5SrhQK732UqeZidP45zES3A4gri8621MW/40Q9qMBFTFr3RMVm1UZwI6qLfW91c8y79HzcKBg87N+rr3lX45dx/eytRlT1V5ndKmIYcj2D1IxFHFF8FTqEfTubfatbf7gOrDOnHem5tKg6rLVULxKWSXGtb+Gq7pdgdR4Y3ZnrWRD1Y66R47mAE+5vsXVjF9ztPmjDVY+5ahtRjAOa0vJSq8cZ14qxXiTCosLuD9Ff+kTyudkKBQujSv+BzLOnKAVxc9WOV1PLvqjj/Hgis7vIywkOPTwk7mOVba710d+R6VA28Jd3wZnHgJY3reS5OIFuw+vJVP17xCYkxHzm93ZZXnFbuKK8zk8Sb98HaW7pzPoMSL6R03tEyXaW3tOy9V6wJ6w7AoGtaLqbQGeiBvN9uzNtK2UReiPKZIZB3ZT3x0e5o1iGNbZvIJ/R9XVFLA3pwdxEW1IcGjGagqadmb3H9v3ahTlasAtfVontrhhz6XPXbfmcMRRPOGce6+tBNxfY+7Gd3lVnKOZfPWkin8nvYdLlzuUZv+8rU1Fa3FAIKDQujZcgigRvt6vuULEehCgkJpFd2u0la83ILDbNi/gu6xg2kYFk2wI5hiV7G7Cy+mflPSD28jvzD3hO6361AqnZr1dtfUffF8HrVp1JlF27+t9FjPxWM8n3+nKj1nu/vvsZGJHDp68ITPvbTTeMb1ut9duVu49StKXCVlpqH5w6zkqQxMvAgHDvrYrYzph7ezctdCv97H32pdH3q9kAj+rr9e6UpqIUGhNLanfKR7DPD4I/1XQCVcGdXllirvUZqSEdR8Q1CjHfu0Ot9n+fbl7nTXlC/pOI4oj2uV/Rz1uUJTgyqKSgr98kPYlrXBPXhkWPtrT/i8pg1aMqrzzQDMTZnOorS5XpMm+MPGAysrDCyUvnNxtglyBPPQea+5+7bLcziCaBKhFm7Zk7PDXQEpfY45cHCVjylYns+xndmbAWjWoJXPmiqoF4rSaVfnt7uSZh7N956Cg0K4ptsdgGoZ3JaZ7PPavqRlpbj73Ie1v+aEz4sIbch13e8C4OctM/k5dabP1oVTtetQKivLjTv6duOHp+256S+1LqCDWkP4mYs/YWTnCWUSrrRt3JU7Bz3jHgXq2ZexaPtc96C3q7Q/MbrLrRXSLSbEJHH/uS8xrtcD7m2zN7zn/jFNHvgEetsrKvQnJzXtSXt7VSSXq4Tpf7wIQGS9RvxDf4M2Hv3qoDIZPaS/5v6RfLn+Lb+s255+eBu/bJsNqOkrF3e8ocq+71Ktotq5m/JyjpadA34i55+suRuPT03bdSiV1fZDSoizSVR4Y5646EOu0v5U5sU/IboDk/pPcedm2Hjg+HNsxa4F7pkgIzqO5foedxNWLmtabGRr/jz4n/xpwPFZJt+mTHfPYJnQ50FGdBxboRuxTaPOdG7Wx/3vj1a9AKhm9If01+jUrHeZ45tExPLAuS+754p/t+mTSgcBn4xDRw+6B8MNbn0JV2qTquz7LtUysrW7r/zwsfLPMf+Hsm89nmOZ+ftYlDbX7/fwt1rX5F7af1wvpD5je97Hdd3vIiNvD6HB9WgS0cJ9VPrh7cxOfs/97/zCHKYuf5r7hrxIcFAI1/e4myu6TmT34a0EO0KIjUx0DzD7Pe0793k7szczd+N0Rne5hYjQSCYNeIwxPe9lT852SlwltIxsQ3R4Yz5e/RKpmRagpoz1bHkOgxMvISEmiacums6BvHT25+6mcUQLYiMT3V/QlAN/8E0l87tPxYw1r9KtxUCaRMQyofeDXNn1drKPHODwsSxKXMVeE1Z4JkAY2fkmso9msD93F4MSR3BO60sBNeK9X/wwWsd0Yub6N6tVRs9Ru9/UgbdaIfxPfedDgkK5uttkrtAmcTBvLw4HZWrDWUf28/na19z/Liop4K2lj2Gc/xbBQSGM7nIrIzqOI/3wNlyuEmIjW7vH43jm4sjIS2fmujcZa2eJG9/7b1yl/Yk9OdspKC6gZWQijeo3Z3bye+4WtDV7FvHD5s+4OOkGYiMTeWTYuxzM28O+3J3EhDclNrK1u1K0M3sz/1v7ut/+63xlvUvvuPOIi2rLNd3uZETHG9Vz7Ggmxa4ioupVbPncn5eOy1WCwxHERUnXsy93Bzuzt9A3/nyGJ10PqArKoMQRtGnUmc/W/KdaZezQ9Phz7LtNH3sdyV/b1LqAfjB/H88t/DNjetxN28ZdCQkKrdD8nnLgD6Yuf6pCNqFVu01eW2xw+4DHCQ+JUFMzyq03nHLgD35OnVlm2//WvsaBvN3c0PMvRIQ2JLJeDJH1elVZzjeXTCH14Hqu634X9ULq07xhfJnpcAXFx5iz4T2+2fCRe46jP+Qcy+bheWOY0OdBzm0zyi5r5XMvAfbkpPHrtjkMbTuauKg2/O08lXghIy+djQdWorUYSHBQCH8Z8q8Kc+pPVnhIBMOTrrOvv4clafOqdT0h6qKC4mM8Of9WxvS8h87N+hDsCHZPdy21LWsDU5c9VWEGScqBP3jx13u5a/BzNAyLIiy4XoVWwG2ZyRWmfM1N+S9ZRzKY0OdvRNZrRIOwKPe0q8pMX/UvdmRtYmyv+2gQFkXTBnE0bRDn3l9cUsS8TR/zlfWu1yyUp+pY0RGm/DCeG3rey/Ck69XYqbAo8JivXl7OsSy+S/mYkZ0n0CQilr8MUS2l2UcySN633D23/a7Bz5J+eHu1AnpwUAiXdlTZM3MLDrMg9ctTvtaZVOsCOoC1bymP/bgUrcUAWsd0pGVUWyJCG7InZzupBy3+SP+l0nOX7ZzPur2LGZx4Ca2i2xFVrzGHj2ZyIG83Ww6uY4udSMWTCxcLUr9k1W6Tni2HEBfVhhYNEzlalEdG3l42HFjBpgNlB3W5XCV8v+lTlu/6Ga3FABKiO9C0QUv25+5m96FUkvcvdydkKG/5zp/Zm7Oj0pHq+3J3uZdVLM1o5ym/MJe3lz7O52tfIyEmifjo9l5Hn3o2j7277EmS96+ga/N+HCnKY3vmBhbv+IGw4HqM6nILzRrEsSljNQs98hMvTpvH9qwNJ7UwzrAO1xARGgnAdyn/PaHBiUIEoi0H1/LPn2+nY9NetGvclZZRrYms14i9OTvYnrWR5bt+rvRlf/3epfxl9qUMSryYhJgkYsKbknMsi4y8dLZlbah06tTiHfNYt/d3esWdR1xUG2IjEykoPkZm/j427F9JSrnxLQDmtln8sedXuscOJsFeFOtg3l52Hd7Khv0rKk1xunbP7+6XEW+j1bOPZrifY9uyNlTYX1B8lI9WvcDXyVNJjEkiProDEaENKxznOUD60zWvkJq5nh6xgykqKSItayO/75hHiauYy7tMpGVUa7ZmWvy85XilbeVuk4P5e09qZtA5rS+lsd0i/OPmGX7pMj0THC4vmcVOxoQZfb4GrvB5oAh4IUGhvDRqDo3qNyPnWDb3zbmsyhXj/Ojt6WNW3XEmbiQC04QZfd4Cqh6FJs4KDhw8d+n/iItqS0HxUe6bc5k7t/1pNmv6mFW+RzRWoVYOihN105A2l9GofjMAftj86ZkK5kII4TdqMSmV/Gbh1q/PVDD3Cwnowi9Kl6AFlQBo/ubPa7hEQghx8kbb056LXcVlZuzUBRLQhV/0bXW+eynZhalfuRemEUKIuqJzsz7uWTpL0uZxMH9vDZfo5EhAF37hfqstKeK7k1hwQQghaovSpGQuXMzZ+GHNFuYUSEAX1da1eT/39MBFaXPJrGR0vxBC1FYJMUnudNWr039l96HUGi7RyauV09ZE3bLzUCp//06lcPRcMlEIIeqKzPx97ufYoaOZNVyaUyMBXVRbzrEsd9pdIYSoi/JOcJno2kya3IUQQogAIAFdCCGECAAS0IUQQogAIAFdCCGECAAS0IUQQogAIAFdCCGECAD+COjzAf8t+C3EySkCfq7pQog672fUd0mImlCCiqXVUu3lUwEmzOjTCdCB9kA7oDUQVu0LC1HRMWAbsBVIBeZPH7MqrWaLJALBhBl9WgPDOf4cawvUq9FCiUBVAKRx/DlmTh+zKqW6F/VLQBdCCCFEzZI+dCGEECIASEAXQgghAoAEdCGEECIASEAXQgghAoAEdCGEECIASEAXQgghAoAEdCGEECIA/D88g2Z5sOf6NgAAAABJRU5ErkJggg==)

以上结构图中，客户端从主节点读取数据，在客户端写入数据到主节点时， 主节点与从节点进行数据交互保障数据的一致性。
副本集特征：

    N 个节点的集群
    任何节点可作为主节点
    所有写入操作都在主节点上
    自动故障转移
    自动恢复


##### MongoDB副本集设置

在本教程中我们使用同一个MongoDB来做MongoDB主从的实验， 操作步骤如下：

1、关闭正在运行的MongoDB服务器。

现在我们通过指定 --replSet 选项来启动mongoDB。
--replSet 基本语法格式如下：
    mongod --port "PORT" --dbpath "YOUR_DB_DATA_PATH" --replSet "REPLICA_SET_INSTANCE_NAME"

实例
    mongod --port 27017 --dbpath "D:\set up\mongodb\data" --replSet rs0

以上实例会启动一个名为rs0的MongoDB实例，其端口号为27017。
启动后打开命令提示框并连接上mongoDB服务。
在Mongo客户端使用命令rs.initiate()来启动一个新的副本集。
我们可以使用rs.conf()来查看副本集的配置
查看副本集状态使用 rs.status() 命令

##### 副本集添加成员

添加副本集的成员，我们需要使用多台服务器来启动mongo服务。进入Mongo客户端，并使用rs.add()方法来添加副本集的成员。
语法
rs.add() 命令基本语法格式如下：

>rs.add(HOST_NAME:PORT)

实例
假设你已经启动了一个名为mongod1.net，端口号为27017的Mongo服务。 在客户端命令窗口使用rs.add() 命令将其添加到副本集中，命令如下所示：

>rs.add("mongod1.net:27017")
>

MongoDB中你只能通过主节点将Mongo服务添加到副本集中， 判断当前运行的Mongo服务是否为主节点可以使用命令db.isMaster() 。
MongoDB的副本集与我们常见的主从有所不同，主从在主机宕机后所有服务将停止，而副本集在主机宕机后，副本会接管主节点成为主节点，不会出现宕机的情况。


#### 3.1.9、 MongoDB 分片

在Mongodb里面存在另一种集群，就是分片技术,可以满足MongoDB数据量大量增长的需求。

当MongoDB存储海量的数据时，一台机器可能不足以存储数据，也可能不足以提供可接受的读写吞吐量。这时，我们就可以通过在多台机器上分割数据，使得数据库系统能存储和处理更多的数据。
为什么使用分片

    复制所有的写入操作到主节点
    延迟的敏感数据会在主节点查询
    单个副本集限制在12个节点
    当请求量巨大时会出现内存不足。
    本地磁盘不足
    垂直扩展价格昂贵

MongoDB分片

下图展示了在MongoDB中使用分片集群结构分布：
![](data:image/png;base64,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)

上图中主要有如下所述三个主要组件：

- Shard:
    用于存储实际的数据块，实际生产环境中一个shard server角色可由几台机器组个一个replica set承担，防止主机单点故障
    
- Config Server:
    mongod实例，存储了整个 ClusterMetadata，其中包括 chunk信息。
    
- Query Routers:
    前端路由，客户端由此接入，且让整个集群看上去像单一数据库，前端应用可以透明使用。

分片实例:
```shell script
# 分片结构端口分布如下：
Shard Server 1:27020
Shard Server 2:27021
Shard Server 3:27022
Shard Server 4:27023
Config Server :27100
Route Process:40000

# 步骤一：启动Shard Server
[root@100 /]# mkdir -p /www/mongoDB/shard/s0
[root@100 /]# mkdir -p /www/mongoDB/shard/s1
[root@100 /]# mkdir -p /www/mongoDB/shard/s2
[root@100 /]# mkdir -p /www/mongoDB/shard/s3
[root@100 /]# mkdir -p /www/mongoDB/shard/log
[root@100 /]# /usr/local/mongoDB/bin/mongod --port 27020 --dbpath=/www/mongoDB/shard/s0 --logpath=/www/mongoDB/shard/log/s0.log --logappend --fork
....
[root@100 /]# /usr/local/mongoDB/bin/mongod --port 27023 --dbpath=/www/mongoDB/shard/s3 --logpath=/www/mongoDB/shard/log/s3.log --logappend --fork

# 步骤二： 启动Config Server
[root@100 /]# mkdir -p /www/mongoDB/shard/config
[root@100 /]# /usr/local/mongoDB/bin/mongod --port 27100 --dbpath=/www/mongoDB/shard/config --logpath=/www/mongoDB/shard/log/config.log --logappend --fork
# 注意：这里我们完全可以像启动普通mongodb服务一样启动，不需要添加—shardsvr和configsvr参数。因为这两个参数的作用就是改变启动端口的，所以我们自行指定了端口就可以。

# 步骤三： 启动Route Process
/usr/local/mongoDB/bin/mongos --port 40000 --configdb localhost:27100 --fork --logpath=/www/mongoDB/shard/log/route.log --chunkSize 500
# mongos启动参数中，chunkSize这一项是用来指定chunk的大小的，单位是MB，默认大小为200MB.

# 步骤四： 配置Sharding
# 接下来，我们使用MongoDB Shell登录到mongos，添加Shard节点
[root@100 shard]# /usr/local/mongoDB/bin/mongo admin --port 40000
MongoDB shell version: 2.0.7
connecting to: 127.0.0.1:40000/admin
mongos> db.runCommand({ addshard:"localhost:27020" })
{ "shardAdded" : "shard0000", "ok" : 1 }
......
mongos> db.runCommand({ addshard:"localhost:27029" })
{ "shardAdded" : "shard0009", "ok" : 1 }
mongos> db.runCommand({ enablesharding:"test" }) #设置分片存储的数据库
{ "ok" : 1 }
mongos> db.runCommand({ shardcollection: "test.log", key: { id:1,time:1}})
{ "collectionsharded" : "test.log", "ok" : 1 }

# 步骤五： 程序代码内无需太大更改，直接按照连接普通的mongo数据库那样，将数据库连接接入接口40000
```


#### 3.1.10、 MongoDB 备份与恢复
备份(mongodump)与恢复(mongorestore)

##### 备份
在Mongodb中我们使用mongodump命令来备份MongoDB数据。该命令可以导出所有数据到指定目录中。
mongodump命令可以通过参数指定导出的数据量级转存的服务器。

mongodump命令脚本语法如下：
   >mongodump -h dbhost -d dbname -o dbdirectory

    -h：  MongDB所在服务器地址，
          例如：127.0.0.1，当然也可以指定端口号：127.0.0.1:27017

    -d：  需要备份的数据库实例，
          例如：test

    -o：  备份的数据存放位置，
          例如：c:\data\dump，当然该目录需要提前建立，在备份完成后，系统自动在dump目录下建立一个test目录，这个目录里面存放该数据库实例的备份数据。 

实例

在本地使用 27017 启动你的mongod服务。打开命令提示符窗口，进入MongoDB安装目录的bin目录输入命令mongodump:
  >mongodump

执行以上命令后，客户端会连接到ip为 127.0.0.1 端口号为 27017 的MongoDB服务上，并备份所有数据到 bin/dump/ 目录中。命令输出结果如下： 


mongodump 命令可选参数列表如下所示：

|语法|描述|实例|
|--|---|----|
|mongodump --host HOST_NAME --port PORT_NUMBER	|该命令将备份所有MongoDB数据	|mongodump --host runoob.com --port 27017|
|mongodump --dbpath DB_PATH --out BACKUP_DIRECTORY|		|mongodump --dbpath /data/db/ --out /data/backup/|
|mongodump --collection COLLECTION --db DB_NAME	|该命令将备份指定数据库的集合。	|mongodump --collection mycol --db test|


##### 恢复备份

mongodb使用 mongorestore 命令来恢复备份的数据。
语法

mongorestore命令脚本语法如下：

>mongorestore -h <hostname><:port> -d dbname <path>

    --host <:port>, -h <:port>：
    MongoDB所在服务器地址，默认为： localhost:27017
    
    --db , -d ：
    需要恢复的数据库实例，例如：test，当然这个名称也可以和备份时候的不一样，比如test2
    
    --drop：
    恢复的时候，先删除当前数据，然后恢复备份的数据。就是说，恢复后，备份后添加修改的数据都会被删除，慎用哦！
    
    <path>：
    mongorestore 最后的一个参数，设置备份数据所在位置，例如：c:\data\dump\test。
    
    你不能同时指定 <path> 和 --dir 选项，--dir也可以设置备份目录。
   
    --dir：
    指定备份的目录

    你不能同时指定 <path> 和 --dir 选项。

接下来我们执行以下命令:

>mongorestore

执行以上命令输出结果如下：


#### 3.1.11、 MongoDB 监控

在你已经安装部署并允许MongoDB服务后，你必须要了解MongoDB的运行情况，并查看MongoDB的性能。这样在大流量得情况下可以很好的应对并保证MongoDB正常运作。

MongoDB中提供了mongostat 和 mongotop 两个命令来监控MongoDB的运行情况。


##### mongostat 命令

mongostat是mongodb自带的状态检测工具，在命令行下使用。它会间隔固定时间获取mongodb的当前运行状态，并输出。如果你发现数据库突然变慢或者有其他问题的话，你第一手的操作就考虑采用mongostat来查看mongo的状态。

启动你的Mongod服务，进入到你安装的MongoDB目录下的bin目录， 然后输入mongostat命令，如下所示：

```shell script
zx@zx:~$ mongostat
insert query update delete getmore command dirty used flushes vsize   res qrw arw net_in net_out conn                time
    *0    *0     *0     *0       0     2|0  0.0% 0.0%       0  998M 70.0M 0|0 1|0   158b   58.0k    2 Apr 10 16:07:31.511
    *0    *0     *0     *0       0     1|0  0.0% 0.0%       0  998M 70.0M 0|0 1|0   157b   57.6k    2 Apr 10 16:07:32.513
    *0    *0     *0     *0       0     2|0  0.0% 0.0%       0  998M 70.0M 0|0 1|0   158b   57.9k    2 Apr 10 16:07:33.510
    *0    *0     *0     *0       0     1|0  0.0% 0.0%       0  998M 70.0M 0|0 1|0   157b   57.7k    2 Apr 10 16:07:34.511
    *0    *0     *0     *0       0     2|0  0.0% 0.0%       0  998M 70.0M 0|0 1|0   158b   57.8k    2 Apr 10 16:07:35.510
    *0    *0     *0     *0       0     1|0  0.0% 0.0%       0  998M 70.0M 0|0 1|0   157b   57.6k    2 Apr 10 16:07:36.513
    *0    *0     *0     *0       0     2|0  0.0% 0.0%       0  998M 70.0M 0|0 1|0   158b   57.9k    2 Apr 10 16:07:37.510
    *0    *0     *0     *0       0     1|0  0.0% 0.0%       0  998M 70.0M 0|0 1|0   157b   57.7k    2 Apr 10 16:07:38.510
    *0    *0     *0     *0       0     1|0  0.0% 0.0%       0  998M 70.0M 0|0 1|0   157b   57.7k    2 Apr 10 16:07:39.511
    *0    *0     *0     *0       0     2|0  0.0% 0.0%       0  998M 70.0M 0|0 1|0   158b   57.9k    2 Apr 10 16:07:40.508

```


##### mongotop 命令

mongotop也是mongodb下的一个内置工具，mongotop提供了一个方法，用来跟踪一个MongoDB的实例，查看哪些大量的时间花费在读取和写入数据。 
mongotop提供每个集合的水平的统计数据。默认情况下，mongotop返回值的每一秒。

启动你的Mongod服务，进入到你安装的MongoDB目录下的bin目录， 然后输入mongotop命令，如下所示： 

```shell script
zx@zx:~$ mongotop
2020-04-10T16:09:38.086+0800	connected to: 127.0.0.1

                    ns    total    read    write    2020-04-10T16:09:39+08:00
    admin.system.roles      0ms     0ms      0ms                             
  admin.system.version      0ms     0ms      0ms                             
config.system.sessions      0ms     0ms      0ms                             
     local.startup_log      0ms     0ms      0ms                             
  local.system.replset      0ms     0ms      0ms                             
              test.col      0ms     0ms      0ms                             
               zx1.col      0ms     0ms      0ms                             
             zx1.mycol      0ms     0ms      0ms                             
            zx1.writer      0ms     0ms      0ms                             
               zx1.zx1      0ms     0ms      0ms  
```

输出结果字段说明：

|字段名|含义|
|---|---|
|ns  |包含数据库命名空间，后者结合了数据库名称和集合。|
|db  |包含数据库的名称。名为 . 的数据库针对全局锁定，而非特定数据库。|
|total   |mongod花费的时间工作在这个命名空间提供总额。|
|read    |提供了大量的时间，这mongod花费在执行读操作，在此命名空间。|
|write   |提供这个命名空间进行写操作，这mongod花了大量的时间。|

mongotop --locks：
    报告每个数据库的锁的使用中，使用mongotop - 锁
mongotop 10：
    后面的10是<sleeptime>参数 ，可以不使用，等待的时间长度，以秒为单位，mongotop等待调用之间。通过的默认mongotop返回数据的每一秒。 



### 3.2、 MongoDB 高级教程

#### 3.2.1、 MongoDB 关系

MongoDB 的关系表示多个文档之间在逻辑上的相互联系。

文档间可以通过嵌入和引用来建立联系。

MongoDB 中的关系可以是：

    1:1 (1对1)
    1: N (1对多)
    N: 1 (多对1)
    N: N (多对多) 

接下来我们来考虑下用户与用户地址的关系。

一个用户可以有多个地址，所以是一对多的关系。

以下是 user 文档的简单结构：
```shell script
{
   "_id":ObjectId("52ffc33cd85242f436000001"),
   "name": "Tom Hanks",
   "contact": "987654321",
   "dob": "01-01-1991"
}
```
以下是 address 文档的简单结构：
```shell script
{
   "_id":ObjectId("52ffc4a5d85242602e000000"),
   "building": "22 A, Indiana Apt",
   "pincode": 123456,
   "city": "Los Angeles",
   "state": "California"
} 
```

##### 嵌入式关系

使用嵌入式方法，我们可以把用户地址嵌入到用户的文档中：
```shell script
{
   "_id":ObjectId("52ffc33cd85242f436000001"),
   "contact": "987654321",
   "dob": "01-01-1991",
   "name": "Tom Benzamin",
   "address": [
      {
         "building": "22 A, Indiana Apt",
         "pincode": 123456,
         "city": "Los Angeles",
         "state": "California"
      },
      {
         "building": "170 A, Acropolis Apt",
         "pincode": 456789,
         "city": "Chicago",
         "state": "Illinois"
      }]
} 
```
以上数据保存在单一的文档中，可以比较容易的获取和维护数据。 你可以这样查询用户的地址：
>db.users.findOne({"name":"Tom Benzamin"},{"address":1})

注意：以上查询中 db 和 users 表示数据库和集合。
这种数据结构的缺点是，如果用户和用户地址在不断增加，数据量不断变大，会影响读写性能。



##### 引用式关系

引用式关系是设计数据库时经常用到的方法，这种方法把用户数据文档和用户地址数据文档分开，通过引用文档的 id 字段来建立关系。
```shell script
{
   "_id":ObjectId("52ffc33cd85242f436000001"),
   "contact": "987654321",
   "dob": "01-01-1991",
   "name": "Tom Benzamin",
   "address_ids": [
      ObjectId("52ffc4a5d85242602e000000"),
      ObjectId("52ffc4a5d85242602e000001")
   ]
}
```
以上实例中，用户文档的 address_ids 字段包含用户地址的对象id（ObjectId）数组。

我们可以读取这些用户地址的对象id（ObjectId）来获取用户的详细地址信息。

这种方法需要两次查询，第一次查询用户地址的对象id（ObjectId），第二次通过查询的id获取用户的详细地址信息。

>var result = db.users.findOne({"name":"Tom Benzamin"},{"address_ids":1})
>var addresses = db.address.find({"_id":{"$in":result["address_ids"]}})


var result = db.users.findOne({"name":"Tom Benzamin"},{"address_ids":1})
注意这一句中的 findOne 不能写成 find，因为 find 返回的数据类型是数组，findOne 返回的数据类型是对象。
如果这一句使用了 find，那么下面一句应该改写为:
var addresses = db.address.find({"_id":{"$in":result[0]["address_ids"]}})


#### 3.2.2、 MongoDB 数据库引用

在上一章节MongoDB关系中我们提到了MongoDB的引用来规范数据结构文档。

MongoDB 引用有两种：

    手动引用（Manual References）
    DBRefs

DBRefs vs 手动引用

考虑这样的一个场景，我们在不同的集合中 (address_home, address_office, address_mailing, 等)存储不同的地址（住址，办公室地址，邮件地址等）。

这样，我们在调用不同地址时，也需要指定集合，一个文档从多个集合引用文档，我们应该使用 DBRefs。
使用 DBRefs

DBRef的形式：

{ $ref : , $id : , $db :  }

三个字段表示的意义为：

    $ref：集合名称
    $id：引用的id
    $db:数据库名称，可选参数

以下实例中用户数据文档使用了 DBRef, 字段 address：

```shell script
{
   "_id":ObjectId("53402597d852426020000002"),
   "address": {
   "$ref": "address_home",
   "$id": ObjectId("534009e4d852427820000002"),
   "$db": "runoob"},
   "contact": "987654321",
   "dob": "01-01-1991",
   "name": "Tom Benzamin"
}
```

address DBRef 字段指定了引用的地址文档是在 runoob 数据库下的 address_home 集合，id 为 534009e4d852427820000002。

以下代码中，我们通过指定 $ref 参数（address_home 集合）来查找集合中指定id的用户地址信息：

>var user = db.users.findOne({"name":"Tom Benzamin"})
>var dbRef = user.address
>db[dbRef.$ref].findOne({"_id":ObjectId(dbRef.$id)})

以上实例返回了 address_home 集合中的地址数据：

```shell script
{
   "_id" : ObjectId("534009e4d852427820000002"),
   "building" : "22 A, Indiana Apt",
   "pincode" : 123456,
   "city" : "Los Angeles",
   "state" : "California"
}
```


#### 3.2.3、 MongoDB 覆盖索引查询

官方的MongoDB的文档中说明，覆盖查询是以下的查询：

    所有的查询字段是索引的一部分
    所有的查询返回字段在同一个索引中

由于所有出现在查询中的字段是索引的一部分， MongoDB 无需在整个数据文档中检索匹配查询条件和返回使用相同索引的查询结果。

因为索引存在于RAM中，从索引中获取数据比通过扫描文档读取数据要快得多。 

使用覆盖索引查询
为了测试覆盖索引查询，使用以下 users 集合:
```shell script
{
   "_id": ObjectId("53402597d852426020000002"),
   "contact": "987654321",
   "dob": "01-01-1991",
   "gender": "M",
   "name": "Tom Benzamin",
   "user_name": "tombenzamin"
}
```

我们在 users 集合中创建联合索引，字段为 gender 和 user_name :
>db.users.ensureIndex({gender:1,user_name:1})

现在，该索引会覆盖以下查询：
>db.users.find({gender:"M"},{user_name:1,_id:0})

也就是说，对于上述查询，MongoDB的不会去数据库文件中查找。相反，它会从索引中提取数据，这是非常快速的数据查询。
由于我们的索引中不包括 _id 字段，_id在查询中会默认返回，我们可以在MongoDB的查询结果集中排除它。
下面的实例没有排除_id，查询就不会被覆盖：
>db.users.find({gender:"M"},{user_name:1})

最后，如果是以下的查询，不能使用覆盖索引查询：

    所有索引字段是一个数组
    所有索引字段是一个子文档 


#### 3.2.4、 MongoDB 查询分析

MongoDB 查询分析可以确保我们所建立的索引是否有效，是查询语句性能分析的重要工具。
MongoDB 查询分析常用函数有：explain() 和 hint()。

#####使用 explain()
explain 操作提供了查询信息，使用索引及查询统计等。有利于我们对索引的优化。

接下来我们在 users 集合中创建 gender 和 user_name 的索引：
>db.users.ensureIndex({gender:1,user_name:1})

现在在查询语句中使用 explain ：
>db.users.find({gender:"M"},{user_name:1,_id:0}).explain()

以上的 explain() 查询返回如下结果：
```shell script
{
   "cursor" : "BtreeCursor gender_1_user_name_1",
   "isMultiKey" : false,
   "n" : 1,
   "nscannedObjects" : 0,
   "nscanned" : 1,
   "nscannedObjectsAllPlans" : 0,
   "nscannedAllPlans" : 1,
   "scanAndOrder" : false,
   "indexOnly" : true,
   "nYields" : 0,
   "nChunkSkips" : 0,
   "millis" : 0,
   "indexBounds" : {
      "gender" : [
         [
            "M",
            "M"
         ]
      ],
      "user_name" : [
         [
            {
               "$minElement" : 1
            },
            {
               "$maxElement" : 1
            }
         ]
      ]
   }
}
```
现在，我们看看这个结果集的字段：

|字段名   |含义   |
|---|---|
|indexOnly| 字段为 true ，表示我们使用了索引|
|cursor|因为这个查询使用了索引，MongoDB 中索引存储在B树结构中，所以这是也使用了 BtreeCursor 类型的游标。如果没有使用索引，游标的类型是 BasicCursor。这个键还会给出你所使用的索引的名称，你通过这个名称可以查看当前数据库下的system.indexes集合（系统自动创建，由于存储索引信息，这个稍微会提到）来得到索引的详细信息|
|n|当前查询返回的文档数量|
|nscanned/nscannedObjects|表明当前这次查询一共扫描了集合中多少个文档，我们的目的是，让这个数值和返回文档的数量越接近越好|
|millis|当前查询所需时间，毫秒数|
|indexBounds|当前查询具体使用的索引|


##### 使用 hint()

虽然MongoDB查询优化器一般工作的很不错，但是也可以使用 hint 来强制 MongoDB 使用一个指定的索引。
这种方法某些情形下会提升性能。 一个有索引的 collection 并且执行一个多字段的查询(一些字段已经索引了)。

如下查询实例指定了使用 gender 和 user_name 索引字段来查询：
>db.users.find({gender:"M"},{user_name:1,_id:0}).hint({gender:1,user_name:1})

可以使用 explain() 函数来分析以上查询：
>db.users.find({gender:"M"},{user_name:1,_id:0}).hint({gender:1,user_name:1}).explain()


#### 3.2.5、 MongoDB 原子操作

mongodb不支持事务，所以，在你的项目中应用时，要注意这点。无论什么设计，都不要要求mongodb保证数据的完整性。

但是mongodb提供了许多原子操作，比如文档的保存，修改，删除等，都是原子操作。

所谓原子操作就是要么这个文档保存到Mongodb，要么没有保存到Mongodb，不会出现查询到的文档没有保存完整的情况。
原子操作数据模型

考虑下面的例子，图书馆的书籍及结账信息。

实例说明了在一个相同的文档中如何确保嵌入字段关联原子操作（update：更新）的字段是同步的。
```shell script
book = {
          _id: 123456789,
          title: "MongoDB: The Definitive Guide",
          author: [ "Kristina Chodorow", "Mike Dirolf" ],
          published_date: ISODate("2010-09-24"),
          pages: 216,
          language: "English",
          publisher_id: "oreilly",
          available: 3,
          checkout: [ { by: "joe", date: ISODate("2012-10-15") } ]
        }
```
你可以使用 db.collection.findAndModify() 方法来判断书籍是否可结算并更新新的结算信息。

在同一个文档中嵌入的 available 和 checkout 字段来确保这些字段是同步更新的:
```shell script
db.books.findAndModify ( {
   query: {
            _id: 123456789,
            available: { $gt: 0 }
          },
   update: {
             $inc: { available: -1 },
             $push: { checkout: { by: "abc", date: new Date() } }
           }
} )
```


|原子操作常用命令| 含义|实例|
|------------|-----|-----|
|$set | 用来指定一个键并更新键值，若键不存在并创建 | { $set : { field : value } }|
|$unset |用来删除一个键 |{ $unset : { field : 1} }|
|$inc |$inc可以对文档的某个值为数字型（只能为满足要求的数字）的键进行增减的操作| { $inc : { field : value } }|
|$push |把value追加到field里面去，field一定要是数组类型才行，如果field不存在，会新增一个数组类型加进去|{ $push : { field : value } }|
|$pushAll |同$push,只是一次可以追加多个值到一个数组字段内 |{ $pushAll : { field : value_array } }|
|$pull |从数组field内删除一个等于value值 |{ $pull : { field : _value } }|
|$addToSet |增加一个值到数组内，而且只有当这个值不在数组内才增加|  |
|$pop |删除数组的第一个或最后一个元素 |{ $pop : { field : 1 } }|
|$rename |修改字段名称 |{ $rename : { old_field_name : new_field_name } }|
|$bit |位操作，integer类型 |{$bit : { field : {and : 5}}}|


偏移操作符
> t.find() { "_id" : ObjectId("4b97e62bf1d8c7152c9ccb74"), "title" : "ABC", "comments" : [ { "by" : "joe", "votes" : 3 }, { "by" : "jane", "votes" : 7 } ] }
 
> t.update( {'comments.by':'joe'}, {$inc:{'comments.$.votes':1}}, false, true )
 
> t.find() { "_id" : ObjectId("4b97e62bf1d8c7152c9ccb74"), "title" : "ABC", "comments" : [ { "by" : "joe", "votes" : 4 }, { "by" : "jane", "votes" : 7 } ] }


#### 3.2.6、 MongoDB 高级索引

考虑以下文档集合（users ）:
```shell script
{
   "address": {
      "city": "Los Angeles",
      "state": "California",
      "pincode": "123"
   },
   "tags": [
      "music",
      "cricket",
      "blogs"
   ],
   "name": "Tom Benzamin"
}
```
以上文档包含了 address 子文档和 tags 数组。


##### 索引数组字段

假设我们基于标签来检索用户，为此我们需要对集合中的数组 tags 建立索引。

在数组中创建索引，需要对数组中的每个字段依次建立索引。所以在我们为数组 tags 创建索引时，会为 music、cricket、blogs三个值建立单独的索引。

使用以下命令创建数组索引：
>db.users.ensureIndex({"tags":1})

创建索引后，我们可以这样检索集合的 tags 字段：
>db.users.find({tags:"cricket"})

为了验证我们使用使用了索引，可以使用 explain 命令：
>db.users.find({tags:"cricket"}).explain()

以上命令执行结果中会显示 "cursor" : "BtreeCursor tags_1" ，则表示已经使用了索引。

##### 索引子文档字段

假设我们需要通过city、state、pincode字段来检索文档，由于这些字段是子文档的字段，所以我们需要对子文档建立索引。

为子文档的三个字段创建索引，命令如下：
>db.users.ensureIndex({"address.city":1,"address.state":1,"address.pincode":1})

一旦创建索引，我们可以使用子文档的字段来检索数据：
>db.users.find({"address.city":"Los Angeles"})   

查询表达不一定遵循指定的索引的顺序，mongodb 会自动优化。所以上面创建的索引将支持以下查询：
>db.users.find({"address.state":"California","address.city":"Los Angeles"}) 

同样支持以下查询：
>db.users.find({"address.city":"Los Angeles","address.state":"California","address.pincode":"123"})


#### 3.2.7、 MongoDB 索引限制

##### 额外开销
每个索引占据一定的存储空间，在进行插入，更新和删除操作时也需要对索引进行操作。所以，如果你很少对集合进行读取操作，建议不使用索引。
内存(RAM)使用

由于索引是存储在内存(RAM)中,你应该确保该索引的大小不超过内存的限制。

如果索引的大小大于内存的限制，MongoDB会删除一些索引，这将导致性能下降。

##### 查询限制
索引不能被以下的查询使用：

    正则表达式及非操作符，如 $nin, $not, 等。
    算术运算符，如 $mod, 等。
    $where 子句

所以，检测你的语句是否使用索引是一个好的习惯，可以用explain来查看。

##### 索引键限制
从2.6版本开始，如果现有的索引字段的值超过索引键的限制，MongoDB中不会创建索引。
插入文档超过索引键限制

如果文档的索引字段值超过了索引键的限制，MongoDB不会将任何文档转换成索引的集合。与mongorestore和mongoimport工具类似。
最大范围

    集合中索引不能超过64个
    索引名的长度不能超过128个字符
    一个复合索引最多可以有31个字段


#### 3.2.8、 MongoDB ObjectId

在前面几个章节中我们已经使用了MongoDB 的对象 Id(ObjectId)。

在本章节中，我们将了解的ObjectId的结构。

ObjectId 是一个12字节 BSON 类型数据，有以下格式：

    前4个字节表示时间戳
    接下来的3个字节是机器标识码
    紧接的两个字节由进程id组成（PID）
    最后三个字节是随机数。

MongoDB中存储的文档必须有一个"_id"键。这个键的值可以是任何类型的，默认是个ObjectId对象。

在一个集合里面，每个文档都有唯一的"_id"值，来确保集合里面每个文档都能被唯一标识。

MongoDB采用ObjectId，而不是其他比较常规的做法（比如自动增加的主键）的主要原因，因为在多个 服务器上同步自动增加主键值既费力还费时。
```shell script
# 创建新的ObjectId

# 使用以下代码生成新的ObjectId：
>newObjectId = ObjectId()
# 上面的语句返回以下唯一生成的id：
ObjectId("5349b4ddd2781d08c09890f3")

# 你也可以使用生成的id来取代MongoDB自动生成的ObjectId：
>myObjectId = ObjectId("5349b4ddd2781d08c09890f4")

# 创建文档的时间戳

# 由于 ObjectId 中存储了 4 个字节的时间戳，所以你不需要为你的文档保存时间戳字段，你可以通过 getTimestamp 函数来获取文档的创建时间:
>ObjectId("5349b4ddd2781d08c09890f4").getTimestamp()
# 以上代码将返回 ISO 格式的文档创建时间：
ISODate("2014-04-12T21:49:17Z")

# ObjectId 转换为字符串
# 在某些情况下，您可能需要将ObjectId转换为字符串格式。你可以使用下面的代码：
>new ObjectId().str
# 以上代码将返回Guid格式的字符串：：
5349b4ddd2781d08c09890f3
```




