##Python项目-Day27-token解析装饰器-python连接mysql
1. 使用装饰器解析token


		from functools import wraps
		import jwt
		import datetime
		from flask import Blueprint,request
		datetimeInt = datetime.datetime.utcnow() + datetime.timedelta(seconds=180)
		SECRECT_KEY = 'secret'
		def checkToken():
		    def decorated(func):
		        @wraps(func)
		        def wrapper():
		            
		            try:
		                token=request.headers['token']
		                print('token 是：')
		                print(token)
		                decoded = jwt.decode(token, SECRECT_KEY, audience='webkit', algorithms=['HS256'])
		                return func()
		            except jwt.ExpiredSignatureError as err:
		                print("erroing.................",err)
		                decoded = {"error_msg": "is timeout !!", "some": None}
		                return '{"code":"004"}'+request.url #此处需要改进哦
		            except Exception:
		                decoded = {"error_msg": "noknow exception!!", "some": None}
		                print("erroing2.................")
		                return '{"code":"004"}'+request.url
		
		        return wrapper
		
		    return decorated
		
		
		def jwtEncoding(some, aud='webkit'):
		    datetimeInt = datetime.datetime.utcnow() + datetime.timedelta(seconds=180)
		    print(datetimeInt)
		    option = {
		        'iss': 'jobapp.com',
		        'exp': datetimeInt,
		        'aud': 'webkit',
		        'some':some
		    }
		    encoded2 = jwt.encode(option, SECRECT_KEY, algorithm='HS256')
		    print(encoded2.decode())
		    return encoded2.decode()
		
		if __name__ == '__main__':
		    res=jwtEncoding('{"userid","889"}')
		
		    print(res)
		
	在路由方法中调用
	
		@resume_app.route('/add')  #/user/add
		@checkToken()  #此处需要用户权限调用
		def add():
		    return '添加简历'

2. python连接数据库MySQL


		首页导入pymysql
		import pymysql
		#新建一个连接到数据库
		connect = pymysql.connect(host='127.0.0.1', user='root', port=3306, password='', db=database)
		生成一个游标
		cursor=connect.cursor()
		#写出要执行的sql语句
		sql='select * from user'
		#执行sql
		cursor.execut(sql)
		#获取执行结果
		res=cursor.fetchall()
		print(res)
		#关闭游标
		cursor.close()
		connect.close()


	将python连接mysql封装起来

	\__init__.py
		
		import pymysql
		def get_connect(database):
		    connect = pymysql.connect(host='127.0.0.1', user='root', port=3306, password='', db=database)
		    return connect



	mysql_connect.py

		from app.dao.__init__ import get_connect
		def test_a(**kwargs):
		    print(kwargs)
		    sql=''
		    for i in kwargs.keys():
		        print(i)
		        if not sql:
		            sql=sql+i
		        else:
		            sql = sql + ',' + i
		    print(sql)
		def create_mysql_connect(database,table,name,psd):
		    try:
		        connect = get_connect(database)
		        cursor = None
		
		
		        cursor = connect.cursor()
		
		
		        sql = 'INSERT INTO {0} (username,password) VALUES ("{1}","{2}")'.format(table,name,psd)
		        print(sql)
		        res = cursor.execute(sql)
		
		        connect.commit()
		    except Exception as ex:
		        print(ex)
		    finally:
		        if cursor:
		            cursor.close()
		        if connect:
		            connect.close()
		
		def select_table(table):
		    try:
		        connect=None
		        cursor=None
		        connect = get_connect('test')
		        cursor = connect.cursor()
		        sql = 'SELECT * from {0}'.format(table)
		        cursor.execute(sql)
		        res=cursor.fetchall()
		        return res
		    except Exception as ex:
		        print(ex)
		    finally:
		        if cursor:
		            cursor.close()
		        if connect:
		            connect.close()

