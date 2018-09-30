##Python项目-Day45-Scrapy
1. 安装scrapy

	先安装twisted

		pip install twisted

	再安装scrapy

		pip install Scrapy

	中途遇到pywin32错误

	安装pypiwin32

		pip install pypiwin32


2. scrapy学习网址

	[Scrapy框架官方网址](http://doc.scrapy.org/en/latest)

	[Scrapy中文维护站点](http://scrapy-chs.readthedocs.io/zh_CN/latest/index.html)

3. scrapy的项目结构

		scrapy.cfg
		myproject/
		    __init__.py
		    items.py
		    pipelines.py
		    settings.py
		    spiders/
		        __init__.py
		        spider1.py
		        spider2.py

	scrapy.cfg:存放的目录被认为是项目的根目录,项目的配置文件。

	myproject:项目的Python模块，将会从这里引用代码
	
	items.py:定义了储存数据的字段名，在编辑此文件前需先分析要提取那些信息，定义好名称即可。

	pipelines.py:此文件是用来处理提取的数据的，可以将数据转存为其他格式或数据库中,如果要启用此文件需要先在settings.py中指明pipelines.py中的类，并且如果有多个类的话还要定义优先级，就是后面的数字，越小优先级越高， 在每个pipeline类中必有一个process_item的函数，此函数是数据处理的具体流程。

	settings.py:一些项目的设置


	1. 创建项目

			scrapy startproject myproject

	2. 创建一个新的spider


			scrapy genspider mydomain mydomain.com
			#注意:填写是它的域名
			scrapy genspider csdnSpider download.csdn.net

		创建完毕之后,就会在spiders目录下生成一个csdnSpider.py的文件

			import scrapy
			
			
			class CsdnspiderSpider(scrapy.Spider):
			    name = 'csdnSpider'
			    allowed_domains = ['download.csdn.net']
			    start_urls = ['http://download.csdn.net/']
			
			    def parse(self, response):
			        pass

		1. name = "" ：这个爬虫的识别名称，必须是唯一的，在不同的爬虫必须定义不同的名字。
		2. allow_domains = [] 是搜索的域名范围，也就是爬虫的约束区域，规定爬虫只爬取这个域名下的网页，不存在的URL会被忽略。
		3. start_urls = () ：爬取的URL元祖/列表。爬虫从这里开始抓取数据，所以，第一次下载的数据将会从这些urls开始。其他子URL将会从这些起始URL中继承性生成。
	
		4. parse(self, response) ：解析的方法，每个初始URL完成下载后将被调用，调用的时候传入从每一个URL传回的Response对象来作为唯一参数，主要作用如下：


			负责解析返回的网页数据(response.body)，提取结构化数据(生成item)
		生成需要下一页的URL请求。

	3. 查看所有爬虫

			scrapy list

		* 执行爬虫,并把结果保存到指定文件

				scrapy crawl ziyuanSpider -o taobo.json
		* 利用命令行住区指定URL的代码

				scrapy fetch https://s.taobao.com/list?q=iphone

	4. 安装ipython

		种交互式计算和开发环境,使命令行更加方便和清爽

			pip install ipython

	5. scrapy shell 命令
		
		一般是在写爬虫之前用来测试代码的

		* 进入scrapy shell
	
				scrapy shell "http://www.runoob.com/"
				# xpath工具
				response.xpath('//div[@class="col nav"]/ul/li')
				# css工具
				response.css("div[class='col nav']")
		
4. 完整的scrapy的Demo

	树结构
	
	![](https://i.imgur.com/pZyoO49.jpg)

	* runoobSpider.py

			# -*- coding: utf-8 -*-
			import scrapy
			from myspiders.items import RunnoobItem
			
			class RunoobspiderSpider(scrapy.Spider):
			    name = 'runoobSpider'#爬虫的识别名称
			    allowed_domains = ['runoob.com']#搜索范围,规定只搜索该域名下的所有网址
			    start_urls = ['http://www.runoob.com/']
				#爬取的URL列表
			    def parse(self, response):
			        print('***********')
			        links=response.xpath('//div[@class="col nav"]/ul/li')
					#使用xpath选择器来选择元素
			        items=[]
			        for link in links:
						#创建一个items对象
			            item=RunnoobItem()
			            item['href']=link.xpath('a/@href').extract()
			            item['title']=link.xpath('a/text()').extract()
						#交给管道pipelines去处理数据
			            yield item
			        #     items.append(item)
			        # return items

	* items.py


	
			import scrapy
			from scrapy.item import Item,Field
			
			class MyspidersItem(scrapy.Item):
			    # define the fields for your item here like:
			    # name = scrapy.Field()
			    pass
			
			class RunnoobItem(scrapy.Item):
			    href=Field()#域,也可以说是存储数据的一个变量
			    title=Field()
			    desc=Field()

	* pipelines.py

			class MyspidersPipeline(object):
			    def process_item(self, item, spider):
			        # return item
			        print("**********pipelines******")
			        print(item)
			class TestPipeline(object):
			    def process_item(self, item, spider):
			        # return item
			        print("??????????test******")
			        print(item)

			#要开启TestPipeline,需要在settings里面设置


	* settings.py


			ITEM_PIPELINES = {
			   'myspiders.pipelines.MyspidersPipeline': 300,
	
				#加上这一句,400是优先级的意思,越小越优先
	
			   'myspiders.pipelines.TestPipeline': 400,
			}