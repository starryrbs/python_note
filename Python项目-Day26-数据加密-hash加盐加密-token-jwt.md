##Python项目-Day26-数据加密-hash加盐加密-token-jwt
1. 数据加密

		import hashlib

		pwd='a123456'
		#sha1的参数必须是二进制
		temp=hashlib.sha1(pwd.encode())
		
		print(temp.hexdigest())

2. hash加盐加密

	1. 导入加密函数

			from werkzeug.security import generate_password_hash,check_password_hash

	2. 密码生成函数：generate_password_hash
		
			werkzeug.security.generate_password_hash(password, method='pbkdf2:sha1:2000', salt_length=8)
			
		参数说明：

		* password：明文密码
		* method：哈希加密的方法（需要hashlib库支持的），格式为pdpdf2:<method>[:iterations] 
		* method：哈希的方式，一般为SHA1
		* iterations：（可选参数）迭代次数，默认为1000
		* salt_length：盐值的长度，默认为8
	
		加密之后的字符串格式：

			method$salt$hash
	3. 密码验证函数：check_password_hash
		函数定义：
		
			werkzeug.security.check_password_hash(pwhash, password)
		参数定义：
		
		pwhash：generate_password_hash生成的哈希字符串
		password：需要验证的明文密码

		>check_password_hash函数用于验证经过generate_password_hash哈希的密		码 。若密码匹配，则返回真，否则返回假。
		实例:

			from werkzeug.security import generate_password_hash,check_password_hash
			import hashlib
			pwd='123456'
			hash_pwd=generate_password_hash(pwd,method='pbkdf2:sha1:2000',salt_length=8)
			print(check_password_hash(hash_pwd,pwd))

3. token

	JWT的声明一般被用来在身份提供者和服务提供者间传递被认证的用户身份信息，以便于从资源服务器获取资源。

	 **流程是这样的**

	1. 用户使用用户名密码请求服务器
	1. 服务器进行验证用户信息
	1. 服务器通过验证发送给用户一个token
	1. 客户端存储token，并在每次请求时附加这个token值
	1. 服务器验证token，并返回数据


4. JWT构成

	JWT由三部分构成

	例如:
	
		eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJVc2VySWQiOjEyMywiVXNlck5hbWUiOiJhZG1pbiJ9.Qjw1epD5P6p4Yy2yju3-fkq28PddznqRj3ESfALQy_U


	第一部分我们称它为头部（header）第二部分我们称其为载荷（payload，类似于飞机上承载的物品），第三部分是签证（signature）

	1. header
	
		* jwt的头部承载两部分信息：
		
			> 声明类型，这里是jwt
	
			> 声明加密的算法 通常直接使用 HMAC SHA256
	
		完整的头部就像下面这样的JSON：
	
			{
			  'typ': 'JWT',
			  'alg': 'HS256'
			}

	2. plyload

		载荷就是存放有效信息的地方。这个名字像是特指飞机上承载的货品，这些有效信息包含三个部分
	
		标准中注册的声明
		公共的声明
		私有的声明 
		标注中注册的声明（建议不强制使用）
		
		iss：jwt签发者
		sub：jwt所面向的用户
		aud：接收jwt的一方
		exp：jwt的过期时间，这个过期时间必须大于签发时间
		nbf：定义在什么时间之前，该jwt都是不可用的
		iat：jwt的签发时间
		jti：jwt的唯一身份标识，主要用来作为一次性token，从而回避重放攻击 
		公共的声明：
		
		公共的声明可以添加任何的信息，一般添加用户的相关信息或其它业务需要的必要信息，但不建议添加敏感信息，因为该部分在客户端可解密；
		
		私有的声明
		
		私有的声明是提供者和消费者功能定义的声明，一般不建议存放敏感信息，因为base64是对称解密的，意味着该部分信息可以归类为名文信息。
		
		定义一个payload

			{
			  "sub": "1234567890",
			  "name": "John Doe",
			  "admin": true
			}
	    然后将其base64加密，得到jwt的一部分
	
			eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9
	Signature
	
	    jwt的第三部分是一个签证信息，这个签证信息由三部分组成：
	
		header(base64后的)
		payload(base64后的)
		secred     
		
		这个部分需要base64加密后的header和base64加密后的payload使用“.”连接组成的字符串，然后通过header中声明的加密方式进行加secret组合加密，然后就构成了jwt的第三部分
	
	      
	
			var encodedString = base64UrlEncode(header) + '.' + base64UrlEncode(payload);
			var signature = HMACSHA256(encodedString, 'secret'); // TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
	    将这三部分用“.”连接成一个完整的字符串，构成了最终的jwt：
	
			eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
			
	     注意：secret是保存在服务器端的，jwt的签发也是在服务端的，secret就是用来进行jwt的签发和jwt的验证，所以它就是你服务端的私钥，在任何场景都不应该流露出去，一旦客户端得知这个secret，那就意味着客户端可以自我签发jwt了

	3. 总结

      优点：

		因为json的通用性，所以JWT是可以跨语言支持的，像C#，JavaScript，NodeJS，PHP等许多语言都可以使用
		因为由了payload部分，所以JWT可以在自身存储一些其它业务逻辑所必要的非敏感信息
		便于传输，jwt的构成非常简单，字节占用很小，所以它是非常便于传输的
		它不需要在服务端保存会话信息，所以它易于应用的扩展
       安全相关

		不应该在jwt的payload部分存储敏感信息，因为该部分是客户端可解密的部分
		保护好secret私钥。该私钥非常重要
		如果可以，请使用https协议
		
=====
# pyjwt
	
1. 安装

			pip install pyjwt -i https://pypi.tuna.tsinghua.edu.cn/simple

2. 生成token

		import jwt
		import datetime
		import hashlib
		
		#当前时间加上180秒，意味着token过期时间为3分钟以后
		datetimeInt = datetime.datetime.utcnow() + datetime.timedelta(seconds=180)
		SECRECT_KEY = 'secret'
		option = {
				  'iss':'jobapp.com', #token的签发者
		        'exp':datetimeInt, #过期时间
		        'aud': 'webkit',   #token的接收者，这里指定为浏览器
		        'user_id': '001'   #放入用户信息，唯一标识，解析后可以使用该消息
		    }
		# encoded2 = jwt.encode(payload=option,key= SECRECT_KEY, algorithm='HS256')
		#这时token类型为字节类型，如果传个前端要进行token.decode()
		token = jwt.encode(option,SECRECT_KEY, 'HS256')
		print(token)
		
3. 解析token

		decoded = jwt.decode(token, SECRECT_KEY,audience='webkit', algorithms=['HS256'])

		print(decoded)
		
4. 代码封装

			
			# 生成jwt 信息
			def  jwtEncoding(some,aud='webkit'):
			    datetimeInt = datetime.datetime.utcnow() + datetime.timedelta(seconds=180)
			    print(datetimeInt)
			    option = {
			        'exp':datetimeInt,
			        'aud': aud,
			        'some': some
			    }
			    encoded2 = jwt.encode(option, SECRECT_KEY, algorithm='HS256')
			    return encoded2
			    
			# 解析jwt 信息
			def  jwtDecoding(token,aud='webkit'):
			    decoded = None
			    try:
			        decoded = jwt.decode(token, SECRECT_KEY, audience=aud, algorithms=['HS256'])
			    except jwt.ExpiredSignatureError :
			        print("erroing.................")
			        decoded = {"error_msg":"is timeout !!","some":None}
			    except Exception:
			        decoded ={"error_msg":"noknow exception!!","some":None}
			        print("erroing2.................")
			    return decoded
			    



	