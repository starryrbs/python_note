##Python项目-Day42-urllib基础-handler-opener()
1. urlopen（）

	 在python2.x版本中可以直接使用import urllib来进行操作，但是python3.x版本中使用的是import urllib.request来进行操作


	
2. GET请求

	urllib的request模块可以非常方便地抓取URL内容，也就是发送一个GET请求到指定的页面，然后返回HTTP的响应

	例如，对豆瓣的一个URLhttps://api.douban.com/v2/book/2129650进行抓取，并返回响应：


		from urllib import request
		
		with request.urlopen('https://api.douban.com/v2/book/2129650') as f:
		    data = f.read()
		    print('Status:', f.status, f.reason)
		    for k, v in f.getheaders():
		        print('%s: %s' % (k, v))
		    print('Data:', data.decode('utf-8'))

	可以看到HTTP响应的头和JSON数据：

		Accept-Ranges bytes
		Cache-Control no-cache
		Content-Length 227
		Content-Type text/html
		Date Thu, 13 Sep 2018 08:32:11 GMT
		Etag "5b8641dc-e3"
		Last-Modified Wed, 29 Aug 2018 06:49:00 GMT
		P3p CP=" OTI DSP COR IVA OUR IND COM "
		Pragma no-cache
		Server BWS/1.1
		Set-Cookie BD_NOT_HTTPS=1; path=/; Max-Age=300
		Set-Cookie BIDUPSID=34DDE02F7170E819905118D8890D9EEA; expires=Thu, 31-Dec-37 23:55:55 GMT; max-age=2147483647; path=/; domain=.baidu.com
		Set-Cookie PSTM=1536827531; expires=Thu, 31-Dec-37 23:55:55 GMT; max-age=2147483647; path=/; domain=.baidu.com
		Strict-Transport-Security max-age=0
		X-Ua-Compatible IE=Edge,chrome=1
		Connection close

	如果我们想要模拟浏览器发送请求，因为默认User-Agent是python，会轻松的被检测成爬虫，修改User-Agent就要使用到Request对象。

		from urllib import request
		
		req = request.Request('http://www.douban.com/')
		req.add_header('User-Agent', 'Mozilla/6.0 (iPhone; CPU iPhone OS 8_0 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Version/8.0 Mobile/10A5376e Safari/8536.25')

	还可以设置一个模拟的浏览器列表，每次请求使用不同的浏览器

		  MY_USER_AGENT = [
		        "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; AcooBrowser; .NET CLR 1.1.4322; .NET CLR 2.0.50727)",
		        "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; Acoo Browser; SLCC1; .NET CLR 2.0.50727; Media Center PC 5.0; .NET CLR 3.0.04506)",
		        "Mozilla/4.0 (compatible; MSIE 7.0; AOL 9.5; AOLBuild 4337.35; Windows NT 5.1; .NET CLR 1.1.4322; .NET CLR 2.0.50727)",
		        "Mozilla/5.0 (Windows; U; MSIE 9.0; Windows NT 9.0; en-US)",
		        "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0; .NET CLR 3.5.30729; .NET CLR 3.0.30729; .NET CLR 2.0.50727; Media Center PC 6.0)",
		        "Mozilla/5.0 (compatible; MSIE 8.0; Windows NT 6.0; Trident/4.0; WOW64; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; .NET CLR 1.0.3705; .NET CLR 1.1.4322)",
		        "Mozilla/4.0 (compatible; MSIE 7.0b; Windows NT 5.2; .NET CLR 1.1.4322; .NET CLR 2.0.50727; InfoPath.2; .NET CLR 3.0.04506.30)",
		        "Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN) AppleWebKit/523.15 (KHTML, like Gecko, Safari/419.3) Arora/0.3 (Change: 287 c9dfb30)",
		        "Mozilla/5.0 (X11; U; Linux; en-US) AppleWebKit/527+ (KHTML, like Gecko, Safari/419.3) Arora/0.6",
		        "Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.8.1.2pre) Gecko/20070215 K-Ninja/2.1.1",
		        "Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN; rv:1.9) Gecko/20080705 Firefox/3.0 Kapiko/3.0",
		        "Mozilla/5.0 (X11; Linux i686; U;) Gecko/20070322 Kazehakase/0.4.5",
		        "Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.0.8) Gecko Fedora/1.9.0.8-1.fc10 Kazehakase/0.5.6",
		        "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11",
		        "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_3) AppleWebKit/535.20 (KHTML, like Gecko) Chrome/19.0.1036.7 Safari/535.20",
		        "Opera/9.80 (Macintosh; Intel Mac OS X 10.6.8; U; fr) Presto/2.9.168 Version/11.52",
		        "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.11 TaoBrowser/2.0 Safari/536.11",
		        "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.1 (KHTML, like Gecko) Chrome/21.0.1180.71 Safari/537.1 LBBROWSER",
		        "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; WOW64; Trident/5.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E; LBBROWSER)",
		        "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; QQDownload 732; .NET4.0C; .NET4.0E; LBBROWSER)",
		        "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.84 Safari/535.11 LBBROWSER",
		        "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.1; WOW64; Trident/5.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)",
		        "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; WOW64; Trident/5.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E; QQBrowser/7.0.3698.400)",
		        "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; QQDownload 732; .NET4.0C; .NET4.0E)",
		        "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; Trident/4.0; SV1; QQDownload 732; .NET4.0C; .NET4.0E; 360SE)",
		        "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; QQDownload 732; .NET4.0C; .NET4.0E)",
		        "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.1; WOW64; Trident/5.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)",
		        "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.1 (KHTML, like Gecko) Chrome/21.0.1180.89 Safari/537.1",
		        "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.1 (KHTML, like Gecko) Chrome/21.0.1180.89 Safari/537.1",
		        "Mozilla/5.0 (iPad; U; CPU OS 4_2_1 like Mac OS X; zh-cn) AppleWebKit/533.17.9 (KHTML, like Gecko) Version/5.0.2 Mobile/8C148 Safari/6533.18.5",
		        "Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:2.0b13pre) Gecko/20110307 Firefox/4.0b13pre",
		        "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:16.0) Gecko/20100101 Firefox/16.0",
		        "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.11 (KHTML, like Gecko) Chrome/23.0.1271.64 Safari/537.11",
		        "Mozilla/5.0 (X11; U; Linux x86_64; zh-CN; rv:1.9.2.10) Gecko/20100922 Ubuntu/10.10 (maverick) Firefox/3.6.10",
		        "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36",
		    ]


	* get提交数据-urlencode（）

			from urllib import request,parse
			#当前urllib放在parse模块中
			query={"q":"python"}
			query=parse.urlencode(query)
			url='http://www.bootcss.com/'+'?'+query

	* 解决https无法爬取的问题

			import ssl
			ssl._create_default_https_context = ssl._create_unverified_context


