##Python项目-Day16-装饰器-设计模式

1. 装饰器(只能给函数使用)
	
	解释:拓展原来函数的一种函数

	目的:在不修改原函数的代码前提下添加新的功能

	* 装饰器的使用

		举例:

			def debug(func):
				def wrapper():
					print("执行了装饰器里的方法")
					func()#这个func叫回调函数
				return wrapper
			@debug
			def show():
				print("执行了show方法")
			show()

			执行步骤: show()->看到show方法上面的debug->执行debug方法,->返回wrapper去执行->执行print->执行func()->func就是show方法->执行结束


	* 装饰器的传参和返回值


			def log(func):
			    from datetime import datetime
			    def wrapper(m,*args):
			        print("当前执行的代码是:",func.__name__)
			        print("添加用户是:",m)
			        dd=datetime.now().strftime('%Y-%m-%d %H-%M-%S')
			        print("执行时间是:",dd)
			        return func(m)
			    return wrapper
			
			@log
			def addUser(user):
			    if user:
			        # 添加用户省略
			        return True
			    else:
			        return False
			res=addUser(' ')
			
			res and print("添加用户成功")

		注意:在addUser()里面加上形参,在wrapper上也要加上形参

	* 多个装饰器

			def A(func):
			    def wrapper(*args):
			        print('a begin.........')
			        func()
			        func()
			        print('a end ........')
			    return wrapper
			
			
			def B(func):
			    def wrapper(*args):
			        print('b begin.........')
			        func()
			        func()
			        print('b end ........')
			    return wrapper
			
			
			def C(func):
			    def wrapper(*args):
			        print('c begin.........')
			        func()
			        print('c end ........')
			    return wrapper
			@A
			@B
			@C
			def show():
			    print("show is running")
			
			
			show()
			
			执行结果:
			a begin.........
			b begin.........
			c begin.........
			show is running
			c end ........
			b end ........
			a end ........

	* python3装饰器

		导入包:

		from functools import wraps

		使用wraps会使代码运行的更快
			
			from functools import wraps
			def log(func):
			    from datetime import datetime
			    wraps(func)
			    def wrapper(m,*args):
			        print("当前执行的代码是:",func.__name__)
			        print("添加用户是:",m)
			        dd=datetime.now().strftime('%Y-%m-%d %H-%M-%S')
			        print("执行时间是:",dd)
			        return func(m)
			    return wrapper
			
			@log
			def addUser(user):
			    if user:
			        # 添加用户省略
			        return True
			    else:
			        return False
			res=addUser(' ')
			
			res and print("添加用户成功")

	* 装饰器传值

			from functools import wraps
			def log(*log_args):
			    def decorated(func):
			        from datetime import datetime
			        @wraps(func)
			        def wrapper(m,*args):
			            print("当前执行的代码是:",log_args[0],func.__name__)
			            print("添加用户是:", m)
			            dd = datetime.now().strftime('%Y-%m-%d %H-%M-%S')
			            print("执行时间是:", dd)
			            return func(m)
			        return wrapper
			    return decorated
			
			@log("a")
			def addUser(user):
			    if user:
			        # 添加用户省略
			        return True
			    else:
			        return False
			res=addUser(' ')
			
			res and print("添加用户成功")

2. 设计模式


	\_\_new__用来声明对象
	
	\_\_init__用来初始化对象

	单例模式的实现:
	
	声明一个为None的类变量__instance
	
	如果创建过对象,这个类变量__instance就会被改变

	以后再创建对象,只会返回第一次创建的对象,也就是__instance

		class Person(object):
		    __instance=None
		    def __new__(cls, *args, **kwargs):
		        print("我在生产对象")
		        if not cls.__instance:
		            cls.__instance=object.__new__(cls)
		        return cls.__instance
		    def __init__(self,id,name):
		        super(Person,self).__init__()
		        self.id = id
		        self.name = name

			p1=Person('001','python')
			p2 = Person('002','python')
			p3 = Person('003','python')
			
			print(p1.id)
			print(p2.id)
			print(p3.id)
			
			
			p3和p4本质上都是p1,只不过属性都是p3(最后一次创建的对象的属性)