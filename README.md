## 出题前必看

输入描述类似于数据库设计文档，写明白表结构和每个字段的意义及关系；

测试用例可以多个，对于每个测试用例，都在单独干净的Mysql实例中进行运行；

#### 对于每个测试用例的输入部分：

> 为一组SQL语句，应包含：

>> create table建表语句

>> insert数据初始化语句；

>> 如果需要，可以加入其他建索引语句。

#### 对于每个测试用例的输出部分：

通过运行您的标程select语句，得出的符合题意的数据。

#### 如何判题

> 对于题目中的每一个测试用例，都将开启一个Mysql实例；

> 执行测试用例的输入部分的SQL语句，建立表结构和相关索引，插入数据进行数据的初始化；

> 执行考生提交的答案，应该是select语句，提交到Mysql实例进行执行，获取其查询到的数据；

> 将考生答案语句查询到的数据和测试用例的输出部分进行比对，不比对第一行表头，完全一致即为正确。

#### 其他

每一组测试用例的输入部分，其建表语句和建索引语句应该相同，不同的是insert数据初始化语句。

## 题干
Employee Salaries and Departments

## 题目描述
A company uses 2 data tables, Employee and Department, to store data about its employees and departments. Write a query to print the respective Employee Name, Salary, Department Name, and Location for each employee in the Employee table. Sort your results by descending Salary; if two or more employees have the same Salary, then sort those employees alphabetically by Name.

## 输入描述
The Employee and Department tables are described as follows:

```
Employee
Field    Data Type    
ID    Integer    
NAME    String    
SALARY    Integer    
DEPT_ID    Integer
```

where ID is the employee's ID number, NAME is the employee's name, SALARY is the employee's salary in dollars, and DEPT_ID is the ID number for the department where the employee works.

```
Department
Field    Data Type    
DEPT_ID    Integer    
NAME    String    
LOCATION    STRING
```

where DEPT_ID is the department ID number, NAME is the department name (category), and LOCATION is the office location.

## 输出描述
The output must contain 4 columns: "Employee Name", "Salary", "Department Name", and "location".

## 输入样例
```sql
create table Department(dept_id int primary key not null, name varchar(30),location varchar(20));
insert into Department(dept_id,name,location) values(1,'Recruitment','Bangalore');
insert into Department(dept_id,name,location) values(2,'Sales','U.S.A');

create table Employee (id int, name varchar(20), salary int, dept_id int, foreign key(dept_id) references Department(dept_id));
insert into Employee(id, name, salary,dept_id) values (1, 'Hari', 5000,2);
```

## 输出样例
```
Employee Name	Salary	Department Name	location
Hari	5000	Sales	U.S.A
```

## 标程
```sql
SELECT e.name AS "Employee Name", e.salary AS Salary, d.name AS "Department Name", d.location
FROM Employee e
INNER JOIN Department d ON e.dept_id=d.dept_id
ORDER BY e.salary DESC, e.name ASC;
```

## 测试用例一输入
```sql
create table Department(dept_id int primary key not null, name varchar(30),location varchar(20));
insert into Department(dept_id,name,location) values(1,'Recruitment','Bangalore');
insert into Department(dept_id,name,location) values(2,'Sales','U.S.A');
insert into Department(dept_id,name,location) values(3,'Engineering','Kolkata');
insert into Department(dept_id,name,location) values(4,'Product','Bangalore');
insert into Department(dept_id,name,location) values(5,'Research and Development','Kolkata');
insert into Department(dept_id,name,location) values(6,'Operations','U.S.A');
insert into Department(dept_id,name,location) values(7,'Finance','U.S.A');

create table Employee (id int, name varchar(20), salary int, dept_id int, foreign key(dept_id) references Department(dept_id));
insert into Employee(id, name, salary,dept_id) values (1, 'Hari', 5000,2);
insert into Employee(id, name, salary,dept_id) values (3, 'Vivek', 6000,1);
insert into Employee(id, name, salary,dept_id) values (4, 'Rakesh', 1000,3);
insert into Employee(id, name, salary,dept_id) values (5, 'Abhimanyu', 600,3);
insert into Employee(id, name, salary,dept_id) values (6, 'Aakansha', 600,4);
insert into Employee(id, name, salary,dept_id) values (7, 'Scott', 1300,1);
insert into Employee(id, name, salary,dept_id) values (8, 'Jessica', 600,2);
insert into Employee(id, name, salary,dept_id) values (9, 'Stephinie', 400,4);
insert into Employee(id, name, salary,dept_id) values (10, 'Mike', 100,3);
insert into Employee(id, name, salary,dept_id) values (11, 'John', 250,3);
insert into Employee(id, name, salary,dept_id) values (12, 'Michael', 1134,3);
insert into Employee(id, name, salary,dept_id) values (13, 'Ronaldo', 1500,1);
insert into Employee(id, name, salary,dept_id) values (2, 'Heraldo', 1500,1);
insert into Employee(id, name, salary,dept_id) values (14, 'Abhilasha',600,2);
insert into Employee(id, name, salary,dept_id) values (15, 'Rachael', 1234,1);
insert into Employee(id, name, salary,dept_id) values (16, 'Dean', 3454,6);
```

## 测试用例一输出
```
Employee Name	Salary	Department Name	location
Vivek	6000	Recruitment	Bangalore
Hari	5000	Sales	U.S.A
Dean	3454	Operations	U.S.A
Heraldo	1500	Recruitment	Bangalore
Ronaldo	1500	Recruitment	Bangalore
Scott	1300	Recruitment	Bangalore
Rachael	1234	Recruitment	Bangalore
Michael	1134	Engineering	Kolkata
Rakesh	1000	Engineering	Kolkata
Aakansha	600	Product	Bangalore
Abhilasha	600	Sales	U.S.A
Abhimanyu	600	Engineering	Kolkata
Jessica	600	Sales	U.S.A
Stephinie	400	Product	Bangalore
John	250	Engineering	Kolkata
Mike	100	Engineering	Kolkata
```

## 测试用例二输入

您可以提供多组测试用例，也可以不提供。

每一组测试用例的输入部分，其建表语句和建索引语句应该相同，不同的是insert数据初始化语句。

## 测试用例二输出

您可以提供多组测试用例，也可以不提供。

## 其他注意事项

#### MYSQL

> mysql版本：8.0.27

> 默认安装，所以表名和列名大小写敏感（后期有可能改为大小写不敏感）。

#### SQLite

> sqlite版本：3.36.0

> 其语法和标准mysql所支持的SQL有很多地方不一样，参考文档：

> the standard SQL language syntax: https://labfiles.acmcoder.com/sqlite-doc/lang.html

> core functions: https://labfiles.acmcoder.com/sqlite-doc/lang_corefunc.html

> date time functions: https://labfiles.acmcoder.com/sqlite-doc/lang_datefunc.html

> aggregate functions: https://labfiles.acmcoder.com/sqlite-doc/lang_aggfunc.html

> window functions: https://labfiles.acmcoder.com/sqlite-doc/windowfunctions.html

> json functions: https://labfiles.acmcoder.com/sqlite-doc/json1.html