3. POST请求

	如果要以POST发送一个请求，只需要把参数data以bytes形式传入
	我们模拟一个微博登录，先读取登录的邮箱和口令，然后按照weibo.cn的登录页的格式以username=xxx&password=xxx的编码传入：

		from urllib import request, parse
		
		print('Login to weibo.cn...')
		email = input('Email: ')
		passwd = input('Password: ')
		login_data = parse.urlencode([
		    ('username', email),
		    ('password', passwd),
		    ('entry', 'mweibo'),
		    ('client_id', ''),
		    ('savestate', '1'),
		    ('ec', ''),
		    ('pagerefer', 'https://passport.weibo.cn/signin/welcome?entry=mweibo&r=http%3A%2F%2Fm.weibo.cn%2F')
		])
		
		req = request.Request('https://passport.weibo.cn/sso/login')
		req.add_header('Origin', 'https://passport.weibo.cn')
		req.add_header('User-Agent', 'Mozilla/6.0 (iPhone; CPU iPhone OS 8_0 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Version/8.0 Mobile/10A5376e Safari/8536.25')
		req.add_header('Referer', 'https://passport.weibo.cn/signin/login?entry=mweibo&res=wel&wm=3349&r=http%3A%2F%2Fm.weibo.cn%2F')
		
		with request.urlopen(req, data=login_data.encode('utf-8')) as f:
		    print('Status:', f.status, f.reason)
		    for k, v in f.getheaders():
		        print('%s: %s' % (k, v))
		    print('Data:', f.read().decode('utf-8'))

	如果登录成功，我们获得的响应如下：

		Status: 200 OK
		Server: nginx/1.2.0
		...
		Set-Cookie: SSOLoginState=1432620126; path=/; domain=weibo.cn
		...
		Data: {"retcode":20000000,"msg":"","data":{...,"uid":"1658384301"}}

	如果登录失败，我们获得的响应如下：

		Data: {"retcode":50011015,"msg":"\u7528\u6237\u540d\u6216\u5bc6\u7801\u9519\u8bef","data":{"username":"example@python.org","errline":536}}

