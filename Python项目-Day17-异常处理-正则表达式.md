##Python项目-Day17-异常处理-正则表达式

1. 异常处理

	用来处理程序执行过程中可能出现的导致程序无法正常执行的问题

	* 异常的分类:

		* 程序遇到逻辑或算法错误
		* 运行过程中计算机错误:内存不够或者io错误

	* 异常的步骤:

		* 异常产生,检查到错误且解释器认为是异常,抛出异常
	
	* 异常处理的格式:

			try
				语句
			except Exception as ex:
				print(ex)
			else:#程序正常执行会执行到else后的语句
				pass
			finally:#不管程序有没有出错,肯定会执行finally后面的语句
				pass

2. 常见的异常


	* AttributeError 试图访问一个对象没有的属性,比如foo.x,但是foo没有属性x

			class Person(object):
			    def __init__(self):
			        pass
			p1=Person()
			try:
			    print(p1.name)
			except AttributeError  as ex:
			    print(ex)
			
			#报错:'Person' object has no attribute 'name'

	* IOError 输入/输出异常:基本上是无法打开文件

			try:
			    fr = open('data.txt', 'r')
			except IOError as ex:
			    print(ex)

			#报错:[Errno 2] No such file or directory: 'data.txt'
	
	* ImportError 无法引入模块和包;基本上是路径问题或名称错误,基本上很少出现
	* IndexError 下标索引超出序列边界,比如当x只有三个元素,却试图访问x[5]

			a=[1,2,3]
			
			try:
			    print(a[4])
			except IndexError as ex:
			    print(ex)
			
			#报错:list index out of range

	* KeyError试图访问字典里不存在的键
	* KeyboardInterrupt Ctrl+C被按下
	* NameError 尝试访问一个没有声明的变量
	
			try:
			    print(a)
			except NameError as ex:
			    print(ex)

			#报错:name 'a' is not defined
	* SyntaxError Python代码非法，代码不能编译
	* TypeError 传入对象类型与要求的不符合
	
			try:
			    i = '1'
			    j = 2
			    print(i + j)
			except TypeError as ex:
			    print(ex)

			#报错:must be str, not int

	* UnboundLocalError试图访问一个还未被设置的局部变量,基本上是由于另有一个同名的全局变量,导致你以为正在访问它
	* ValueError传入无效的参数
	
			try:
			    print(int('s'))
			except ValueError as ex:
			    print(ex)

			#报错:invalid literal for int() with base 10: 's'
	* Exception所有常规异常它都能捕捉到
	* BaseException所有异常的基类,补货所有异常

3. raise主动触发异常
	
	我们可以使用raise语句自己触发异常

		try:
		    num=13
		    if num%2==0:
		        print(num)
		    else:
		        raise TypeError('num 不是偶数')#抛出异常
		except (NameError,TypeError) as ex:
		    print(type(ex))
		else:
		    pass
		finally:
		    pass

4. 自定义异常

		class MyException(Exception):
			def __index__(self,arg):
				self.args=arg
		
		try:
			raise MyException('OH')
		except MyException as ex:
			print(ex)
		
		#报错:OH

5. 正则表达式

		#  . 匹配除换行符\n之外的所有字符
		#  * 0次或多次
		#  + 一次或多次
		#  ? 0次或1次
		# \ 表示转义字符
		# \t 相当于按一个tab键
		# | 表示或者
		# []表示或者 [01234567]=>[0-7]=>0|1|2..|7
		# {}表示匹配前面的字符 ,例如 4{2,4}匹配4  2到4次
		# regex=r'^h\d+o$'
		# () 用来分组
		# [^] 中括号之内的^表示非
		# \s 空白字符
		# \s 非空白字符
		# \w 匹配数字字母下划线

	\ 的作用:

		* 反斜杠去除后面字符的特殊功能
		* 和后面的普通字符实现特殊功能

	 预定义字符集

		* \d 数字:[0-9]
		* \D 非数字:[^\d]
		* \s 匹配任何空白字符:[ ]
		* \S 非空白字符
		* \w匹配包括下划线在内的任何字符:[A-Za-z0-9]
		* \W匹配非字母字符,即匹配特殊字符
		* \A 仅匹配字符串开头
		* \Z 仅匹配字符串结尾
		* \b 在边界匹配单词例如， 'er\b' 可以匹配"never" 中的 'er'，但不能匹配 "verb" 中的 'er'。
		* \B 在非边界匹配单词

3 re模块中常用的函数

1. compile()函数

	可以把那些常用的正则表达式编译成正则表达式对象,这样可以提高一点效率

2. match()

	决定re是否在字符串刚开始的位置匹配,当pattern结束时若string还有剩余字符,仍然视为成功.想要全部匹配,就要正则表达式末尾加上$

		import re
		# regex = r'^(ht)+.+o$'
		regex = r'^李.*琴$'
		
		my_str = '李琴'
		
		result = re.match(regex, my_str)
		
		print(result)

		#没有（）就是匹配模式，有了（）就是分组查找模式

3. search()

	re.search()函数会在字符串内查找模式匹配,只要找到第一个匹配然后返回,如果字符串没有匹配,则返回None

4. findall

	re.findall遍历匹配,可以获取字符串中所有匹配的字符串,返回一个列表

5. split()

	按照能够匹配的字符串将string分割后返回到列表
		import re
		
		str='ne-ve-r:s:s'
		
		regex=r'[-:]'
		
		res=re.split(regex,str)

		print(res)


6. 贪婪模式与非贪婪模式

		举例： 
		
		源字符串：aa<div>test1</div>bb<div>test2</div>cc 
		
		正则表达式一：<div>.*</div> 
		
		匹配结果一：<div>test1</div>bb<div>test2</div> 
		
		正则表达式二：<div>.*?</div> 
		
		匹配结果二：<div>test1</div>（这里指的是一次匹配结果，所以没包括<div>test2</div>）

7. re.match与re.search与re.findall的区别：

	re.match只匹配字符串的开始，如果字符串开始不符合正则表达式，
	则匹配失败，函数返回None；而re.search匹配整个字符串，直到找到一个匹配。


	    a=re.search('[\d]',"abc33").group()
	    print(a)
	    p=re.match('[\d]',"abc33")
	    print(p)
	    b=re.findall('[\d]',"abc33")
	    print(b)
	    执行结果：
	    3
	    None
	    ['3', '3']