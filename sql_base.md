三级模式：外模式、模式、内模式  

候选键：属性的值可以唯一标识一个关系    
主键：在候选键中，不能有重复值  
主属性：包含在候选键中的属性    
外键：可以有重复值  

关系名：    表名    
关系模式：  表头    
关系名：    二维表  
元组：      行  
属性：      列  
分量：      一条记录中某个列的值    

自然连接会去掉重复属性  

左外连接（left outer join）：左边不满足条件的依旧保留，右边为null   
右外连接(right outer join)：右边不满足条件的依旧保留，左边为null    


第一范式：数据库表中的所有字段值都是不可分解的原子值。
第二范式：确保数据库表中的每一列都和主键相关，而不能只与主键的某一部分相关（主要针对联合主键而言）。
第三范式：每一列数据都和主键直接相关，而不能间接相关。要求一个数据库表中不包含已在其他表中已包含的非主关键字信息。

为用户ye定义名为miss的架构： create schema miss authorization ye    
删除架构：  drop schema miss    

约束；
not null：限制列取值非空    
primary key：主键   
foreign key:外键    
unique:限制列取值不能重复   
default:指定列的默认值  
check:限制列的取值范围  

定义表：    
create table Jobs(  
    Jid char(6) primary key,      --在列级定义主键  
    Descp nchar(20) not null,   
    Edu nchar(6) default '本科',    
    MinSalary int,  
    MaxSalary int,  
    check(MaxSalary>MinSalary)    --多列的check约束必须定义在表级
)

create table Employees( 
    Eid char(10),   
    Ename nvarchar(20) not null,    
    Sex nchar(1) check(Sex='男' or Sex='女')，  
    Sid  char(18) unique,   
    Jid char(6),    
    Tel char(11),   
    primary key(Eid),   
    foreign key(kid) references Jobs(Jid)    
)

为Employees表增加工资列:    
alter table Employees   
    add Salary int  

修改Jobs表Descp列的数据类型：   
alter table Jobs    
    alter column Descp nchar(40)    

删除Employees表的Tel列：    
alter table Employees   
    drop column Tel 

添加约束：  
alter table Jobs    
    add chaek(MinSalary >= 1600)    

添加索引：
ALTER TABLE table_name 
    ADD INDEX index_name ON (column(length))    

删除表: 
drop table Jobs 

插入数据：
INSERT INTO table_name (列1, 列2,...) VALUES (值1, 值2,....)    
    
select查询可以是属性列，表达式，常量，函数  
查询全体学生的姓名和出生年份，并在出生年份前加入一个列，此列的每行数据均为”出生年份“    
select Sname, '出生年份'， 2019-age

去掉结果中重复行(distinct放在select的后面，列名的前面，对所有列名去重)  
select distinct Sno from SC 

查询年龄在20~23的学生姓名   
select Sname from Student   
    where Sage between 20 and 23    

或
select Sname from Student   
    where Sage>=20 and Sage<=23 

查询年龄不在20~23的学生姓名 
select Sname from Student   
    where Sage not between 20 and 23    

或  
select Sname from Student   
    where Sage<20 and Sage>23

查询信息工程系、通信工程系学生的姓名    
select Sname from Student   
    where Sdep in ('信息管理系', '通信工程系')      

或
select Sname from Student   
    where Sdep='信息管理系' or Sdep='通信工程系'    


查询不在信息工程系、通信工程系学生的姓名    
select Sname from Student   
    where Sdep not in ('信息管理系', '通信工程系')       

或
select Sname from Student   
    where Sdep！='信息管理系' and Sdep！='通信工程系'   


查询姓”张“姓”李“学生的详细信息  
select * from Student   
    where Sname like '[张李]%'  

升序：asc， 降序：desc  
将学生按年龄升序排列    
select * from Student order by Sage       --默认升序    


查询全体学生的信息，查询结果按所在系的系名升序排列，同一个系的学生按年龄降序排列    
select * from Student   
    order by Sdep asc, Sage desc    

UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

