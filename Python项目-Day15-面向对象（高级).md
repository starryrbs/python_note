##Python项目-Day15-面向对象（高级）

1. 动态为**对象**绑定方法

		from types import MethodType
		class Person:
			pass
		def displayMe(self):
			print("my genderis:",self.gender)
		#给一个实例绑定的方法，对另一个实例是不起作用的：
		p1.displayMe=MethodType(displayMe,p1)
		p1.displayMe()

2. 动态为**类**增加属性和方法

		Person.gender='male'
		def displayMe(self):
			print('my genders:',self.gender)
		Person.displayMe=displayMe

3. 使用__slots__限制实例的属性，比如，只允许对Student实例添加name和age属性。
	
		class Person:
			__slots=['age','name']
		
		p1=Person()
		print(dir(p1))
		#这是看到p1对象里已经存在name和age属性了
		p1.gender='female'
		#这里会报错

4. 删除属性

		Person.nation='china'
		p1.gender='male'
		
		del p1.gender
		
		del p1.nation #error nation是属于类的，不可以通过对象删除
		
		del Person.nation
		
		del p1.age

5. 利用动态函数绑定

		setattr(ee2,'age',8)
	
		getattr(ee1,'age')
	
		hasattr(ee1,'age')
	
		delattr(ee1,'age')

6. 私有属性

	1. _xx以单下划线开头表示的是protected类型的变量.即保护型变量
	2. \_\_xx双下划线开头的是私有类型的变量.只允许这个类内部进行访问,类外部不能访问.类内部可以写一个方法调用私有变量,然后类外部就可以访问这个方法进行访问该私有变量了
	3. \_\_xx__定义的是特例方法.  如\_\_slots__限制属性,重写__str__方法等等
		
		
			class pub():
				# protected类型的变量和方法 在类的实例中可以获取和调用
			    _name = 'protected类型的变量'
			    __info = '私有类型的变量'
			    def _func(self):
			        print("这是一个protected类型的方法")
			    def __func2(self):
			        print('这是一个私有类型的方法')
			    # 如果想要在实例中获取到类的私有类形变量可以通过在类中声明普通方法，返回私有类形变量的方式获取
			    def get(self):
			        return(self.__info)
			        
			p=pub()
			p.__info # error 因为__info是私有变量只有在类内部才可见，所以要用内部方法

7. python内置类属性

		__dict__ : 类的属性（包含一个字典，由类的数据属性组成）
	
		__doc__ :类的文档字符串
	
		__module__: 类定义所在的模块（类的全名是'__main__.className'，如果类位于一个导入模块mymod中，那么className.__module__ 等于 mymod）
	
		__bases__ : 类的所有父类构成元素（包含了一个由所有父类组成的元组

8. 只读属性

	@ property 作用就是采用访问属性的方式访问函数。
	
		class Car:
		    __wheels=4
		
		    @property
		    def wheels(self):
		        return self.__wheels

	@property可以把方法变为属性，
	
		class Car:
		    __wheels=4
		    __voice='didi'
		    def __init__(self,color):
		        self.color=color
		        self.speed=80
		    @property
		    def run(self):
		        print('i can run %d speed'%self.speed)
		
		    @run.setter
		    def run(self,wh):
		        self.speed=wh
		
		
		
		car1=Car('blue')
		
		print(car1.color)
		car1.run=120
		car1.run
		
	**这个属性是不可以通过del car1.run 来删除的。因为他本来就不是一个属性**
		
		@run.deleter
	    def run(self):
	        del self.speed
	        print("你的车轮已经被拆除...")
9. 静态方法

	普通的方法，可以在实例化后直接调用，并且在方法里可以通过self.调用实例变量或类变量，但静态方法是不可以访问实例变量或类变量的，一个不能访问实例变量和类变量的方法，其实相当于跟类本身已经没什么关系了，它与类唯一的关联就是需要通过类名来调用这个方法。
	
		class Car:
	    __wheels=4
	    __voice='didi'
	    def __init__(self,color):
	        self.color=color
	    @property
	    def wheels(self):
	        return self.__wheels
	
	  	#静态方法在类中也不需要传入 self参数
	    @staticmethod
	    def wash():
	        print('i am washing')
	       
10. 类方法

	通过@classmethod装饰器实现，类方法和普通方法的区别是， 类方法只能访问类变量，不能访问实例变量
	
		class Car:
	    __wheels=4
	    __voice='didi'
	    def __init__(self,color):
	        self.color=color
	    @property
	    def wheels(self):
	        return self.__wheels
	
	    @classmethod
	    def dudu(cls):
	        print(cls.__voice)
	        
	    @staticmethod
	    def wash():
	        print('i am washing')



		