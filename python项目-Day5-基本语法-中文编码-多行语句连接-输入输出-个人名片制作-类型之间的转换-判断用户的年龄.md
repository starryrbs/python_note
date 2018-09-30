###python项目-Day5

1. pycharm快捷键

	复制当前行ctrl+D

	删除当前行ctrl+x

	注释当前行ctrl+/

	多行注释''' '''

	单行注释#
	
	另起一行shift+enter

2. python编码问题

	使python支持中文
		
	(1). #在文件的头部加上

		
		#-*- coding:utf-8 -*-
		
	
	(2).  #file/setting/editor/file encoding/project-encode:utf-8默认设置编码方式为utf-8
	
3. 多行语句 用连接符\

		a=1+2+\
		3
		print(a)
		
4. python的输入与输出
	
	输入:input()
	
		
		s=input("请输入内容：")
	
	输出:print()
	
		print(s)
	
	变量和字符串同时输出
		
	1. 第一种方式


			age=12
			school="清华"
			print("小明的年龄是",age,'它的学校是：',school)

	2. 第二种方式

			%d数字占位符 ,%s字符串占位符,%f浮点数
			print("小明的年龄是%d,他的学校是%s"%(age,school))

5. demo-个人名片的制作

		print("请问你叫什么名字?")
		name=input()#得到用户输入姓名
		print("请问你的电话号码是:")
		tel=input()#用户输入电话
		print("你是哪个公司的?")
		gongsi=input()#用户输入公司名称
		print("===================")
		print("姓    名:",name)
		print("电    话: %s"%(tel))
		print("公司名称:",gongsi)
		print("===================")

	结果:

		请问你叫什么名字?
		爱丽丝
		请问你的电话号码是:
		132209
		你是哪个公司的?
		华为
		===================
		姓    名: 爱丽丝
		电    话: 132209
		公司名称: 华为
		===================	

6. 变量的赋值

		a=b=c=1
		m,n,s=12,12.5,'python'
		print(m,n,s)

7. 变量类型

	1. int
	2. float
	3. str
	4. bool

8. 类型之间的转换

	float=>int

	n=int(f)#将浮点数的点以及点以后的数全部去掉

	int=>float

	n=int(f)#将int类型转化为float类型,就是在int变量后面加上.0

	str=>int

		s='12'
		print(int(s))#将字符串类型转化为int型

	
9. 判断用户的年龄

		a = input('请输入你的年龄:')
		while True:
		if a.isdigit()==True:#isdigit()如果字符串只包含数字则返回 True 否则返回 False。
		    if int(a)>18:
		        print("你自由了")
		    else:
		        print("在家好好呆着")
		    break
		else:
		    print("你的年龄输入错误,请重新输入一个正确的年龄:")
		    a = input()

	结果:

		请输入你的年龄:hh
		你的年龄输入错误,请重新输入一个正确的年龄:
		12
		在家好好呆着
