##Python项目-Day20

1. daudh

	数据库泛型就是数据库应该遵守的规则。数据库泛型也称为范式。
	目前最常用的四个范式：
	第一范式：数据库的每一列都是不可分割的原子数据项。（简单来说就是属性不可再分割）
	
	id|姓名|地址|
	--|--|--|
	1|张三丰|中国安徽省安庆市|
	
	中国安徽省安庆市不满足第一范式，还可以再分割，应改为：

	id|姓名|所在省份|所在市	
	--|--|--|--|
	1|张三丰|安徽省|安庆市
	
	
	第二范式：满足第一范式的前提下，当存在多个主键的时候，才会发生不符合第二范式的情况。比如两个主键，不能存在这样的属性，它只依赖于其中一个主键，这就是不符合第二范式。
	
	学生证名称|学生证号|学生证办理时间|借书证名称|借书证号|	借书证办理时间
	--|--|--|--|--|--|
	
	
	上面的例子中学生证号和借书证号为联合主键
	而学生证名称依赖学生证号，借书证名称依赖借书证号，不满足第二范式
	
	应该为：
	
	学生证|学生证号|学生证办理时间
	--|--|--|
	
	
	借书证名称|借书证号|借书证办理时间
	--|--|--|
	
	
	
	第三范式：（属性不能传递依赖于主属性）在满足第二范式的前提下，如果某一属性依赖于其他非主键属性，而其他非主键属性又依赖于主键属性，这种情况被称为传递依赖于主属性。
	
	爸爸|儿子|女儿|女儿的小熊
	--|--|--|--|
	
	
	上面的例子中女儿的小熊依赖于女儿，女儿依赖于爸爸
	
	
	应该为2张表：

	爸爸|儿子|女儿
	--|--|--|
	
	
	女儿|女儿的小熊
	--|--|
	
	


2. 关系型数据库编程基础

	> 登陆mysql

		mysql -h localhost -u root -p

	* 实体
	
	现实世界中任何一个可以识别的对象

	* 属性

	实体所具有的特性

	一个实体可用若干属性来描述

	* 在关系数据库中的表现


	实体的实例是储存在表中的行，属性是储存在表中的列

	* 键


	在实体属性中，用于区别实体集合中不同个体的某个属性或某几个属性的组合，称为关键字（键）
	* 主键


	唯一标识的自己的一列
	* 外键

	如果公共关键字在一个关系中是主关键字，那么这个公共关键字被称为另一个关系的外键。由此可见，外键表示了两个关系之间的相关联系。以另一个关系的外键作主关键字的表被称为主表，具有此外键的表被称为主表的从表。外键又称作外关键字
	
	* 实现数据的完整性

		1. 实体完整性（行），对关系中的记录唯一性，也就是主键的约束
		2. 引用完整性，定义外键与主键之间的定义规则
		![](https://i.imgur.com/N9XAU6z.png)
		3. 域完整性和域约束（列），通常是指数据的有效性

		完整性类型|约束类型
		--|--
		实体完整性|PRIMARY KEY 	UNQIUE
		引用完整性|FOREIGN KEY
		域完整性|DEFAULT	CHECK

	* mysql数据类型

		[查看菜鸟教程mysql数据类型](http://www.runoob.com/mysql/mysql-data-types.html)

3. mysql代码

	数据库定义及删除
	
	定义一个学生-课程数据库

		CREATE DATABASE testdb;
		
		CREATE DATABASE school DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

	删除数据库

		drop database if EXISTS testdb;

	查看定义语句

		show CREATE TABLE course;

	创建学生数据表：

		CREATE TABLE student(
			sno varCHAR(9) PRIMARY KEY,
			sname VARCHAR(20) UNIQUE,
			ssex VARCHAR(2),
			sage SMALLINT,
			sdept varchar(20)
		)

	创建课程表

		CREATE TABLE course(
			cno VARCHAR(20) PRIMARY KEY,
			cname varchar(20) UNIQUE,
			cpno VARCHAR(20),
			ccredit VARCHAR(2),
			FOREIGN KEY (cpno) REFERENCES course(cno)
		)

	创建选课表

		CREATE TABLE sc(
			sno VARCHAR(9) ,
			cno VARCHAR(20) ,
			grade SMALLINT,
			PRIMARY KEY(sno,cno),
			FOREIGN KEY (sno) REFERENCES student(sno),
			FOREIGN KEY (cno) REFERENCES course(cno)
		)

	查看表定义

		DESC student;

	添加主键

		ALTER TABLE sc Add PRIMARY KEY(cno,sno)
	
	删除主键
	
		ALTER TABLE sc DROP PRIMARY KEY
	
	删除外键
	>注意这里的外键不是sno，而是sc_ibfk_1
	
	![](https://i.imgur.com/rF8V2pU.png)

		ALTER TABLE sc drop FOREIGN KEY sc_ibfk_1;

	添加主键

		ALTER TABLE sc ADD FOREIGN KEY (sno) REFERENCES student(sno);
		
		ALTER TABLE sc ADD FOREIGN KEY (cno) REFERENCES course(cno);

	添加主键的要求：[点击这里](https://blog.csdn.net/shijiedemuguang/article/details/8026020)

	插入语句

		INSERT INTO course (cname,cpno,ccredit) VALUES ('信息系统','1',4);

	设置属性自动增长（需满足属性是int类型，是主键）

		alter table test modify id int(11) auto_increment;

