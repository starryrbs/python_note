##Python项目-Day51--中间件--跨域请求-jsonp-CORS
1. django中间件

	django 中的中间件（middleware），在django中，中间件其实就是一个类，在请求到来和结束后，django会根据自己的规则在合适的时机执行中间件中相应的方法。

	在django项目的settings模块中，有一个
	**MIDDLEWARE_CLASSES** 变量，其中每一个元素就是一个中间件.

2. 自定义中间件

	1. 在django_jobapp项目下新建一个文件夹mymiddleware,文件夹下创建一个middlewareauth.py文件

		中间中可以定义五个方法,分别是:


			1.process_request(self,request)
			2.process_view(self, request, callback, callback_args, callback_kwargs)
			3.process_template_response(self,request,response)
			4.process_exception(self, request, exception)
			5.process_response(self, request, response)

		[五个方法的详细介绍](https://www.cnblogs.com/felo/p/5600549.html)

		前二个方法是从前往后执行的，后三个方法是从后往前执行的

		执行流程:


	 	![](https://i.imgur.com/ocMXnsF.png)

			class AuthMiddleWare(MiddlewareMixin):
			    def process_request(self,request):
			        print("process_request")
			    def process_view(self, request, callback, callback_args, callback_kwargs):
			        print("process_view")
			    def process_template_response(self,request,response):
			        print("process_template_response")
			    def process_exception(self, request, exception):
			        print("process_exception")
			    def process_response(self, request, response):
			        return response

	2. 在settings.py设置自定义中间件
			
			MIDDLEWARE = [
			    'django.middleware.security.SecurityMiddleware',
			    'django.contrib.sessions.middleware.SessionMiddleware',
			    'django.middleware.common.CommonMiddleware',
			    # 'django.middleware.csrf.CsrfViewMiddleware',
			    'django.contrib.auth.middleware.AuthenticationMiddleware',
			    'django.contrib.messages.middleware.MessageMiddleware',
			    'django.middleware.clickjacking.XFrameOptionsMiddleware',
				#在这里加自定义中间件
			    'mymiddlewares.middlewareauth.AuthMiddleWare'
			]

##跨域请求
1. 为什么有跨域请求?

	同源策略

	首先基于安全的原因，浏览器是存在同源策略这个机制的，同源策略阻止从一个源加载的文档或脚本获取或设置另一个源加载的文档的属性。

	而如果我们要跳过这个策略，也就是说非要跨域请求，那么就需要通过JSONP或者CORS来实现了。

	解决方法

	1. JSONP
	2. CORS
2. JSONP

	[JSONP详细讲解](https://www.cnblogs.com/lijian-22huxiaoshan/p/7867649.html)

	1. 什么是JSONP?

		ajax请求受同源策略影响，不允许进行跨域请求，而script标签src属性中的链接却可以访问跨域的js脚本，利用这个特性，服务端不再返回JSON格式的数据，而是返回一段调用某个函数的js代码，在src中进行了调用，这样实现了跨域。

	2. 代码实现

		前端页面

			$.ajax({
                url:"http://127.0.0.1:8000/user/jsonp/",
                type:"get",
                dataType:"JSONP",     // 伪造ajax  基于script
                jsonp: 'callbacks',
                jsonpCallback:"alex",
                success:function (data) {
                    console.log(111);
                    console.log(data)
                }
            })

		后台views.py

			def jsonp_test(request):
			    func=request.GET.get("callbacks") #获取请求的callbacks参数
			    info={"name":"fuyong","age":18} #定义数据
			    return HttpResponse('{}({})'.format(func,json.dumps(info)) )#传json对象


		>总结:一句话就是利用script标签绕过同源策略，获得一个类似这样的数据。ajax里边的callbacks本质上是（伪装成script标签src属性发送请求的方式）发送一个回调方法，参数data就是想得到的json数据。

2. CORS

	1. 什么是CORS?

		Cross-Origin Resource Sharing（CORS）跨域资源共享是一份浏览器技术的规范，提供了 Web 服务从不同域传来沙盒脚本的方法，以避开浏览器的同源策略，是 JSONP 模式的现代版。与 JSONP 不同，CORS 除了 GET 要求方法以外也支持其他的 HTTP 要求。用 CORS 可以让网页设计师用一般的 XMLHttpRequest，这种方式的错误处理比 JSONP 要来的好。另一方面，JSONP 可以在不支持 CORS 的老旧浏览器上运作。现代的浏览器都支持 CORS。

	2. CORS对比jsonp

		都能解决 Ajax直接请求普通文件存在跨域无权限访问的问题
		
		1. JSONP只能实现GET请求，而CORS支持所有类型的HTTP请求
		2. 使用CORS，开发者可以使用普通的XMLHttpRequest发起请求和获得数据，比起JSONP有更好的错误处理
		3. JSONP主要被老的浏览器支持，它们往往不支持CORS，而绝大多数现代浏览器都已经支持了CORS


	3. CORS实现原理

		CORS背后的基本思想是使用自定义的HTTP头部允许浏览器和服务器相互了解对方

	##具体代码实现

	1. 安装CORS

			pip install django-cors-headers


		下面在settings.py里面进行配置
	2. 添加app

			INSTALLED_APPS = (

				    'corsheaders',

				)

	3. 添加中间件

			MIDDLEWARE = [  # Or MIDDLEWARE_CLASSES on Django < 1.10
			#注意顺序
					    ...
					    'corsheaders.middleware.CorsMiddleware',
					    'django.middleware.common.CommonMiddleware',
					    ...
					]

	4. 配置允许跨站访问本站的地址

			CORS_ORIGIN_ALLOW_ALL = False
						CORS_ORIGIN_WHITELIST = (
						      'localhost:63343',
						)

	5. 设置允许访问的方法

			CORS_ALLOW_METHODS = (
			'GET',
			'POST',
			'PUT',
			'PATCH',
			'DELETE',
			'OPTIONS'
			)

	6. 设置允许的header：

			默认值:
			
			CORS_ALLOW_HEADERS = (
			'x-requested-with',
			'content-type',
			'accept',
			'origin',
			'authorization',
			'x-csrftoken'
			)

    **request.getAllResponseHeaders()负责取出数据**
    
    **但是不行啊，原因**
    
    1：W3C的 xhr 标准中做了限制，规定客户端无法获取 response 中的 Set-Cookie、Set-Cookie2这2个字段，无论是同域还是跨域请求；

	2：W3C 的 cors 标准对于跨域请求也做了限制，规定对于跨域请求，客户端允许获取的response header字段只限于“simple response header”和“Access-Control-Expose-Headers” ，在“Access-Control-Allow-Headers”中加了无效

	"simple response header"包括的 header 字段有：Cache-Control,Content-Language,Content-Type,Expires,Last-Modified,Pragma;
	
	"Access-Control-Expose-Headers"：首先得注意是"Access-Control-Expose-Headers"进行跨域请求时响应头部中的一个字段，对于同域请求，响应头部是没有这个字段的。这个字段中列举的 header 字段就是服务器允许暴露给客户端访问的字段。

    
    ###服务器端代码
   	
		resp['token'] = '8888888888888'
		#允许暴露token
	   	resp["Access-Control-Expose-Headers"] = "token"


	###客户端代码

		ajax('POST',"http://127.0.0.1:8000/user/login/",null,function (result,xhr) {
		
	                // console.log(1,getCookie('sda'));
	                console.log(11111111);
	                console.log(result,xhr);
	                console.log(xhr.getAllResponseHeaders());
	                console.log(xhr.getResponseHeader('token'))

3. 在接口函数中配置

	这是最简单的一种方法

		from django.http import HttpResponse,response,JsonResponse
		def login(request):
		    todo_list = [
		        {"id": "1", "content": "吃饭"},
		        {"id": "2", "content": "吃饭"},
		    ]
		    response = JsonResponse(todo_list, safe=False)
		    response["Access-Control-Allow-Origin"] = "*"
		    response["Access-Control-Allow-Methods"] = "POST, GET, OPTIONS"
		    response["Access-Control-Max-Age"] = "1000"
		    response["Access-Control-Allow-Headers"] = "*"
		    return response