##Python项目-Day25-response-cookie-session
1. response
	
	response的方法和属性有:


	
		1. headers	
		2. status	
		3. status_code	
		4. data	
		5. get_json(force=False, silent=False, cache=True)	
		6. is_json	
		7. max_cookie_size	
		8. mimetype	
		9. set_cookie(key, value=”, max_age=None, expires=None, path=’/’, domain=None, secure=False, httponly=False, samesite=None)

	* 关于response

			@app.route('/1')
			def hello1():
			    return 'Hello'
			#当只有一个字符串返回，会自动转换为状态码为200， MIME 类型是text/html的response对象
			#return后面的值都是response对象
			@app.route('/3')
				def hello2():
				    return 'Hello3',200,{"key":"value"}#当返回多个字段时,会智能对照,MIME 类型是text/html的response对象,字典里的东西会被当成headers

			@app.route('/4')
				def hello3():
					 rsp = make_response('hello4') #这个方法生成了一个response对象
					 rsp.mimetype = 'text/plain'
					 rsp.headers['key'] = 'value'
					 rsp.set_cookie('user','wang')#这个值可以用接下来访问的request.cookies来取得
					 rsp.data='返回的内容'
					 return rsp #使用make_response来处理response

	* 请求拦截

		请求之前:

			@app.before_request
			def all():
			    print('必须经过这里')

		请求之后

			@app.after_request
			def after_request(response):
			    print('请求结束的时候')

	* jsonnify和json.dumps(注意:要导入flask包中的jsonnify)

		jsonnify:将我们传入的json形式数据序列化成为json字符串，作为响应的body，并且设置响应的Content-Type为application/json，构造出响应返回至客户端。

		json.dumps:Content-Type字段值为text/html


2. session和cookie的区别

	1、cookie数据存放在客户的浏览器上，session数据放在服务器上。
	
	2、cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗
	   考虑到安全应当使用session。
	
	3、session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能
	   考虑到减轻服务器性能方面，应当使用COOKIE。
	
	4、单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。
	
	5、所以个人建议：
	   将登陆信息等重要信息存放为SESSION
	   其他信息如果需要保留，可以放在COOKIE中

	在flask项目中,session和cookies以及一些第三方扩张都会用到SECRET_KEY值,是一个比较重要的配置值.
	* session

			#开启session持久化存储
			session.permanent = True
			app.permanent_session_lifetime = timedelta(hours=1)
			#这个uid就会用app.secret_key = '123456'来进行加密，然后会通过cookie发送到客户端
			session['uid'] = '1'
	启用 permanent 之后 session lifetime 才会被应用，否则 session 在浏览器关闭时过期（在浏览器端就是 cookies 过期）；
	
			#获取session
				1.session['id']
				2.session.get('id')
			#删除session
			session.clear()

	* cookie
	
	服务器要识别来自同一个用户的请求 依赖与cookie 访问者在第一次请求 服务器的时候 服务器会在其cookie中 设置唯一的sessionId值 服务器就可以通过唯一的sessionid来去区分不同用户的请求(访问)

		response.set_cookie(
				key,
			    value,
			    max_age=None,设置过期时间 单位为秒
			    expires=None,以秒为单位的寿命
			    path = '/'

				)

		#设置cookie的过期时间
		1.
		response.set_cookie('name','zhangsan',expires=life_time) #设置当期cookie存活时间为1分钟
		2.
		response.set_cookie('name','zhangsan',max_age=60) #设置当期cookie存活时间为1分钟

		#获取cookie
		myCookie = request.cookies #获取所有cookie
		#删除cookie
		response.delete_cookie('name') #删除key为name的cookie