聚合函数(不能出现在where中) 
count ：统计元组个数， 不忽略null值 
sum
avg
max
min

统计选了课程的学生人数（一个人可选多门课程）    
select count(distinct Sno) from SC  

统计每门课程的选课人数：    
select Cno， count(Sno) from SC     
    group by Cno    

统计每个系的学生人数和平均年龄
select Sdep, count(*), avg(Sage) from Student
    group by Sdep

having:可使用聚合函数,对分组后的列作判断
查询选课门数超过3门的学生的学号和选课门数
select Sno， count(*) from SC   
    group by Sno having count(*) > 3    


查询每个学生及其选课的详细信息  
select * from Student join SC   
    on Student.Sno = SC.Sno 

去掉重复列  
select Student.Sno, Sname, Ssex, Sage, Sdep, Cno, Cgrade    
    from Student join SC on Student.Sno = SC.Sno    


3表连接
select Sname， Cname, Grade 
    from Student s join SC on s.Sno = SC.Sno    
    join Course c on c.Cno = SC.Cno 

自连接
查询与刘晨在同一个系学习的学生的姓名和所在系    
select S2.Sname, S2.Sdep from Student S1 join Student S2     
    on S1.Sdep = S2.Sdep    
    where S1.Sname = '刘晨' and S2.Sname != '刘晨'  


课程A分数大于平均分的总人数     
- select  count(*) from test_index where a > (select avg(a) from test_index)        


子查询  
```sql
select name,age 
from person     
where age > ( select age    
              from person   
              where name = '张三'); 
```

in  
```sql
select name 
from person 
where countryid in ( select countryid 
                     from country
                     where countryname = '中国');   
```

some
```sql
select name from person 
where countryid = some ( select countryid from country　　--用等号和以下查询到的值比较，如果与其中一个相等，就返回
                         where countryname = '中国');
```

all
```sql
select name from person 
where countryid > all　( select countryid from country　 --当countryid大于以下返回的所有id，此结果才为True，此结果才返回
                         where countryname = '中国');
```

exists

```sql
SELECT * FROM Person
WHERE exists ( SELECT * FROM Person 
               WHERE Person_Id = 100);   --如果不存在Person_Id的记录，则子查询没有结果集返回，主语句不执行

```


建立索引    
CREATE [UNIQUE][CLUSTERED | NONCLUSTERED]  INDEX  index_name ON {table_name | view_name} [WITH [index_property [,....n]]

说明：  

UNIQUE: 建立唯一索引。      

CLUSTERED: 建立聚集索引。       

NONCLUSTERED: 建立非聚集索引。   


- 自然连接是一种特殊的等值连接，他要求两个关系表中进行比较的必须是相同的属性列，无须添加连接条件，并且在结果中消除重复的属性列。
- 内连接是保证两个表中所有行都满足连接条件，而外连接则不然。内连接基本与自然连接相同，不同之处在于自然连接要求是同名属性列的比较，而内连接则不要求两属性列同名。     
- 外连接不仅包含符合连接条件的行，还包含左表(左连接时)、右表(右连接时)或两个边接表(全外连接)中的所有数据行。      

## drop,delete与truncate
- drop：直接删掉表
- delete：删除表中数据，可以加 where 字句；每次从表中删除一行，并且同时将该行的删除操作作为事务记录在日志中保存以便进行进行回滚操作。
- truncate： 删除表中所有数据，再插入时自增长id又从1开始     

表和索引所占空间：
- 当表被 TRUNCATE 后，这个表和索引所占用的空间会恢复到初始大小
- DELETE 操作不会减少表或索引所占用的空间
- drop 语句将表所占用的空间全释放掉。

应用范围：TRUNCATE 只能对TABLE；DELETE可以是table和view     
TRUNCATE TABLE 删除表中的所有行，但表结构及其列、约束、索引等保持不变。   

## 视图作用：
1. 简化数据查询语句  
2. 提高数据安全性：定制用户可以查看哪些数据，屏蔽敏感数据    
3. 多角度看待同一数据    



