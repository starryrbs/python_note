##Python项目-Day21-数据查询
1. mysql基本的四条语句(增删改查)

	* 增:

		insert into student (sno,id,sdept) values ('001',1,'计算机系')

	* 删:

		delete from student where sno='020'

		删除表的三种方式

		程度从强到弱
		1、drop  table tb 
		      drop将表格直接删除，没有办法找回
		2、truncate (table) tb
		      删除表中的所有数据，不能与where一起使用
		3、delete from tb (where)
		      删除表中的数据(可制定某一行)

	[具体可查看](https://www.cnblogs.com/shuaiandjun/p/6042600.html)

	* 改:
	
		UPDATE student SET sage=sage+1

	* 查:

		> 选择若干列

			SELECT sno,sname FROM student;

		> 可读性更强 使用as
	
			SELECT sno as 学号,sname as 姓名 from student WHERE sno=015;

		> 通过年龄计算出生年(另外year(data)可获取年份)

			SELECT sno as 学号,'我什么都不做',sname as 姓名,2018-sage as 出生年 from student;

		> 清除重复行()

			SELECT DISTINCT(sage) from student

		> where关系比较

		 > < != <> !> !<

			SELECT * FROM sc WHERE grade<>56

		>  between and 和 not between and

			SELECT * FROM sc WHERE grade BETWEEN 80 and 100
			SELECT * FROM sc WHERE grade NOT BETWEEN 80 and 100
			SELECT * FROM sc WHERE grade>= 80 AND grade <=100

		>  查询计算机或者经济学的学生信息

			SELECT * FROM student WHERE sdept='计算机' or sdept='经济学'

		>  查询不是计算机或者经济学的学生信息
	
			SELECT * FROM student WHERE sdept NOT in ('计算机','经济学')

		> is NULL 和is not null

			SELECT DISTINCT(sno) FROM sc WHERE grade IS NOT NULL

		> like的使用(配合%或者_使用)
		
		查询姓李的同学

			SELECT * FROM student WHERE sname LIKE '李%'

		> 查询叫张X绮的同学


			SELECT * FROM student WHERE sname LIKE '张_绮'

			-- '%a'     //以a结尾的数据
			-- 'a%'     //以a开头的数据
			-- '%a%'    //含有a的数据
			-- '_a_'    //三位且中间字母是a的
			-- '_a'     //两位且结尾字母是a的
			-- 'a_'     //两位且开头字母是a的

		> 排序asc 升序 desc降序

			SELECT * FROM sc WHERE grade is NOT null AND sno LIKE '002' ORDER BY grade ASC
			多次排序用,隔开
			SELECT * FROM student ORDER BY sage desc,sno ASC

		> 聚合函数

		count()计数

			SELECT COUNT(sno) FROM student;

		> 分组聚合 order by 

			SELECT count(grade),sno FROM sc GROUP BY sno;

		> having

		having是在分组聚合之后筛选,where是在分组聚合之前筛选

		> limit 0,1  0表示从哪一行开始,不写默认从第一行开始,1表示取几行

			SELECT cno,avg(grade) as ag from sc GROUP BY cno ORDER BY ag DESC LIMIT 2,1

		> 内置函数

		abs(-2)取绝对值

			 SELECT abs(-2)

		concat(sno,sname,ssex)  将字符串连接在一起

			SELECT CONCAT(sno,sname,ssex)from student
		
		CONCAT_WS("-",sno,sname,ssex)  将字符串用分隔符连接在一起

			SELECT CONCAT_WS("-",sno,sname,ssex)from student

		-- LEFT(s,n)返回字符串s最左边的n个字符

			-- `REPLACE`(str,from_str,to_str)	

			UPDATE student SET ssex=replace(ssex,'男','女')

		- CHAR_LENGTH(str)得到字符个数,LENGTH(str)得到字节个数 比如二狗 两个字符 6个字节

		获取时间

			SELECT CURRENT_DATE();
			2018-08-09
			SELECT CURRENT_TIME();
			11:57:05
			SELECT CURRENT_TIMESTAMP();
			2018-08-09 11:57:20
			SELECT UNIX_TIMESTAMP()
			1533787053
		加密:

			-- 为密码字段加密
			
			UPDATE test set da=sha1(da)

	1. char_length(str):返回str所包含的字符数，一个多字节字符算一个字符
	1. length(str): 返回字符串的字节长度，如utf8中，一个汉字3字节，数字和字母算一个字节
	1. concat(s1, s1, ...): 返回连接参数产生的字符串
	1. concat_ws(x, s1, s2, ...): 使用连接符x连接其他参数产生的字符串
	1. INSERT(str,pos,len,newstr):返回str,其起始于pos，长度为len的子串被newstr取代。
		1. 若pos不在str范围内，则返回原字符串str
		2. 若str中从pos开始的子串不足len,则将从pos开始的剩余字符用newstr取代
		3. 计算pos时从1开始，若pos=3,则从第3个字符开始替换
	1. lower（str)或者lcase(str):
	1. upper(str)或者ucase(str):
	1. left(s,n):返回字符串s最左边n个字符
	1. right(s,n): 返回字符串最右边n个字符
	1. ltrim(s):删除s左侧空格字符
	1. rtrim(s):
	1. TRIM([{BOTH | LEADING | TRAILING} [remstr] FROM] str)或TRIM([remstr FROM] str)：从str中删除remstr, remstr默认为空白字符
	1. REPEAT(str,count)：返回str重复count次得到的新字符串
	1. REPLACE(str,from_str,to_str)： 将str中的from_str全部替换成to_str
	1. SPACE(N):返回长度为N的空白字符串
	1. STRCMP(str1,str2):若str1和str2相同，返回0， 若str1小于str2, 返回-1， 否则返回1.
	1. SUBSTRING(str,pos), SUBSTRING(str FROM pos), 	1. SUBSTRING(str,pos,len), SUBSTRING(str FROM pos FOR len),MID(str,pos,len): 获取特定位置，特定长度的子字符串

			SELECT SUBSTR(sdept,2)  FROM student WHERE sno=019