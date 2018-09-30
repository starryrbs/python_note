##Python项目-Day8
1. List

	- List的初始化

			fruits=['orange','apple','apple','water','banana','pear']

	- List相加

			price=[12,23,12]
			print(fruits+price,"test")

		>结果为

			['orange', 'apple', 'apple', 'water', 'banana', 'pear', 12, 23, 12] 

	- List添加,插入,删除
		
			fruits.append('water')#向列表添加元素
			fruits.extend(price)#向列表中添加列表


			fruits.insert(2, 'aaa')
			print(fruits,"test")#向列表中插入元素

		>删除元素(3种)

			 删除元素
			fruits.remove('apple')
			fruits.remove(fruits[1])

			del fruits[1]
			#删除多个元素
			del fruits[0:2]


			fruits[0:2]=[]

	- 清空List

			fruits.clear()
			fruits[:]=[]

	- List去重
		定义一个新数组,遍历原数组,如果元素不在新数组中,就加入到新数组
	
			new_fruits=[]
			
			for item in fruits:
				if item not in new_fruits:
					new_fruits.append(item)
			print(new_fruits)

	- 二维的List

			books=[['三国演义','罗贯中',100,'三国出版社',10],
			       ['水浒传', '施耐庵', 10, '西天出版社',50],
			        ['三国志','网易',80,'天天出版社',40],
			        ['西游记','吴承恩',20,'美团出版社',60],
			        ['三国杀','腾讯',900,'饿了么出版社',75]
			]

	- List的初始化
			
			list01=[i for i in range(10)]#数组的初始化
			list02=[i for i in range(10) if i%2==0]#数组的初始化
			list03=[i*2 for i in range(10)]

2. queue队列

	* deque在collections中

			from collections import deque
			# # 从collections导入queue
	* 将List转化成队列

			fruits=['orange','apple']
			
			queue=deque(fruits)

	* 队列的几种方法

			queue.append('after')#右边加元素
			queue.appendleft('before')#左边加元素
			queue.pop()#右边删除元素
			queue.popleft()#左边删除元素

	* 用deque达成栈和队列效果

			append()+popleft()形成队列数据结构
			
			append()+pop()形成栈数据结构

3. 选择排序和冒泡排序

		# 冒泡排序
		num=[3,1,2]
		for i in range(len(num)-1):
		    for j in range(len(num)-i-1):
		        if num[j]<num[j+1]:
		            num[j],num[j+1]=num[j+1],num[j]
		
		print(num)
		# 选择排序
		arr=[5,3,7]
		
		for i in range(len(arr)-1):
		    for j in range(i+1,len(arr)):
		        if arr[j]>arr[i]:
		            arr[j], arr[i] = arr[i], arr[j]
		
		print(arr)

4. 元组
	就是不能修改值得列表

		tu=(7.8,9)#元组初始化
		任何以,分隔开的元素是元组
		c=12,13,14


5. 类型转化

		# 类型转化
		int() float() bool() str() list() tuple()
