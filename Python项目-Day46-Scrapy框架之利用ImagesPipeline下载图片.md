##Python项目-Day46-Scrapy框架之利用ImagesPipeline下载图片
1. 确定下载的图片

	找到图片的url并存在items

		item['img'] = link.select('div/a/img/@data-original').extract()[0]	

	> 这里找图片的src时会有一个问题,明明在浏览器中使用检查看到图片上是有src属性的,但是用scrapy shell去取的时候并没有src属性,这是因为srcapy爬取的response中并没有src


	这是浏览器检查时看到的,是有src的

		<img class="thumb" style="width: 253px; height: 169px; display: inline;"
		 data-original="https://www.ziyuan.tv/wp-content/themes/Git-alpha/timthumb.php?src=https://www.ziyuan.tv/wp-content/uploads/2015/02/162931fJ7.png&amp;h=169&amp;w=253&amp;q=90&amp;zc=1&amp;ct=1" 
		alt="圆梦站长网源码,DEDECMS内核,站长资源下载站源码,站长类站点源码" 
		src="https://www.ziyuan.tv/wp-content/themes/Git-alpha/timthumb.php?src=https://www.ziyuan.tv/wp-contentuploads/2015/02/162931fJ7.png&amp;h=169&amp;w=253&amp;q=90&amp;zc=1&amp;ct=1">

	但是,其实源代码是这样的:

		<img class="thumb" style="width:253px;height:169px" 
		data-original="https://www.ziyuan.tv/wp-content/themes/Git-alpha/timthumb.php?src=https://www.ziyuan.tv/wp-content/uploads/2015/02/162931fJ7.png&h=169&w=253&q=90&zc=1&ct=1" 
		alt="圆梦站长网源码,DEDECMS内核,站长资源下载站源码,站长类站点源码" />

	解决方法:
	
		可以使用data-origina代替src(最简单的方法)

