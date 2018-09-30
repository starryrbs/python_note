##python字符串

1. 字符串切片的用法

	*  切片工具的格式
	
		s1[a:b:c]
		a表示起始位置,b表示终止位置,c表示步长,隔多少个切 例如2,-1..默认为1

	*  顺序切片
		
		表示从1截取到5,包括1,不包括5

			s1='i love python'
			print(s1[1:5])
		
		表示切片到最后

			print(s1[11:])
		表示从-2往最后一位截取,最后一位为-1

			print(s1[-2:])
		表示从-6位往-2位截取
			print(s1[-6:-2])


	* 逆序切片
	
		表示从第7位往第3位逆序切
		
			print(s1[7:3:-1])#结果为p ev

	* 切片工具的应用

		
		1. 字符串反转:
			
				s2='abcdefghijklm'
				print(s2[::-1])
			> 结果为:
		
				mlkjihgfedcba

		2. 截取第一个字符

				print(s2[0:1])

		3. 截取最后一个字符

				print(s2[-1:])

		4. 所有
		
				print(s2[:])

		5. 奇数个或者偶数个

				print(s2[::2])
				print(s2[1::2])

		6. 反向切

				print(s2[7:3:-1])

2. 判断用户名全是小写字母
		
		user_id = "a1dmin"
		flag = True
		for i in user_id:
			if not ('a' <= i <= 'z'):
			#如果i不在a到z的范围里,输出no ok
				flag = False
				print("no ok")
				break
		#如果执行到最后,都没有break,执行ok,即正常走完循环执行这句话
		else:
			print("ok")

3. 字符串连接符

	+号表示字符串的连接,*号表示字符串的重复

		s1 = 'py'
		s2 = 'thon'
		s3 = s1 + s2
	
		s3=s1*2

4. 字符串的格式输出

		u_name = 'python'
		u_age = 20

		1.转义字符形式:
		print('i am %s ,and i am %d' % (u_name, u_age))
		print('i am %8s ,and i am %d' % (u_name, u_age))#8s右对齐,如果是-8s就是左对齐,长度为8

		2.format形式:
		print('i am {0} ,and i am {1}' .format(u_name, u_age))
		print('i am {1} ,and i am {0}' .format(u_name, u_age))
		print('i am {1} ,and i am {0:20s}' .format(u_name, u_age))#20s表示字符串长度为20
		print('i am {nn} ,and i am {aa}' .format(nn=u_name, aa=u_age))


5. 一些内部函数
		
	* count函数
	
			s1 = 'hello world hello china'
			c1 =s1.count('hello')
			print(c1)
		小应用:字符串去重
			
			ss1=''
			for i in  s1:
				if ss1.count(i)==0:#如果ss1字符串中没有i,就将i加入,如果已经有了,就不加入ss1字符串 
					ss1=ss1+i
	* find函数

			i=s1.find('h')#查找字符串,找不到返回-1,找到返回要查询的字符串'h'所在的位置

	* replace函数

			s2=s1.replace('hello','hi',2)#替换,不改变原来的字符串,可以赋值给另一个变量
			# 第一个参数为要被替换的字符串,第二个参数为替换后的字符串,第三个参数为替换几次

	* split函数

			date='2018-3-1'
			times=date.split('-')#根据特定的分隔符去截断

	* join函数
		
			s2='python'
			s3='-'#在s2中每个元素中加入s3
			s4=s3.join(s2)
			print(s4)

	* isdigit函数

		>如果字符串中只有数字返回True,否则返回False

	* isalpha函数
		
		>如果字符串中只有字母返回True,否则返回False

	* isalnum函数

		>如果字符串中只有数字和字母返回True,否则返回False
		
6. 编码问题

	* encode	将字符串变为字节码

			s="你好 python"
			print(s)
			byte_s = s.encode('utf-8')

	* decode	将字节码变为字符串

			utf_s=byte_s.decode('utf-8')
			print(utf_s)

7. list(相当于**数组**)

	* list的定义
		
			arr3 = [1, 12.3, 'python']

	* 数组是可以改变元素的,而字符串不行
	
			arr3[2] = 'java'

	* list也支持切片
	*  分页的实现
	
			books=['aaaa','bbbbb','ccccccc','dddddd','eeeeeeee']
			page_count = 2 #每页有多少本书
			page_index = 1 #页码
			books_index = books[(page_index-1)*page_count:page_index*page_count]
			
		总页数:
			

			m=len(books)/page_count
			n=len(books)//page_count
			pages = n if m==n else n+1#总页数,如果m=2代表page_count和len(books)是整数倍,总页数为n,反之不是,总页数向上取整,也就是n+1

8. 其他的几个函数

	* index判断字符串"banana"在fruits中的位置

			fruits=['orange','apple','pear','banana','apple']
			print(fruits.index('banana'))#
		
		**注意没找到会出错**

	* reverse反转列表,改变了原来的列表

			fruits.reverse()#反转数组,改变了数组
			f=fruits[::-1]#反转数组,不改变原数组
	
	* sort()排序,升序排列

			fruits.sort()#排序,升序排列
			print(fruits)

9. 浅拷贝与深拷贝的问题

		f=fruits
		f[0]='water'
		print(fruits)
		
		结果为:
		['water', 'apple', 'banana', 'orange', 'pear']


		f=fruits[:]
		f[0]='water'
		print(f)
		print(fruits)
		结果为:
		['apple', 'apple', 'banana', 'orange', 'pear']

10. 密码判断

	要求:1.密码为全数字2.密码位数大于6
		
		def judgePsd(psd):
		
			for i in range(len(psd)):
				if not (('0' <= psd[i] <= '9') and (len(psd) > 6)):
				    print("这个密码不行啊")
				    break
			# if (i + 1) == len(psd):
			else:
				print("这个密码可以")
		judgePsd("542125d6")

11. 找出列表的最大值和最小值以及它们所在的位置

		arr=[1,2,21,3,432,54,12]
		max_num =arr[0]#数组的最大值
		min_num =arr[0]#数组的最小值
		max_index=0#数组最大值的下标
		min_index=0#数组最小值的下标
		for i in range(len(arr)):
		    if max_num<arr[i]:#判断是否与当前数组值是否比max_num小,如果小,当前数组值变为max_num,当前值的序号为max_index
		        max_num=arr[i]
		        max_index=i
		    if min_num>arr[i]:#与上面相似
		        min_num=arr[i]
		        min_index=i
		print("这个数组的最大值是:{0},它的位置是:{1},这个数组的最小值是{2},它的位置是:{3}".format(max_num,max_index,min_num,min_index))


##补充:

1. 字典排序
	可以根据key或者value

		from collections import OrderedDict
		dic={
		    'z':1,
		    'i':2,
		    'x':0
		}
		print(dic.items())
		#使用sorted方法进行排序,第一个参数为字典的items,关键字参数key是一个lambda函数x[0]是拿key比较,
		dic2=sorted(dic.items(),key=lambda x:x[1])

		#dic3=OrderedDict(dic2)
		dic3=dict(dic2)
		print(dic3['x'])
[OrderedDict与dict的区别](https://www.cnblogs.com/gide/p/6370082.html)

