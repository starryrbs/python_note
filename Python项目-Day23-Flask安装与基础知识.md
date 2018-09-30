##Python项目Day23-Flask安装与基础知识
1. Flask安装与介绍

	>使用pip命令

			pip install flask

	>Flask是一个轻量级的web应用框架

2. Flask的启动

		#导入flask包中的Flask方法
		from flask import Flask
		#创建一个Flask类的实例,第一个参数是模块的名字
		app = Flask(__name__)
		#route装饰器告诉Flask什么样的url能触发函数
		@app.route('/')
		def hello_world():
		    return 'Hello World!'
		#__name=="__main"表示当前模块作为启动模块才会执行下面的代码
		if __name__ == '__main__':
			#让应用运行在服务器上
			app.run()
3. 变量规则

	要给url添加变量部分,这个部分将会作为命名参数传递到你的函数

		@app.route('/user/<username>')
		def show_user_profile(username):
		    # show the user profile for that user
		    return 'User %s' % username
		#指定参数类型
		@app.route('/post/<int:post_id>')
		def show_post(post_id):
		    # show the post with the given id, the id is an integer
		    return 'Post %d' % post_id

	参数的类型有以下几种:

	![](https://i.imgur.com/I3d5DtA.jpg)

4. url_for()

	通过url_for()来给指定的函数构造url

		from flask import Flask, url_for
		app = Flask(__name__)
		@app.route('/')
		def index(): pass
		
		@app.route('/login')
		def login(): pass
		
		@app.route('/user/<username>')
		def profile(username): pass
		
		with app.test_request_context():
		print url_for('index')
		print url_for('login')
		print url_for('login', next='/')
		print url_for('profile', username='John Doe')

5. redirect

	可以使用redirect()函数把用户重定向到其它地方

		from flask import abort, redirect, url_for
		
		@app.route('/')
		def index():
		    return redirect(url_for('login'))
		
		@app.route('/login')
		def login():
		    retur "login....."

6. Flask的Demo

	route.py

		from flask import Flask,url_for,redirect
		# url_for()根据方法名获取路径
		# redirect()路由重定向
		from app import app
		print(id(app))
		from public.var import *
		public_param()
		setValue('isLogin',False)
		now_url=""
		@app.route('/')
		def hello_world():
		    return 'hello world'
		def login(user_id,password):
		    if user_id=='admin' and password=='123456':
		
		        return 'hello user ' + user_id + password
		    else:
		        login_url = url_for('hello')
		        print(login_url,11111111111111111)
		        return redirect(login_url)
		        # return 'False'
		@app.route('/user/<user_id>/<password>')
		def user(user_id,password):
		    return login(user_id,password)
		
		@app.route('/hello')
		def hello():
		    return "hello"

	app.py

		
		from flask import Flask
		app=Flask(__name__)


	程序入口文件 run.py

		from flask import Flask
		
		
		from app import app
		print(id(app))
		import route
		
		if __name__ == '__main__':
		    app.run()