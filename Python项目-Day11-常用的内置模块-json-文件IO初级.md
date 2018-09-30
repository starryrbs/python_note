##Python项目-Day11
1. datetime和time

	* 获取当前时间

			date_now=datetime.now()
			#2018-07-25 18:45:15.875485

	* 格式化输出时间

	

			current_time_format=current_time.strftime("%Y-%m-%d")
			#2018-07-25

			current_time_format=datetime.strftime(current_time,"%Y-%m-%d")
			#2018-07-25

	格式参数：
	
	%Y 带世纪部分的十制年份
	
	%m 十进制表示的月份
	
	%d 十进制表示的每月的第几天
	
	%H 24小时制的小时
	
	%M 十时制表示的分钟数
	
	%S 十进制的秒数
	
	%c  标准时间，如：04/25/17 14:35:14  类似于这种形式

	* 获取昨天或者明天的时间

			yestoday=current_time+timedelta(days=1)


	* 时间格式的相互转化

		1. 字符串转datetime
		
				string = '2017/11/10 02:29:58'.replace('/','-') 
				# string = '2017-11-10 02:29:58'

				string = '2017-11-10 02:29:58'
				time1=datetime.strptime(string,"%Y-%m-%d %H:%M:%S")

		2. datetime转化为string

				time1_str = datetime.strftime(time1, '%Y-%m-%d %H:%M:%S')
				print(type(time1_str))
				print(time1_str)

		3. 时间戳转时间对象

				time2=time.time()
				print(time2)
				time2_s=datetime.fromtimestamp(time2)
				print(time2_s)

		4. 时间对象转为时间戳
	
				timeStamp = int(time.mktime(date_now.timetuple()))
				print(timeStamp)
		 	

		5. 计算时间差
		    
			    days=(date_now-time1).days
			    seconds=(date_now-time1).seconds
			    print(seconds)


2. json

	>JSON (JavaScript Object Notation) 是一种轻量级的数据交换格式。它基于ECMAScript的一个子集。

		import json
		#导入json
	
		# json.dumps	    将Python 字典类型转换为 JSON 对象
		# json.loads	    将 JSON 对象转换为 Python 字典


3. 文件IO

		file object = open(file_name [, access_mode][, buffering])
		fr=open('user.txt','w+',encoding="utf-8")

	![](https://i.imgur.com/rw65igP.png)