2. 取到图片的url之后,交给管道处理

	* 新建一个类GetImagePipeline(注意一定要继承ImagesPipeline)

		from scrapy.pipelines.images import ImagesPipeline

	* 可以事先在另一个管道先进行数据清理.

	* 定义请求的request的headers
			
			default_headers = {
			        'accept': 'image/webp,image/*,*/*;q=0.8',
			        'accept-encoding': 'gzip, deflate, sdch, br',
			        'accept-language': 'zh-CN,zh;q=0.8,en;q=0.6',
			        'cookie': 'bid=yQdC/AzTaCw',
			        'referer': '',
			        'user-agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/52.0.2743.116 Safari/537.36',
			    }

	* 重写file_path方法,定义图片的文件名

		    def file_path(self, request, response=None, info=None):
		        print("执行了file_path方法")
		        item = request.meta['item']
		        folder = item['title']
		        # folder_strip = self.strip(folder)
		        image_guid = request.url.split('/')[-1]
		        filename = u'full/{0}/{1}'.format(folder, image_guid)
		        return filename

		其中meta是用来在两个方法之间传递参数的

	* 重写get_media_requests方法来请求图片

		    def get_media_requests(self, item, info):
		        print("执行了get_media_requests")
		        referer = item['img']
		        self.default_headers['referer'] = referer
		        yield Request(item['img'], headers=self.default_headers, meta={'item': item, 'referer': referer})
	* 重写item_completed方法完成了图片

		    def item_completed(self, results, item, info):
		        print("--------results-------")
		        print(results)
		        print("执行了item_completed方法")
		
		        image_paths = [x['path'] for ok, x in results if ok]
		        if not image_paths:
		            raise DropItem("Item contains no images")
		        return item

		results是一个元组列表

			[(True, {'url': 'https://www.ziyuan.tv/wp-content/themes/Git-alpha/timthumb.php?src=https://www.ziyuan.tv/wp-content/uploads/2018/05/aa9c9f7dd639cc0262d9eb583398abc1-4.png&h=169&w=
			253&q=90&zc=1&ct=1', 'path': "full/['爱搜资源网整站源码清新蓝调模板后台地址 admin1 账号刘小顺 520 密码 lzs128451此处内容已经被作者隐藏，请输入验证码查看内容验证码：请关注本站微信公
			众号，回复“验证码”，获取验证码。在微信里搜索“ 小说骑士”或者“ziyuan_tv”或者微信扫描右侧二维码都可以关注本站微信公众号。此处内容已经被作者隐藏，请输入验证码查看内容验……']/aa9
			c9f7dd639cc0262d9eb583398abc1-4.png&h=169&w=253&q=90&zc=1&ct=1", 'checksum': '67b69ec35fa370d03ed9a314252821f3'})]

	* 最后,需要在settings.py中进行设置


			#设置图片的下载路径
			IMAGES_STORE = r'D:\images'
			#设置图片的过期天数,30天内不再重复抓取
			IMAGES_EXPIRES = 30
			#大图和小图
			IMAGES_THUMBS = {
					    'big': (270, 270),
					    'small': (80, 80)
					}

3. 项目代码

	* items.py

			import scrapy
			from scrapy.item import Item,Field
			class ZiyuanItem(scrapy.Item):
			    href=Field()#域
			    title=Field()
			    date=Field()
			    resourse_type=Field()
			    img=Field()
			    image_paths = Field()


	* ziyuanSpider.py

			import scrapy
			from urllib import parse
			import string
			from myspiders.items import ZiyuanItem
			class ZiyuanspiderSpider(scrapy.Spider):
			    name = 'ziyuanSpider'
			    allowed_domains = ['ziyuan.tv']
			    start_urls = ["https://www.ziyuan.tv/yuanma/"]
			    custom_settings = {
			        # 'SOME_SETTING': 'some value',
			        "ITEM_PIPELINES":{
			            # 'myspiders.pipelines.ResPipeline': 400,
			            'myspiders.imagePipelines.ImagePipeline': 400,
			            'myspiders.imagePipelines.GetImagePipeline': 500,
			        }
			    }
			
			    def start_requests(self):
			        url_s = "https://www.ziyuan.tv/"
			        query={
			            "search":"资源",
			        }
			
			        for i in range(1,3):
			            url = url_s + "search" + '/' + query["search"] + '/page/' + str(i)
			            url = parse.quote(url, safe=string.printable)
			            print(url)
			            yield scrapy.FormRequest(url=url,callback=self.parse)
			
			    def parse(self, response):
			        print("开始解析数据")
			        links=response.xpath('//div[@class="card-item"]')
			        items=[]
			        for link in links:
			            item = ZiyuanItem()
			            item['title'] = link.xpath('p/text()').extract()[0]
			            item['href'] = link.xpath('div/a/@href').extract()[1]
			            item['date'] = link.xpath('div[@class="cardpricebtn"]/text()').extract()
			            item['resourse_type'] = link.xpath('.//a[@class="metacat"]/text()').extract()
			            item['img'] = link.select('div/a/img/@data-original').extract()[0]
			
			            print("-------------------")
			            print("item:",item)
			
			            items.append(item)
			            yield item
			        print("回来-----------------")
			        return items

		* settings.py

				#设置图片下载路径
				IMAGES_STORE = r'D:\images'
				IMAGES_EXPIRES = 30
				IMAGES_THUMBS = {
						    'big': (270, 270),
						    'small': (80, 80)
						}

		* imagePipelines

				# Define your item pipelines here
				#
				# Don't forget to add your pipeline to the ITEM_PIPELINES setting
				# See: https://doc.scrapy.org/en/latest/topics/item-pipeline.html
				import pymysql
				import json
				import re
				from scrapy import Request
				from scrapy.exceptions import DropItem
				from scrapy.pipelines.images import ImagesPipeline
				# class MyspidersPipeline(object):
				#     def process_item(self, item, spider):
				#         # return item
				#         print("**********pipelines******")
				#         print(1,item)
				#         with open("href.json",'w') as f:
				#             json.dump({"href":item["href"]},f)
				#         return item
				#     def open_spider(self,spider):
				#         print('open--------------')
				#     def close_spider(self,spider):
				#         print('close--------------')
				# json.dump(ensure_ascii=False)
				#ensure_ascii不要转化成ascii码
				
				# 存储资源的基本信息
				class ImagePipeline(object):
				
				
				    def process_item(self, item, spider):
				        if spider.name == "ziyuanSpider":
				            print("执行了process_item方法")
				            return item
				
				
				
				
				
				class GetImagePipeline(ImagesPipeline):
				    default_headers = {
				        'accept': 'image/webp,image/*,*/*;q=0.8',
				        'accept-encoding': 'gzip, deflate, sdch, br',
				        'accept-language': 'zh-CN,zh;q=0.8,en;q=0.6',
				        'cookie': 'bid=yQdC/AzTaCw',
				        'referer': '',
				        'user-agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/52.0.2743.116 Safari/537.36',
				    }
				    id=0
				    def file_path(self, request, response=None, info=None):
				        print("执行了file_path方法")
				        item = request.meta['item']
				        folder = item['title'].strip()[0:5]
				        # folder_strip = self.strip(folder)
				        image_guid = re.findall(r'/(\w*)\.[jpg,png]',request.url)[1]
				        filename = u'full/{0}/{1}'.format(folder,image_guid+".jpg")
				        print("filename",filename)
				        return filename
				
				    def get_media_requests(self, item, info):
				        print("执行了get_media_requests")
				        referer = item['img']
				        self.default_headers['referer'] = referer
				        yield Request(item['img'], headers=self.default_headers, meta={'item': item, 'referer': referer})
				
				    #
				    def item_completed(self, results, item, info):
				        print("--------results-------")
				        print(results)
				        print("执行了item_completed方法")
				
				        image_paths = [x['path'] for ok, x in results if ok]
				        if not image_paths:
				            raise DropItem("Item contains no images")
				        item['image_paths'] = image_paths
				        return item