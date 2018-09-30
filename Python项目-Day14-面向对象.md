##Python项目-Day14-面向对象

1. 动态添加属性

	* python可以为一个对象添加一个属性,但是并不会影响到同类的其他属性


			class Person:
				pass
			
			p1=Person()
			p2=Person()
			
			p1.gender="male"
			
			#p2的并不会添加gender属性

	* 动态为对象绑定方法

			from types import MethodType
			class Person:
				pass
			def displayMe(self):
				print("my genderis:",self.gender)
			#给一个实例绑定的方法,对另一个实例是不起作用的
			
			p1.displayMe=MethodType(displayMe,p1)
			p1.displayMe()


	* 通过动态给类增加属性和方法，可以实现所有对象都增加了属性和方法
	
			```
				Person.gender='male'
				def displayMe(self):
	    			print('my genderis:', self.gender)
	    			
	    		Person.displayMe=displayMe
			```

	* 使用__slots__限制实例的属性.比如，只允许对Student实例添加name和age属性。


		
			class Person(object):
			    __slots__=('name','age')
			
			p1=Person()
			print(dir(p1))
			# 这是看到p1对象里已经存在name和age属性了
			try:
			    p1.gender = 'female'
			except Exception:
			    print('使用__slots__限制实例的属性')

2. 删除属性

	

	
			class Person:
			        def __init__(self):
        				self.age=1
			p1=Person()
			p2=Person()
			p1.gender='male'
			
			Person.nation='china'
			
			del p1.gender
			
			del p1.nation #error nation属于类的，不可以通过对象删除
			
			del Person.nation
			
			del p1.age #这是可以的

3. 利用函数动态绑定

	
		#该语句只能添加属性，不能添加方法
		setattr(ee2, 'age', 8) # 添加属性 'age' 值为 8
		getattr(ee1, 'age')   	# 返回 'age' 属性的值
		hasattr(ee1, 'age')   	# 如果存在 'age' 属性返回 True。
		delattr(ee1, 'age')  	# 删除属性 'age'

