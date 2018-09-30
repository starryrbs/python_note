##使用requests爬取易物天下商品类型实战
1. 确定要爬取的数据

	1. 爬取的是首页的行业分类
	2. 确定数据来源

		* 先使用requests.get方法获取网页并没有行业分类

				response = requests.get(url, params = qs, headers = headers)

		* 有可能数据是通过发送ajax获取来的

			浏览器打开网址,右键检查,选择network,发现果然是通过ajax发送来请求数据

2. 开始爬取数据

	* 因为数据是通过ajax请求的,所以我直接把浏览器上所有的Request.headers中的所有字段拷贝下来,变成一个字典

			headers={
			
            "Accept": "application/json, text/javascript, */*; q=0.01",
			'Accept-Encoding': "gzip, deflate",
			'Accept-Language': 'zh-CN,zh;q=0.9',
			'Connection': 'keep-alive',
			'Content-Length': '4',
			'Content-Type': 'application/x-www-form-urlencoded',
			'Cookie': 'JSESSIONID=C7BD7DFF7031A1A7EE3B71336BE03419; gr_user_id=47edb7df-b13e-4c2c-8c0c-0db4c28f09ff; Hm_lvt_10bdb52fd1832ac4eeceeabdc4df132f=1537604218; Hm_lpvt_10bdb52fd1832ac4eeceeabdc4df132f=1537608109; gr_session_id_a08ca0a390ddd043=9646c1ab-1d0c-41be-819e-51a04b592b26; gr_session_id_a08ca0a390ddd043_9646c1ab-1d0c-41be-819e-51a04b592b26=true',
			'Host': 'www.i1515.com',
			'Origin': 'http://www.i1515.com',
			'Referer': 'http://www.i1515.com/',
			'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.92 Safari/537.36',
			'X-Requested-With': 'XMLHttpRequest'
			
			        }

	* 查看是否Form Data中是否有字段,如果有,转化成字典

			data={
			    "id":"1"
			}
	* 最后我发现网站一共发送12次ajax请求,并且每一次的id不同,所以我只需要通过循环来发送请求,将数据暂时存储在json文件中

			for i in range(1,12):
			    data["id"]=str(i)
			    try:
			        response = requests.post(url=url, headers=headers, data=data)
			        print(i)
			        print(type(response.json()))
			        result=response.json()
			        print(type(response.json())=="dict")
			        if type(response.json())==type({}):
			            print(response.json())
			            with open('type{}.json'.format(i),'w',encoding='utf-8') as f:
			                json.dump(result,f,ensure_ascii=False)
			                f.close()
			    except Exception as ex:
			        print(ex)

3. 将json文件中的数据存储到数据库中

	* 循环遍历每个文件

			with open('myspiders/type{}.json'.format(index), 'r', encoding='utf-8') as f:

	* 打开数据库

			conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='',
		                                   db='orsp', charset='utf8')

	* 最后插入数据

##源码

* 爬虫test.py

		import requests
		import json
		url='http://www.i1515.com/v2/category/getOtherCategory.html'
		headers={
		
		            "Accept": "application/json, text/javascript, */*; q=0.01",
		'Accept-Encoding': "gzip, deflate",
		'Accept-Language': 'zh-CN,zh;q=0.9',
		'Connection': 'keep-alive',
		'Content-Length': '4',
		'Content-Type': 'application/x-www-form-urlencoded',
		'Cookie': 'JSESSIONID=C7BD7DFF7031A1A7EE3B71336BE03419; gr_user_id=47edb7df-b13e-4c2c-8c0c-0db4c28f09ff; Hm_lvt_10bdb52fd1832ac4eeceeabdc4df132f=1537604218; Hm_lpvt_10bdb52fd1832ac4eeceeabdc4df132f=1537608109; gr_session_id_a08ca0a390ddd043=9646c1ab-1d0c-41be-819e-51a04b592b26; gr_session_id_a08ca0a390ddd043_9646c1ab-1d0c-41be-819e-51a04b592b26=true',
		'Host': 'www.i1515.com',
		'Origin': 'http://www.i1515.com',
		'Referer': 'http://www.i1515.com/',
		'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.92 Safari/537.36',
		'X-Requested-With': 'XMLHttpRequest'
		
		        }
		
		data={
		    "id":"1"
		}
		for i in range(1,12):
		    data["id"]=str(i)
		    try:
		        response = requests.post(url=url, headers=headers, data=data)
		        print(i)
		        print(type(response.json()))
		        result=response.json()
		        print(type(response.json())=="dict")
		        if type(response.json())==type({}):
		            print(response.json())
		            with open('type{}.json'.format(i),'w',encoding='utf-8') as f:
		                json.dump(result,f,ensure_ascii=False)
		                f.close()
		    except Exception as ex:
		        print(ex)

* 将数据写入到数据库中的write_data.py


		import json
		import pymysql
		for index in range(1,12):
		    try:
		        with open('myspiders/type{}.json'.format(index), 'r', encoding='utf-8') as f:
		            data = json.load(f)
		            print(data["name"])
		            conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='',
		                                   db='orsp', charset='utf8')
		            # 建立游标对象
		            cursor = conn.cursor()
		
		            # 先查出name对应的id
		            sql_id_Byname = 'SELECT id FROM product_type WHERE product_type="{}"'.format(data["name"])
		            cursor.execute(sql_id_Byname)
		            res_id = cursor.fetchone()
		            res_id = res_id[0]
		            print(res_id)
		            # 再插入二级类型
		            for i in range(len(data["sCate"])):
		                sql_insert_two = "INSERT INTO `product_type_two` (`product_type_one_id`, `type_two_name`) VALUES ('{0}', '{1}')"
		                two_type = data["sCate"][i]["name"]
		                print("two_type", two_type)
		                sql_insert_two = sql_insert_two.format(res_id, two_type)
		                print(sql_insert_two)
		                cursor.execute(sql_insert_two)
		                insert_id = conn.insert_id()
		                print("insert_id", insert_id)
		                three_data = data["sCate"][i]["tCategorys"]
		                for j in three_data:
		                    print(j["name"])
		                    sql_insert_three = "INSERT INTO `product_type_three` (`product_type_two_id`, `type_three_name`) VALUES ({0}, '{1}')"
		                    sql_insert_three = sql_insert_three.format(insert_id, j["name"])
		                    print(sql_insert_three)
		                    cursor.execute(sql_insert_three)
		
		            conn.commit()
		    except Exception as ex:
		        print(ex)