5. ajax请求json数据

	如果网站采用c/s模式：那么页面数据是返回json这个时候，我们要找到该页面后台接口地址，然后手动爬取数据。

	具体查看数据方式为：chrome-->检查-->network-->找到json文件
	（在左侧的搜索框过滤数据）-->点击右边的preview预览-->点击右面的headers查看地址然后给爬虫爬取。

		from urllib import request,parse
		import urllib
		import ssl
		ssl._create_default_https_context = ssl._create_unverified_context
		
		url = "https://movie.douban.com/j/chart/top_list?type=11&interval_id=100%3A90&action"
		# https://movie.douban.com/j/search_subjects?type=tv&tag=%E7%83%AD%E9%97%A8&sort=recommend&page_limit=20&page_start=0
		headers={"User-Agent": "Mozilla...."}
		
		# 变动的是这两个参数，从start开始往后显示limit个
		formdata = {
		    'start':'0',
		    'limit':'10'
		}
		data = parse.urlencode(formdata).encode()
		
		req = request.Request(url, data = data, headers = headers)
		response = request.urlopen(req)
		
		print(response.read().decode())

6. handler

	
	如果还需要更复杂的控制，比如通过一个Proxy去访问网站，我们需要利用ProxyHandler来处理：

	* HTTPPasswordMgrWithDefaultRealm（）类用来创建一个密码管理对象，用来保存HTTP请求相关的用户名和密码，主要应用两个场景：

		1. 验证代理授权的用户名和密码（ProxyBasicAuthHandler()）
		2. 验证Web客户端的用户名和密码（HTTPBasicAuthHandler()）


	* ProxyBasicAuthHandler（代理授权验证）

		有时候代理需要通过身份验证，需要改写代码：


		HTTPPasswordMgrWithDefaultRealm()：来保存私密代理的用户密码
		ProxyBasicAuthHandler()：来处理代理的身份验证。

		举例：


			import urllib.request
			 
			# 私密代理授权的账户
			user = "mr_mao_hacker"
			# 私密代理授权的密码
			passwd = "sffqry9r"
			# 私密代理 IP
			proxyserver = "61.158.163.130:16816"
			 
			# 1. 构建一个密码管理对象，用来保存需要处理的用户名和密码
			passwdmgr = urllib.request.HTTPPasswordMgrWithDefaultRealm()
			 
			# 2. 添加账户信息，第一个参数realm是与远程服务器相关的域信息，一般没人管它都是写None，后面三个参数分别是 代理服务器、用户名、密码
			passwdmgr.add_password(None, proxyserver, user, passwd)
			 
			# 3. 构建一个代理基础用户名/密码验证的ProxyBasicAuthHandler处理器对象，参数是创建的密码管理对象
			#   注意，这里不再使用普通ProxyHandler类了
			proxyauth_handler = urllib.request.ProxyBasicAuthHandler(passwdmgr)
			 
			# 4. 通过 build_opener()方法使用这些代理Handler对象，创建自定义opener对象，参数包括构建的 proxy_handler 和 proxyauth_handler
			opener = urllib.request.build_opener(proxyauth_handler)
			 
			# 5. 构造Request 请求
			request = urllib.request.Request("http://www.baidu.com/")
			 
			# 6. 使用自定义opener发送请求
			response = opener.open(request)
			 
			# 7. 打印响应内容
			print (response.read())

	* HTTPBasicAuthHandler处理器（Web客户端授权验证）

	![](https://i.imgur.com/2hZff5C.jpg)

	有些Web服务器需要（包括HTTP/FTP）访问时，需要进行用户身份验证，爬虫会报HTTP 401错误，表示访问身份未经授权

	如果我们有客户端的用户名和密码，我们可以通过下面的方法去访问爬取


		import urllib.request
		 
		# 用户名
		user = "test"
		# 密码
		passwd = "123456"
		# Web服务器 IP
		webserver = "http://192.168.199.107"
		 
		# 1. 构建一个密码管理对象，用来保存需要处理的用户名和密码
		passwdmgr = urllib.request.HTTPPasswordMgrWithDefaultRealm()
		 
		# 2. 添加账户信息，第一个参数realm是与远程服务器相关的域信息，一般没人管它都是写None，后面三个参数分别是 Web服务器、用户名、密码
		passwdmgr.add_password(None, webserver, user, passwd)
		 
		# 3. 构建一个HTTP基础用户名/密码验证的HTTPBasicAuthHandler处理器对象，参数是创建的密码管理对象
		httpauth_handler = urllib.request.HTTPBasicAuthHandler(passwdmgr)
		 
		# 4. 通过 build_opener()方法使用这些代理Handler对象，创建自定义opener对象，参数包括构建的 proxy_handler
		opener = urllib.request.build_opener(httpauth_handler)
		 
		# 5. 可以选择通过install_opener()方法定义opener为全局opener
		urllib.request.install_opener(opener)
		 
		# 6. 构建 Request对象
		request = urllib.request.Request("http://192.168.199.107")
		 
		# 7. 定义opener为全局opener后，可直接使用urlopen()发送请求
		response = urllib.request.urlopen(request)
		 
		# 8. 打印响应内容
		print (response.read())

	
	* opener是 urllib.request.OpenerDirector 的实例，我们之前一直都在使用的urlopen，它是一个特殊的opener（也就是模块帮我们构建好的）。
	* 但是基本的urlopen()方法不支持代理、cookie等其他的HTTP/HTTPS高级功能。所以要支持这些功能：

		1. 使用相关的 Handler处理器 来创建特定功能的处理器对象；
		2. 然后通过 urllib.request.build_opener()方法使用这些处理器对象，创建自定义opener对象；
		3. 使用自定义的opener对象，调用open()方法发送请求。

	* 创建一个opener（）


			# 构建一个HTTPHandler 处理器对象，支持处理HTTP请求
		   	# http_handler = request.HTTPHandler()
		   	
		   	# 构建一个HTTPHandler 处理器对象，支持处理HTTPS请求
		   	http_handler = request.HTTPSHandler()
		   	
		   	# 调用request.build_opener()方法，创建支持处理HTTP请求的opener对象
		   	opener = request.build_opener(http_handler)
		   	
		   	url='https://www.liepin.com/sh/zhaopin/pn1/?' \
		   	    'd_pageSize=40&siTag=&d_headId=7523ef4c1e412df5e007f3cfd117447d&d_ckId=7523ef4c1e412df5e007f3cfd117447d&d_sfrom=' \
		   	    'search_city&'
		   	str={
		   	    "key":"python",
		   	    "d_curPage":0
		   	
		   	}
		   	#
		   	url=url+parse.urlencode(str)
		   	
		   	print(url)
		   	# 构建 Request请求
		   	request = request.Request(url)
		   	
		   	# 调用自定义opener对象的open()方法，发送request请求
		   	f = opener.open(request)
		   	
		   	# 获取服务器响应内容
		   	with open('liepin.html','w+') as fp:
		   	    fp.write(f.read().decode())
		
		   >如果在 HTTPHandler()增加 debuglevel=1参数，还会将 Debug Log 打开，这样程序在执行的时候，会把收包和发包的报头在屏幕上自动打印出来，方便调试，有时可以省去抓包的工作。
		
		   	https_handler = urllib2.HTTPSHandler(debuglevel=1)

3. ProxyHandler处理器（代理设置）

  使用代理IP，这是爬虫/反爬虫的第二大招，通常也是最好用的。

  很多网站会检测某一段时间某个IP的访问次数(通过流量统计，系统日志等)，如果访问次数多的不像正常人，它会禁止这个IP的访问。

  所以我们可以设置一些代理服务器，每隔一段时间换一个代理，就算IP被禁止，依然可以换个IP继续爬取。

  免费的开放代理获取基本没有成本，我们可以在一些代理网站上收集这些免费代理，测试后如果可以用，就把它收集起来用在爬虫上面。

  免费短期代理网站举例：

  [西刺免费代理IP](http://www.xicidaili.com/)

  [快代理免费代理](http://www.kuaidaili.com/free/inha/)

  [Proxy360代理](http://www.proxy360.cn/default.aspx)

  [全网代理IP](http://www.goubanjia.com/free/index.shtml)


  **新建代理opener**

  	from urllib import request,parse
  	import urllib
  	import ssl
  	ssl._create_default_https_context = ssl._create_unverified_context
  	
  	# 构建了两个代理Handler，一个有代理IP，一个没有代理IP
  	httpproxy_handler = request.ProxyHandler({"http" : "110.73.1.105:8123"})
  	nullproxy_handler = request.ProxyHandler({})
  	
  	proxySwitch = True #定义一个代理开关
  	
  	# 通过 request.build_opener()方法使用这些代理Handler对象，创建自定义opener对象
  	# 根据代理开关是否打开，使用不同的代理模式
  	if proxySwitch:
  	    opener = request.build_opener(httpproxy_handler)
  	else:
  	    opener = request.build_opener(nullproxy_handler)
  	
  	request = request.Request("http://www.baidu.com/")
  	
  	# 1. 如果这么写，只有使用opener.open()方法发送请求才使用自定义的代理，而urlopen()则不使用自定义代理。
  	response = opener.open(request)
  	
  	# 2. 如果这么写，就是将opener应用到全局，之后所有的，不管是opener.open()还是urlopen() 发送请求，都将使用自定义代理。
  	# urllib2.install_opener(opener)
  	# response = urlopen(request)
  	print(response.read())

  如果代理IP足够多，就可以像随机获取User-Agent一样，随机选择一个代理去访问网站。

  	proxy_list = [
  	    {"http" : "110.73.1.105:8123"},
  	    {"http" : "110.73.40.20:8123"},
  	    {"http" : "124.88.67.81:80"},
  	    {"http" : "124.88.67.81:80"},
  	    {"http" : "124.88.67.81:80"}
  	]
  	
  	# 随机选择一个代理
  	proxy = random.choice(proxy_list)
  	httpproxy_handler = request.ProxyHandler(proxy)

# Requests

1. 介绍

	Requests 继承了urllib的所有特性。Requests支持HTTP连接保持和连接池，支持使用cookie保持会话，支持文件上传，支持自动确定响应内容的编码，支持国际化的 URL 和 POST 数据自动编码。

requests 的底层实现其实就是 urllib3

Requests的文档非常完备，中文文档也相当不错。Requests能完全满足当前网络的需求，支持Python 2.6—3.5，而且能在PyPy下完美运行。

[开源地址](https://github.com/kennethreitz/requests)

[中文文档 API](http://docs.python-requests.org/zh_CN/latest/index.html)

2. 安装

		pip install requests
	
3. get请求

		import requests

		url='https://www.liepin.com/sh/zhaopin/pn1/?' \
		    'd_pageSize=40&siTag=&d_headId=7523ef4c1e412df5e007f3cfd117447d&d_ckId=7523ef4c1e412df5e007f3cfd117447d&d_sfrom=' \
		    'search_city&'
		qs={
		    "key":"python",
		    "d_curPage":0
		
		}
		
		headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.99 Safari/537.36"}
		# params 接收一个字典或者字符串的查询参数，字典类型自动转换为url编码，不需要urlencode()
		response = requests.get(url, params = qs, headers = headers)
		
		# 查看响应内容，response.text 返回的是Unicode格式的数据
		print(response.text)
		# 查看响应内容，response.content返回的字节流数据
		print(response.content)
		
		# 查看完整url地址
		print(response.url)
		
		# 查看响应头部字符编码
		print(response.encoding)
		
		# 查看响应码
		print(response.status_code)
		#查看以一个 Python 字典形式展示的服务器响应头
		
		print(response.headers)
	
	>但是这个字典比较特殊：它是仅为 HTTP 头部而生的。根据 RFC 2616， HTTP 头部是大小写不敏感的。

	因此，我们可以使用任意大写形式来访问这些响应头字段：
	
		r.headers['Content-Type']
		r.headers.get('content-type')
	
3. post 请求

	response = requests.post（url, data = data)
	
	如果是json文件可以直接显示
	
		print(response.json())
	
	>如果 JSON 解码失败， r.json() 就会抛出一个异常。例如，响应内容是 401 (Unauthorized)，尝试访问 r.json() 将会抛出 ValueError: No JSON object could be decoded 异常。

	>需要注意的是，成功调用 r.json() 并**不**意味着响应的成功。有的服务器会在失败的响应中包含一个 JSON 对象（比如 HTTP 500 的错误细节）。这种 JSON 会被解码返回。要检查请求是否成功，请使用 r.raise_for_status() 或者检查 r.status_code 是否和你的期望相同。
	
4. 代理

	如果需要使用代理，你可以通过为任意请求方法提供 proxies 参数来配置单个请求
	
		import requests
	
		# 根据协议类型，选择不同的代理
		proxies = {
		  "http": "http://12.34.56.79:9527",
		  "https": "http://12.34.56.79:9527",
		}
		
		response = requests.get("http://www.baidu.com", proxies = proxies)
		print response.text
	
5. 处理HTTPS请求 SSL证书验证

	要想检查某个主机的SSL证书，你可以使用 verify 参数（也可以不写）
	
		import requests
		response = requests.get("https://www.baidu.com/", verify=True)
		
		# 也可以省略不写
		# response = requests.get("https://www.baidu.com/")
		print r.text
