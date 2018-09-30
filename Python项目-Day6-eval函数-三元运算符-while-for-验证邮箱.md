###python运算符
1. eval函数
	
		
		rex='12+3.5'
		result=eval(rex)#去引号,执行字符串里的语句
		print(result)
	
2. float保留几位小数和四舍五入

		f=3.84212
		
		f_f=float('%.2f'%f)#保留几位小数,四舍五入
		
		f_f_f=round(f,2)#四舍五入

3. 计算时间,输出格式为  时:分:秒

		sec=10000
		
		hour=sec//(60*60)#小于等于9
		hour=str(hour) if hour>9 else '0'+str(hour)
		# 数字大于9正常输出,数字小于等于9前面加上0
		minute=sec%(60*60)/60
		second=sec%60
		
		print("%d:%d:%d"%(hour,minute,second))

4. 运算符

	* 赋值运算符

			a,b,c,d='spam'   #a=s,b=p,c=a,d=m
			
			x,*y,z='spam'   #x=s   y=p,a  z=m

			x,*y='spam'  #取首位字符 x=s y=pam

			*x,y='spam'  #取末尾字符 x=spa y=m

	* 算术运算符

		// 	%   **

			# print(int(m))#去掉小数位
			# print(round(m))#四舍五入
			# print(z//1)#可以用z//1的形式完成向小取整

			print(3**2)#幂运算

	* 关系运算符

			# a=3
			# b='4'
			# print(a>b)#字符串比较两边类型要想等

5. True和False,None

		#整数:0是False 非0就是True
		# 字符串:空字符串就是False,非空就是True

	默认的用法

		n=''
		name=n.strip() or 'python'#默认值的用法
		print(name)
		
	None是一个特殊的常量。

	None和False不同。
	
	None不是0。
	
	None不是空字符串。
	
	None和任何其他的数据类型比较永远返回False。
	
	None有自己的数据类型NoneType。
	
	你可以将None复制给任何变量，但是你不能创建其他NoneType对象。

6. in的使用

		name="python"
		res='pys'  in name#判断前面的字符串是否在后面的字符串当中,结果为True或者False
		print(res)#a in b 和 a not in b
		num=[1,2,3]
		print(1 in num)

	判断邮箱是否正确

		email=''
		
		if email and ('@' in email) and ('.' in email):
		print("is email")
		else:
		print('not is email')

7. is与==的区别

		a=12
		b=12.0
		
		print(a is b)#内容类型都相等
		print(a == b)#判断内容是否相等

8. if的使用

		# # 注意:1.条件外面没有括号,2.以冒号结尾3.语句要缩进
		# if 条件:
		#     # 条件满足时,执行的代码
		# else:
		#     # 条件不满足时,执行的代码

	小示例:

		# num=input("请输入周几?")
		#
		# if num=="1" or num=="2":
		#     print("旅游")
		# elif num=="3" or num=="4" or num=="5":
		#     print("学习")
		# # print(num=="3");
		# else:
		#     print("睡觉")

	一个if只能有一个else,可以有多个elif

9. 三元运算符

		x=1
		a=True if x>0 else False
		print(a)

10. while的使用

		#1.循环变量初始化
		i=0
		# 2.循环条件
		while i<10000:
		# 3.循环体
		print("i am sorry")
		# 改变循环变量的值
		# time.sleep(1)
		i+=1
		else:
		print(i)

11. for循环的使用

		for i in range(100):
		if i%5==0:
		    if i%10==0:
		        continue
		    print(i)


		for i in range(0,100,2):
		     # range(起始值,终止值,步长(每一次循环i加多少))
		     print(i)
