##Python项目-Day24-flask-request

1. request

	1. method
	
		主流的方式是GET,POST,默认浏览器只回应GET方式

		get参数通过url传递，post放在request body中。
		
		get请求在url中传递的参数是有长度限制的，而post没有。
		
		get比post更不安全，因为参数直接暴露在url中，所以不能用来传递敏感信息。
		
		get请求只能进行url编码，而post支持多种编码方式
		
		
		
		get请求参数会被完整保留在浏览历史记录里，而post中的参数不会被保留。
		
		
		GET和POST本质上就是TCP链接，并无差别。但是由于HTTP的规定和浏览器/服务器的限制，导致他们在应用过程中体现出一些不同。
		GET产生一个TCP数据包；POST产生两个TCP数据包。



			from flask import request
	
			@app.route('/login', methods=['GET', 'POST'])
			def login():
			    if request.method == 'POST':
			        return do_the_login()
			    else:
			        return show_the_login_form()
		2. form属性


		
				@app.route('/login', methods=['POST', 'GET'])
				def login():
				    error = None
				    if request.method == 'POST':
				        if valid_login(request.form['username'],
				                       request.form['password']):
				            return log_the_user_in(request.form['username'])
				        else:
				            error = 'Invalid username/password'
				    # the code below is executed if the request method
				    # was GET or the credentials were invalid
				    return render_template('login.html', error=error)
		form的enctype属性为编码属性

			1. application/x-www-form-urlencoded: 表单数据编码为键值对，&分隔
			
			2. multipart/form-data: 表单数据编码为一条消息，每个控件对应消息的一部分

		[请查看详细的区分](https://www.cnblogs.com/mengff/p/7282488.html)

	3. args属性

		可以获取URL(?key)中提交的参数,可以使用args属性:

		地址:127.0.0.1:5081?id=123

		使用request.args		结果为:ImmutableMultiDict([('id', '123')])
		
		使用request.args['id'] 结果为:123

	4. values属性

		比args更强大,使用方法类似

	5. url属性

		request.url			获取当前请求的完整路径，包括查询字符串

		request.base_url   获取基本路径

		示例:


			print(request.url)

			print(request.base_url)
			#结果为:
			http://127.0.0.1:5081/?id=123
			http://127.0.0.1:5081/

	5. json属性和get_json(),get_data()

			        if request.is_json:
			            json_data=request.get_json()
			            print(json_data['userid'])
			        else:
			        	#当ajax提交数据不是json类型是默认是bytes
			        	#将bytes数据转化为dict
			            data=str(request.get_data(),encoding='utf-8')
			            dict_data=eval(data)
			            print(dict_data['userid'])
	

	5. 提交数据的方式

		1. get
			通过url: url?key=value&key2=value2
			数据编码：x-www-form-urlencoded
			数据类型（data-type）:application/text
		2. post

			1. form-data

				数据编码：字节码
			2. x-www-form-urlencoded
			3. json
				
				数据类型（data-type）:application/json

	6. headers

		HTTP Headers是HTTP请求和相应的核心，它承载了关于客户端浏览器，请求页面，服务器等相关的信息。
		
		未完