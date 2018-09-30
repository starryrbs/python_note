##Python-Day10
1. python函数

	* 函数的定义

			def hello() :
			   print("Hello World!")

2. 参数传递

	可更改(mutable)与不可更改(immutable)对象

	>在 python 中，strings, tuples, 和 numbers 是不可更改的对象，而 list,dict 等则是可以修改的对象。

	* python传不可变对象实例

			def ChangeInt( a ):
			    a = 10
			 
			b = 2
			ChangeInt(b)
			print( b ) # 结果是 2
	>number型是不可变对象,所以b并未改变

	* 传可变对象实例

			def changeme( mylist ):
			   "修改传入的列表"
			   mylist.append([1,2,3,4])
			   print ("函数内取值: ", mylist)
			   return
			 
			# 调用changeme函数
			mylist = [10,20,30]
			changeme( mylist )
			print ("函数外取值: ", mylist)
	>list的是可变对象,在函数中已经改变了mylist的值

3. 函数的参数
	python中函数的参数类型有必要参数,不定长参数,默认参数,关键字参数,命名关键字参数

	* 必要参数(在函数调用时必须加上,否则报错)

			def printme( str ):
			   "打印任何传入的字符串"
			   print (str)
			   return
			 
			#调用printme函数
			printme()

		>这里的printme必须加上str参数

	* 不定长参数(不确定参数有多少个时,可以用不定长参数,格式就是*vartuple)

			def printinfo( arg1, *vartuple ):
			   "打印任何传入的参数"
			   print ("输出: ")
			   print (arg1)
			   print (vartuple)
			 
			# 调用printinfo 函数
			printinfo( 70, 60, 50 )

	* 默认参数(在没有给这个参数赋值时,这个参数的值会是默认值)

			def printinfo( name, age = 35 ):
			   "打印任何传入的字符串"
			   print ("名字: ", name)
			   print ("年龄: ", age)
			   return
			 
			#调用printinfo函数
			printinfo( age=50, name="runoob" )
			print ("------------------------")
			printinfo( name="runoob" )

			输出结果:
			名字:  runoob
			年龄:  50
			------------------------
			名字:  runoob
			年龄:  35

	* 关键字参数(**other)用的地方不是很多
		
		其中args是不定长参数,other是		

			def add(m,n,*args,**other):
			    res=int(m)+int(n)
			    for k,v in other.items():
			        print(k,v)
			    print(other)
			    if args:
			        for i in args:
			            res += int(i)
			    return res
			kw={'length':'12'}
			print(add(3,4,5,**kw))

4. 匿名函数

	python可以使用lambda来创建匿名函数

	* lambda 只是一个表达式，函数体比 def 简单很多。
	
	* lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。
	
	* lambda 函数拥有自己的命名空间，且不能访问自己参数列表之外或全局命名空间里的参数。
	
	* 目的是调用小函数时不占用栈内存从而增加运行效率。

			arr=[i for i in range(10)]
			arr2=map(lambda  x:x**2 if x%2==0 else x,arr)
			print(list(arr2))

			其中lambda  x:x**2 if x%2==0 else x就是一个匿名函数,如果x求余2等于0,x就等于x的2次方,否则x不变

			map()函数:第一个参数 function 以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的新列表

			map格式:map(function, iterable, ...)

5. 变量

	* 函数**访问**变量的规则(注意是访问不是修改变量):1.查找函数内部->查找外部函数->全局

	* 函数内部想要编辑全局变量必须声明:

		global a
	
	声明全局变量的弊端就是函数调用完不会关闭,因为其内部有一个全局变量,因此有时候可以先将全局变量的值取出来给b变量,在b上修改

6. 登录注册的实现

	要求:所有功能必须封装起来

		# 注册->查找该用户是否存在->
		# 登录->查找该用户是否存在
		view_index = '''
		       ====================
		           欢迎访问京西购物
		           1.登录
		           2.注册
		           3.退出
		       ====================
		       一定要输入数字才能运行
		       一定要输入数字才能运行
		       一定要输入数字才能运行
		
		   '''
		
		isLogin=False
		# def test():
		#     print(1,users)
		#     isLogin=True
		#     users.append()
		#     print(2,users)
		# test()
		# print(users)
		# print(isLogin)
		
		#登录功能
		def login(id,pwd):
		    global isLogin
		    print("请登录")
		    uu=get_user_by_id(id)
		    if uu:
		        if uu['user_password']==ercryption(pwd):
		            print('登录成功')
		            isLogin=True
		        else:
		            print("用户名或者密码错误")
		    else:
		        print("该用户不存在")
		# 注册功能
		def register(id,pwd,pwd_confirm):
		    if(pwd==pwd_confirm):
		        if get_user_by_id(id):
		            print("该用户已存在")
		        else:
		            user={}
		            user['id']='0012'
		            user['user_name']=id
		            user['user_password']=ercryption(pwd_confirm)
		            user['birthday']='1970-1-1'
		            # 注册语句
		            fileOperation(True,user)
		#             注册成功
		#             print(users)
		# 判断用户是否存在
		def get_user_by_id(id):
		    # for user in users:
		    #     if user['user_name']==id:
		    #         return user
		    # else:
		    #     return None
		#     定义一个数组取到文件中的值
		    users=fileOperation(False)
		    print("users是",users)
		    for user in users:
		        # user从users数组中取出来是一个str类型,要将其转化成字典类型
		        user=eval(user)
		        print(user["id"])
		        if user['user_name']==id:
		            return user
		    else:
		        return None
		
		#获取输入数据
		def get_datas():
		    id = input('请输入用户名\n')
		    pwd = input('请输入用户密码\n')
		    return id, pwd
		# 密码输入
		def get_threedatas():
		    id = input('请输入用户名\n')
		    pwd = input('请输入用户密码\n')
		    pwd_confirm = input('请输入用户密码\n')
		    return id, pwd,pwd_confirm
		# 加密算法
		def ercryption(s):
		    start_s=list(s)
		    s = list(s)
		    result=[]
		    if s:
		        length=len(s)
		        for item in range(length):
		            print(ord(s[item])+2)
		            result.append(chr(ord(s[item])+2))
		            result.append(start_s[item])
		            print(result)
		            item+=1
		            length+=1
		
		    return result
		# 将数据写入和读取文件的方法,True代表写入,False代表读取
		def fileOperation(model,*user):
		
		    if model:
		        fr = open('a.txt', 'a')
		        user="\n"+str(user[0])
		        fr.write(user)
		        print("成功写入")
		
		    else:
		        # 定义一个数组,来接收数据
		        strArr=[]
		        with open('a.txt', 'r+') as fr:
		            strArr=fr.readlines()
		            print("test读取到的数据:",strArr)
		        for i in range(len(strArr)):
		            strArr[i]=strArr[i].rstrip("\n")
		        return strArr
		print(fileOperation(False,{"aa":"112"}))
		# 程序入口方法
		
		
		def main():
		    print(view_index)
		    index =int(input("请选择\n"))
		
		    if index==1:
		        user_id, user_password = get_datas()
		        login(user_id,user_password)
		        print()
		    if index == 2:
		        user_id, user_password, user_password_confirm = get_threedatas()
		        register(user_id, user_password, user_password_confirm)
		
		main()
		
		
