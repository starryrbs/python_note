###Python项目-Day9
1. set
	set是一组无序,元素唯一的集合

		set01={12,12,45,13}
		#set的遍历
		for i in set01:
			print(i)
		
		#判断元素是否在set里面
		print(12 in  set01)
		#判断set最大值
		print(max(set01))
		#判断set最小值
		print(min(set01))

	>注意:set是没有索引的
		
		print(set01[1])#错误
	
		#列表去重
		#原理就是将List转化成set然后再转化成List
		set_li =set(li)
		print(set_li)
		list_li=list(set_li)
		print(list_li)

2. 类型

		#元组只有一个值不是tuple,而是这个值得类型
		tu=(1)
		print(type(tu))

		#set为空是字典
		set01={}

3. set的一些方法

		set01.add(4)
		
		#discard#移除不存在的数据不会报错
		set01.discard(5)
		
		#remove移除不存在的元素会报错
		set01.remove(5)
		
		set01.pop()
		
		s1={6,8,9}
		s2={8,19,9}
		取交集
		s3=s1.intersection(s2)
		
		#去交集并把交集的值放到s2
		s2.intersection_update(s1)
		
		# 取并集
		s3 = s1.union(s2)
		print(s3)
		
		# 取不同项,并赋值 s5为19,6
		s5=s2.symmetric_difference(s1)
		print(s5)
		
		se = {1, 2, 3}
		be = {2}
		print(se.isdisjoint(be))  # False 判断是否不存在交集

4. 字典

		# 字典是可变的,没有索引(不能排序),不能切片
		user1 = {"name": "tom", "age": 12,1:2}  # key:value
		user2 = {"name": "tom", "age": 12,"name":980}  # key:value


		# 字典初始化
		uu={}
		uu['title']='python'
		uu['score']=90


		del uu['score']	#删除元素

		#字典的遍历

		for item in user1:
		     print(user1[item])


		for item in user.keys():
		     print(item)
		for item in user.values():
		     print(item,1)
		for k,v in user1.items():
		     print(k,v)
		for k in sorted(user1.keys()):
		     print(k)

5. 综合案例(用户登录注册系统)

		view_index='''
		    ====================
		        欢迎访问京西购物
		        1.登录
		        2.注册
		        3.退出
		    ====================
		
		'''
		view2='''
		    ====================
		        请选择
		        1.购物
		        2.退出
		    ====================
		
		'''
		view3='''
		    ====================
		        管理页面
		        1.管理用户
		        2.管理商品
		        3.退出
		    ====================
		
		'''
		print(view_index)
		# type:0表示管理员,1表示普通用户
		users=[
		    {"id":"001","username":"admin","password":"123",'type':0},
		    {"id":"002","username":"joker","password":"123",'type':1},
		    {"id":"003","username":"admin","password":"123",'type':1}
		
		
		]
		
		select_index=input("请选择\n")
		select_index=int(select_index)
		if select_index==1:
		    print("请登录:")
		    input_name=input("请输入用户名:\n")
		    input_password=input("请输入密码:\n")
		    isexist=False
		    isLogin=False
		    success_user={}
		    for user in users:
		        if(user["username"]==input_name):
		            isexist = True
		            success_user = user
		            isLogin=True
		            break
		    if isexist:
		         if input_password==success_user['password']:
		             if success_user['type']==1:
		                 print(view2)
		             else:
		                 print(view3)
		
		         else:
		             print("用户名或密码错误")
		    else:
		         print ("该用户不存在")
		elif select_index==2:
		    print("欢迎注册")
		    register_input_name=input("请输入你要注册的用户名")
		    register_input_password=input("请输入你要注册的密码")
		    isexist_reg = False
		    user_msg={}
		    for user in  users:
		        if user['username']==register_input_name:
		            isexist_reg=True
		            user_msg=user
		            break
		        else:
		            print("用户名已存在")
		else:
		    print("欢迎下次光临!")
