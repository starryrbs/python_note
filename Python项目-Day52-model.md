##Python项目-Day52-model
1. 	模型是有关数据的单一，明确的信息来源。它包含您要存储的数据的基本字段和行为。通常，每个模型都映射到单个数据库表。

	基础：

	* 每个模型都是一个子类的Python类 django.db.models.Model。
	* 模型的每个属性代表一个数据库字段。
2. ORM

	关系对象映射（Object Relational Mapping，简称ORM）。
	
	生成表结构(默认数据库为sqllite)

	1. 在app的models.py文件中,创建类

			from django.db import models

			# Create your models here.
			class userinfo(models.Model):
			    # 自动创建一个id列，id为主键、自增长
			    telephone = models.CharField(max_length=30)
			    password = models.CharField(max_length=64)
			    email = models.EmailField()
			    # memo = models.TextField()

		更多字段


			1、models.AutoField　　自增列= int(11)
			　　如果没有的话，默认会生成一个名称为 id 的列，如果要显示的自定义一个自增列，必须将给列设置为主键 primary_key=True。
			2、models.CharField　　字符串字段
			　　必须 max_length 参数
			3、models.BooleanField　　布尔类型=tinyint(1)
			　　不能为空，Blank=True
			4、models.ComaSeparatedIntegerField　　用逗号分割的数字=varchar
			　　继承CharField，所以必须 max_lenght 参数
			5、models.DateField　　日期类型 date
			　　对于参数，auto_now =True则每次更新都会更新这个时间；auto_now_add 则只是第一次创建添加，之后的更新不再改变。
			6、models.DateTimeField　　日期类型 datetime
			　　同DateField的参数
			7、models.Decimal　　十进制小数类型= decimal
			　　必须指定整数位max_digits和小数位decimal_places
			8、models.EmailField　　字符串类型（正则表达式邮箱）=varchar
			　　对字符串进行正则表达式
			9、models.FloatField　　浮点类型= double
			10、models.IntegerField　　整形
			11、models.BigIntegerField　　长整形
			　　integer_field_ranges ={
			　　　　'SmallIntegerField':(-32768,32767),
			　　　　'IntegerField':(-2147483648,2147483647),
			　　　　'BigIntegerField':(-9223372036854775808,9223372036854775807),
			　　　　'PositiveSmallIntegerField':(0,32767),
			　　　　'PositiveIntegerField':(0,2147483647),
			　　}
			12、models.IPAddressField　　字符串类型（ip4正则表达式）
			13、models.GenericIPAddressField　　字符串类型（ip4和ip6是可选的）
			　　参数protocol可以是：both、ipv4、ipv6
			　　验证时，会根据设置报错
			14、models.NullBooleanField　　允许为空的布尔类型
			15、models.PositiveIntegerFiel　　正Integer
			16、models.PositiveSmallIntegerField　　正smallInteger
			17、models.SlugField　　减号、下划线、字母、数字
			18、models.SmallIntegerField　　数字
			　　数据库中的字段有：tinyint、smallint、int、bigint
			19、models.TextField　　字符串=longtext
			20、models.TimeField　　时间 HH:MM[:ss[.uuuuuu]]
			21、models.URLField　　字符串，地址正则表达式
			22、models.BinaryField　　二进制
			23、models.ImageField图片
			24、models.FilePathField文件
	2. 注册app,在settings.py中

			INSTALLED_APPS = [
			'jobapp'   #注意这里加上的是模块名称
			]
	3. 在settings.py中修改数据库配置

			DATABASES = {
					    'default': {
					    'ENGINE': 'django.db.backends.mysql',
					    'NAME':'jobapp',
					    'USER': 'root',
					    'PASSWORD': '',
					    'HOST': '127.0.0.1',
					    'PORT': '3306',
					    }
					}

		**注意**
		
		由于Django内部连接MySQL时使用的是MySQLdb模块，而python3中还无此模块，所以需要使用pymysql来代替
  
		如下设置放置的与project同名的配置的 __init__.py文件中
  
			import pymysql
			pymysql.install_as_MySQLdb()　
			
		**所以啊，要先安装：pip install pymysql**

	3. 生成迁移 

			python manage.py makemigrations

		该模块目录下必须有一个文件夹：migrations（如果没有就新键）

		该模块目录下必须有一个文件夹：migrations（如果没有就新键）
	4. 生成数据表

			python manage.py migrate	

		默认的表名

		job.userinfo	#app.类名

	##可能出现的问题:

	1. mysql版本不对

		在django2.1版本中不支持5.5以下
	2. 修改表的字段

		直接修改models中的类
	
		重新生成迁移

			python manage.py makemigrations

		执行迁移

			python manage.py migrate

	1. **删除数据表重新生成，解决 python No migrations to apply 无法生成表**

		第一步：
			
			删除该app名字下的migrations文件。

		第二步：
			
			进入数据库，找到django_migrations的表，删除该app名字的所有记录。
			delete from django_migrations;
			
			或者删除数据库重新新建

		第三部:
			
			python manage.py makemigrations

			python manage.py migrate

3. 访问数据库

	1. 增加数据

			from . import models

			#1
			uu=models.userinfo.objects.create(
						        telephone="root",
						        password="123456"
						    )

			#2
			uu=models.userinfo.objects.create(**dict)

			#3
			user=models.userinfo(telephone="admin",password="6666")
    			user.save()
			#4
			dic={"telephone":"alex","password":"888"}

    			models.userinfo(**dic).save() #当然了，				models.userinfo.objects.create（**dic）也可以
   		**force_update和force_insert**

		这两个参数一般较少用到，因为save()之后django执行的是UPDATE或者INSERT这两条SQL语句的哪一条，遵循如下算法：
		
		1.如果这个对象已经有主键而且主键的值是True的（即不是None或者空字符串等），就执行UPDATE。
		
		2.如果没有主键或者这条save()不会update任何字段,那么它就INSERT。
		
		只有在某些特定情况下，需要强制save()执行INSERT或UPDATE时才会使force_update=True或force_insert=True（比如我要求能UPDATE就UPDATE，不能我也不取INSERT，那么我就把这个force_update参数设置为True）。

	2. 关于自增长id

			class userinfo(models.Model):
				id = models.AutoField()
				#创建一个自增长列id,自增长必须是主键

			

	3. 删除数据


			affect_rows=models.userinfo.objects.all().delete()

			models.UserInfo.objects.filter(user='yangmv').delete()

	4. 更新数据

			affect_rows=models.userinfo.objects.all().update(password="666666")

			affect_rows=models.userinfo.objects.filter(id='4').update(password="666666")

			obj = models.UserInfo.objects.get(user='yangmv')
			obj.pwd = '520'
			obj.save()

	5. 查询数据

		2. 条件查询

			1. 单条件

			
					users=models.userinfo.objects.filter(telephone='root')
					#select * from userinfo where telephone='root'
	    			for user in users:
	        			print(user.id,user.telephone,user.password)


			2. and

				逗号表示and

					users=models.userinfo.objects.filter(telephone='root',password='123)

					models.UserInfo.objects.all()
					models.UserInfo.objects.all().values('user')    #只取user列
					models.UserInfo.objects.all().values_list('id','user')    #取出id和user列，并生成一个列表
					models.UserInfo.objects.get(id=1)
					models.UserInfo.objects.get(user='yangmv')