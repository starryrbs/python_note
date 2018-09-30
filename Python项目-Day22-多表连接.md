##Python项目-Day22-多表连接-index索引

1. 多表查询

	* 等值连接

			SELECT `user`.id,`user`.`name` FROM user ,menu WHERE `user`.id=menu.id

	* 内连接


			SELECT * FROM course as c ,course as cc WHERE c.cno=cc.cpno

	多级评论是内连接,一张表有评论人和被评论人

	* 外连接

			SELECT * FROM user LEFT JOIN menu on `user`.id = menu.id

	* 统计参加考试的学生

			SELECT DISTINCT(sno) from sc WHERE grade is not NUL

	* 左连接

			SELECT * FROM `user` LEFT JOIN menu ON `user`.id=menu.id

	* 右连接


			SELECT * FROM `user` RIGHT JOIN menu on `user`.id=menu.id
	* 内连接

			SELECT * FROM `user` INNER JOIN menu ON `user`.id=menu.id

	连接格式:-- 左连接  表1 left join 表2 on  表1.xx=表2.xx

2. 索引(提高查询速度)

	* 创建索引的原则：经常作为条件的列上适合创建索引

	* 不适合创建索引:经常改动的列；数据比较少

	* 使用索引：dbms决定是否使用索引

	* 系统会为primary key和unique自动创建索引	primary key


	PRIMARY, INDEX, UNIQUE 这3种是一类
	PRIMARY 主键。 就是 唯一 且 不能为空。
	INDEX 索引，普通的
	UNIQUE 唯一索引。 不允许有重复。
	FULLTEXT 是全文索引，用于在一篇文章中，检索文本信息的。

	添加索引
		
		ALTER TABLE student ADD INDEX index_name(sname);
		ALTER TABLE student ADD UNIQUE INDEX index_name(sname);
		ALTER TABLE student ADD FULLTEXT INDEX index_name(sname);
	删除索引
	
		DROP INDEX index_name ON student；
	添加全文索引
	
		ALTER TABLE student add FULLTEXT INDEX index_name(sname)；

3. 创建视图


		CREATE VIEW student_info AS
		SELECT * FROM student

	1、对视图内容的更新直接影响基本表。

	2、当视图来自多个基本表、不允许删除、增加数据。

	查看所有表和视图

		SHOW TABLES;

	删除视图

		DROP VIEW view_stugrade;

	关系型数据库的三大模式:

	![](https://i.imgur.com/5aPT9sM.png)

4. mysql函数

	* 创建函数

			CREATE FUNCTION fun_getage(str VARCHAR(12))
			RETURNS CHAR(12)
			BEGIN
				RETURN(SELECT sage from student WHERE sname=str);
			END;

	* 调用函数

			SELECT fun_getage('李彤')


	* 方法：
		
		1. 必须有返回值
		2. 返回值指定类型 RETURNS
		3. 返回值通过     return 


5. 存储过程

	* mysql'存储过程的参数类型:IN,OUT,INOUT

	
		* IN 输入参数:表示该参数的值必须在调用存储过程时指定，在存储过程中修改该参数的值不能被返回，为默认值
		* OUT 输出参数:该值可在存储过程内部被改变，并可返回
		* INOUT 输入输出参数:既能输入一个值又能传出来一个值


	* 定义变量

		1. 声明变量(使用DECLARE)

				DECLARE score INT  DEFAULT(0);
				
			DEFAULT可选

		2. 赋值变量
				
				1.使用set实现赋值
				set cname_res="不及格";
				2.使用select XX into xx
				SELECT grade into score FROM sc WHERE cno=cid and sno=sid;
				将grade赋值给score
		3. 条件判断

			格式:

				if 条件  then...
				elseif... then
				else...
				End if;
		
				if score<60 THEN
					set cname_res="不及格";
				ELSEIF score>=60 and score<=80 THEN
					SET cname_res="及格";
				ELSE 
					SET cname_res='优秀';
				end IF;

		4. 循环

			mysql有三种循环while 循环 、 loop 循环和repeat循环

			* while  do

					while i < 11 do 　　　　　　　　　　//   循环体
					insert into user_profile (uid) values (i);
					set i = i +1;
					end while;
			* loop


					lp1 : LOOP　　　　　　　　　　　　　　//  lp1 为循环体名称   LOOP 为关键字
					    insert into user_profile (uid) values (i);
					    set i = i+1;
					    if i > 30 then
					leave lp1;　　　　　　　　　　　　　　//  离开循环体
					    end if;
					end LOOP;

			* repeat

					repeat 
					    insert into user_profile_company (uid) values (i+1);
					    set i = i + 1;
					until i >= 20
					
					end repeat;

			注意默认结束符 ";"， 在mysql 操作中语句结束要使用 ";", 不然会出现语法错误。

		* 创建带输入和输出参数的存储过程

				DELIMITER $$
				CREATE FUNCTION func_employee_sal (empno INT(11))
					RETURNS DOUBLE(10,2)
				COMMENT'查询某个雇员的工资'
				BEGIN
					RETURN (SELECT sal
						FROM t_employee
						WHERE t_employee.empno=empno);
				END$$
				DELIMITER ;

		* 删除存储过程和函数

				
				DROP PROCEDURE proce_name;
				DROP FUNCTION func_name;
