##Python项目-Day13
1. Python的excel操作

	* 安装 openpyxl

			pip install openpyxl

	
	* 打开excel表和读取

			from openpyxl import load_workbook
			try:
			    wb=load_workbook(r'员工表.xlsx')#获取工作簿名字,就是员工表.xlsx
			    sheetnames=wb.get_sheet_names()#获取所有工作表sheet
			    sheet=wb.get_sheet_by_name(sheetnames[0])#获取第一个sheet工作表
			    # print(sheet.max_row)#获取表的最大行数是多少
			    # print(sheet.max_column)#获取表的最大列数是多少
			except Exception as ex:#异常处理
			    print(ex)

	* 获取值
	

		        # 获取某个单元格的值，观察excel发现也是先字母再数字的顺序，即先列再行
		        b4 = sheet['A4']  #A行4列
		
		        # 除了用下标的方式获得，还可以用**cell函数**, 换成数字，这个表示B4
		        b4_too = sheet.cell(row=4, column=2)
		        print(b4_too.value)
		
		
		        for i in range(2):
		            for j in range(5):
		                print(sheet.cell(row=i+1, column=j+1).value,end=' ')
		            print()
	* excel表的写操作
	* 
			try:
			#     新建工作簿
			    wb=Workbook()
			#     新建一个工作表,可以指定索引，适当安排其在工作簿中的位置
			    sheet=wb.create_sheet('Data',index=1)# 被安排到第二个工作表，index=0就是第一个位置
			    sheet.append(table_header)
			    for row in table_content:
			        sheet.append(row)
			    wb.save(r'myexcel.xlsx')
			except Exception as ex:
			    print(ex)
			
			# 删除某个工作表
			            # wb.remove(wb)

2. 面向对象oop（Object Oriented Programming，OOP，面向对象程序设计)

	面向对象最重要的概念就是**类**（Class）和**实例**（Instance），必须牢记类是抽象的模板，而实例是根据类创建出来的一个个具体的“对象”，每个对象都拥有相同的方法，但各自的数据可能不同。

	Python类提供了面向对象编程的所有标准功能：类继承机制允许**多个基类**，派生类可以**重写**其基类或类的任何方法，并且方法可以调用具有相同名称的基类的方法。对象可以包含任意数量和种类的数据。与模块一样，类也具有Python的动态特性：它们是在运行时创建的，并且可以在创建后进一步修改。

	* 定义类

			class Employee:
				empCount=0
				# empCount 变量是一个类变量，它的值将在这个类的所有实例之间共享。你可以在内部类或外部类使用 Employee.empCount 访问。
				# 方法__init__()方法是一种特殊的方法，被称为类的构造函数或初始化方法，当创建了这个类的实例时就会调用该方法
				def __init__(self,name,salary):
					self.name = name
					self.salary = salary
					Employee.empCount += 1
 				# self 代表类的实例，self 在定义类的方法时是必须有的，虽然在调用时不必传入相应的参数。
			def displayCount(self):
			            print ("Total Employee %d" % Employee.empCount)
			            print (self.__class__)

			#创建一个Employee对象employee1
			employee1=Employee("张三",1000)
			#定义对象时必须制定对象的属性,不然会报错
			#动态的添加、删除对象的属性
			employee1.name="李四"
			#删除对象的属性
			del employee1.name
			print(hasattr(ee1,'age'))#如果ee1对象存在'age'属性则返回True,反之False
			print(getattr(ee1,'age'))#返回ee1对象的'age'属性的值
			setattr(ee2,'age',8)#添加属性'age',值为8
		