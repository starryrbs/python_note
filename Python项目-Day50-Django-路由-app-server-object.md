##Python项目-Day50-Django-路由-app-server-object
1. 路由

	urls.py


		from django.conf.urls import url
		    from django.contrib import admin
		    from . import view
		    from . import personal
		    
		    urlpatterns = [
				from django.urls import path
				path('admin/', admin.site.urls),
		        url(r'^$', view.hello),
		        url(r'^person\w*$', personal.login),
				#实现在url上传递参数
				url(r'^get\w*/(?P<myid>\d*)', views.getuserbyid),
		    ]


	path与url是两个不同的模块,效果都是响应返回页面.

	1. path调用的是python第三方模块或框架
	2. 而url则是自定义的模块

2. 导入其他应用的路由文件

	使用include

		from django.conf.urls import include


		urlpatterns = [
		url(r'^polls/', include('polls.urls')),namespace='obapp.user'
		]

	namespace

	由于name没有作用域，Django在反解URL时，会在项目全局顺序搜索，当查找到第一个name指定URL时，立即返回
	我们在开发项目时，会经常使用name属性反解出URL，当不小心定义相同的name时，可能会导致URL反解错误，为了避免这种事情发生，引入了命名空间

	[详细讲解namespace](https://www.cnblogs.com/cq146637/p/7806336.html)

3. path函数

	path(route, view, kwargs=None, name=None, Pattern=None)

    1. route

        模式不搜索GET和POST参数或域名。例如，在请求中https://www.example.com/myapp/，URLconf将查找 myapp/。在请求中https://www.example.com/myapp/?page=3，URLconf也将查找myapp/。不支持正则
    2. view
        当Django找到一个匹配的模式时，它会以一个HttpRequest对象作为第一个参数以及路由中的任何“捕获”值作为关键字参数来调用指定的视图函数。
    3. kwargs

        任意关键字参数可以在字典中传递给目标视图。

		例如:

			path(r'index/<int:id>', views.index,kwargs={"id":1}, name='index'),

			views.py中


			def index(request,id):
			    return HttpResponse("HELLO WORLD"+str(id))

			在地址栏输入:
			http://127.0.0.1:8000/index/1	
			此时就将1传过去了	

    4. name

        命名您的URL可以让您从Django其他地方明确地引用它，特别是在模板中。这个强大的功能允许您在只触摸单个文件的情况下对项目的URL模式进行全局更改。

5. app

	>项目和应用程序有什么区别？
	
	应用程序是一种Web应用程序，它可以执行某些操作，例如Weblog系统，公共记录数据库或简单的轮询应用程序。项目是特定网站的配置和应用程序的集合。**项目可以包含多个应用程序。一个应用程序可以在多个项目中。**

	1. 创建一个app

		python manage.py startapp polls
	
	2. 在settings.py添加app

		INSTALLED_APPS = [
		    'django.contrib.admin',
		    'django.contrib.auth',
		    'django.contrib.contenttypes',
		    'django.contrib.sessions',
		    'django.contrib.messages',
		    'django.contrib.staticfiles',
		    'boke',
		    'job',
		    'user'
		]

	3. 在app下新建一个urls.py文件
			
			from . import views
			from django.conf.urls import url
			
			app_name = "user"
			# user子路由
			urlpatterns = [
			    url(r'^$', views.personal, name="personal"),
			    url(r'login/', views.login, name="login")
			]
	4. 在主路由中添加user子路由

			#导入include
			from django.urls import path,include
			url(r'^user/',include('user.urls',namespace='obapp.user'))

6. 路由重定向

	render：只会返回页面内容，但是未发送第二次请求,用来转向页面

		return render(request,'index.html')

	redirect：发挥了第二次请求，url更新

		my_url=reverse('user:personal')
	    return redirect(my_url)

	reverse:逆向解析url

		my_url=reverse('user:personal',args=(1,))
		#args中的参数传给了url中route的参数id
		url(r'(?P<id>\d+)', views.personal, name="personal"),
		#在这里接收到了id
		def personal(request,id):
		    print("执行了personal")
		    print("id",id)
		    return HttpResponse("个人中心")

##服务器对象
1. request

	request.method

	通过request.method可以查看提交方式

	request.scheme
	
	代表请求的方案,http或者https
	
	request.path
	
	请求的路径,比如请求127.0.0.1/org/list,那这个值就是/org/list
	
	request.method
	
	表示请求使用的http方法,GET或者POST请求
	
	request.encoding
	
	表示提交数据的编码方式
	
	request.GET
	
	获取GET请求
	
	request.POST
	
	获取post的请求,比如前端提交的用户密码,可以通过request.POST.get()来获取
	
	另外：如果使用 POST 上传文件的话，文件信息将包含在 FILES 属性中
	
	request.COOKIES
	
	包含所有的cookie
	
	request.META
	
	一个标准的Python 字典，包含所有的HTTP 首部。具体的头部信息取决于客户端和服务器，下面是一些示例：
	
	CONTENT_LENGTH —— 请求的正文的长度（是一个字符串）。

	CONTENT_TYPE —— 请求的正文的MIME 类型。

	HTTP_ACCEPT —— 响应可接收的Content-Type。

	HTTP_ACCEPT_ENCODING —— 响应可接收的编码。

	HTTP_ACCEPT_LANGUAGE —— 响应可接收的语言。

	HTTP_HOST —— 客服端发送的HTTP Host 头部。

	HTTP_REFERER —— Referring 页面。

	HTTP_USER_AGENT —— 客户端的user-agent 字符串。

	QUERY_STRING —— 单个字符串形式的查询字符串（未解析过的形式）。

	REMOTE_ADDR —— 客户端的IP 地址。

	REMOTE_HOST —— 客户端的主机名。

	REMOTE_USER —— 服务器认证后的用户。

	REQUEST_METHOD —— 一个字符串，例如"GET" 或"POST"。

	SERVER_NAME —— 服务器的主机名。

	SERVER_PORT —— 服务器的端口（是一个字符串）

2. request解析数据

	1. get

			#如果提交数据方式为：
			http://localhost:8080/position/12/?name=tom&pass=123

			获取方式：
					
			request.GET.get('name')
			request.GET['pass']

	2. post

	
		a. post数据为form-data或者x-www-urlencoded

			if request.method=='POST':
	        id=request.POST.get('id')
	        
	        #当客户端数据为{‘key’:[1,3,6,7]} 时（发送数据需加：tranditional:true），
	        list=request.POST.getlist('do')
	        password=request.POST['password']

		b. post数据为json
					
			if request.method=='POST':
				
				
		        data=json.loads(request.body)
		
		        id=data['id']
		        password=data['password']

2. 获取Header中的信息

	1. request.META.get("header key") 用于获取header的信息
	2. 注意的是header key必须增加前缀HTTP，同时大写，例如你的key为username，那么应该写成：request.META.get("HTTP_USERNAME")
	3. 另外就是当你的header key中带有中横线，那么自动会被转成下划线，例如my-user的写成： request.META.get("HTTP_MY_USER")


				token=request.META.get('HTTP_TOKEN')
        		print(token)
        	
	**注意post提交出错**
		
	1. url最后应该加/ 如：http://localhost:8080/position/add/
	2. settings.py中可能要注释掉：# 'django.middleware.csrf.CsrfViewMiddleware',
	**为什么要这样呢，因为django默认会验证token(每次请求django都会带回来一个token,m名字叫X-CSRFtoken).如果要顺利请求则要取出cookie中的token，然后ojax.setRequestHeader('X-CSRFtoken',token)。**
	4. cookie

			request.COOKIES：包含用户发来的所有数据，这个COOKIES就是一个字典，获			取方法有以下2种
			
			获取cookis,获取用户发来请求中的cookies
			
				request.COOKIES['username111']
				request.COOKIES.get('username111')
	