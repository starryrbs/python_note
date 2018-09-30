##Python项目-Day43-爬虫-正则表达式-CSS-XML
1. 正则表达式

	正则表达式本身是一种小型的、高度专业化的编程语言，而在python中，
     通过内嵌集成re模块，程序媛们可以直接调用来实现正则匹配。
     正则表达式模式被编译成一系列的字节码，然后由用C编写的匹配引擎执行。

	[正则表达式复习](https://blog.csdn.net/qq_37892223/article/details/81366590)
2. 使用正则表达式

	1. 实际上爬虫一共就四个主要步骤：

		1. 明确目标 (要知道你准备在哪个范围或者网站去搜索)
		1. 爬 (将所有的网站的内容全部爬下来)
		1. 取 (去掉对我们没用处的数据)
		1. 处理数据（按照我们想要的方式存储和使用）


	2. 匹配中文

	在某些情况下，我们想匹配文本中的汉字，有一点需要注意的是，中文的 unicode 编	 码范围 主要在 [u4e00-u9fa5]，这里说主要是因为这个范围并不完整，比如没有包	 括全角（中文）标点，不过，在大部分情况下，应该是够用的。

	假设现在想把字符串 title = u'你好，hello，世界' 中的中文提取出来，可以这么做：


		import re
		str="中a国111打线"
		
		regex=ur'[\u4e00-\u9fa5]+'
		
		result=re.findall(regex,str)
		print(result)

	注意到，我们在正则表达式前面加上了两个前缀 ur，其中 r 表示使用原始字符串，u 表示是 unicode 字符串。但是在python3中默认编码为unicode所以u必须省略。
	
	执行结果:

		['中', '国', '打线']

	如果爬取的网页中有中文，可能会出现乱码。原因是网页的编码格式可能是GBK,我们可以这样

		gbk_html = html.decode('gbk').encode('utf-8') 

3. 案例一:解析淘宝数据
		
		#导入re正则表达式包
		import re
		#用来存储数据
		li=[]
		#打开爬取下来的html文件
		with open('taopage0.html','r+') as fp:
		    data=fp.read()
		#根据正则表达式匹配
		    plt = re.findall(r'\"view_price\"\: \"[\d\.]*\"', data)
		
		    # 在爬取下来的网页中查找物品
		    tlt = re.findall(r'\"raw_title\"\: \".*?\"', data)
		
		    loc=re.findall(r'\"item_loc\"\: \".*?\"', data)
			
		    for i in range(len(plt)):
		        price = eval(plt[i].split(':')[1])
		        title = eval(tlt[i].split(':')[1])
		        location = eval(loc[i].split(':')[1])
		
		        li.append([price,title,location])
		
		
		print(li)

4. XML (lxml+xpath爬取)

	1. 什么是XML?

		* XML 指可扩展标记语言（EXtensible Markup Language）
		* XML 是一种标记语言，很类似 HTML
		* XML 的设计宗旨是传输数据，而非显示数据
		* XML 的标签需要我们自行定义。
		* XML 被设计为具有自我描述性。
		* XML 是 W3C 的推荐标准

	2. 什么是XPath?

		XPath (XML Path Language) 是一门在 XML 文档中查找信息的语言，可用来在 XML 文档中对元素和属性进行遍历。
		
		XPath 开发工具

		- 开源的XPath表达式编辑工具:XMLQuire(XML格式文件可用)
		- Chrome插件 XPath Helper
		- Firefox插件 XPath Checker

	3. XML示例

			<?xml version="1.0" encoding="utf-8"?>

			<bookstore> 
			
			  <book category="cooking"> 
			    <title lang="en">Everyday Italian</title>  
			    <author>Giada De Laurentiis</author>  
			    <year>2005</year>  
			    <price>30.00</price> 
			  </book>  
			
			  <book category="children"> 
			    <title lang="en">Harry Potter</title>  
			    <author>J K. Rowling</author>  
			    <year>2005</year>  
			    <price>29.99</price> 
			  </book>  
			
			  <book category="web"> 
			    <title lang="en">XQuery Kick Start</title>  
			    <author>James McGovern</author>  
			    <author>Per Bothner</author>  
			    <author>Kurt Cagle</author>  
			    <author>James Linn</author>  
			    <author>Vaidyanathan Nagarajan</author>  
			    <year>2003</year>  
			    <price>49.99</price> 
			  </book> 
			
			  <book category="web" cover="paperback"> 
			    <title lang="en">Learning XML</title>  
			    <author>Erik T. Ray</author>  
			    <year>2003</year>  
			    <price>39.95</price> 
			  </book> 
			
			</bookstore>

	> 安装lxml

		pip install lxml

	4. 常用的方法

		1. etree.parse()

			读取xml文件,结果为**xml对象**(不是字符串)

		2. etree.HTML(string_html)

			将字符串形式的html文件转换为xml对象

		3. etree.toString(htmlelement,encoding="utf-8").decode("utf-8")

				etree.tostring(html,encoding="utf-8", pretty_print=True).decode()

				解决中文显示问题
	5. 选择器

		|表达式|	描述|
		|---|---|---|
		|nodename|	选取此节点的所有子节点。|
		|/	|从根节点选取。|
		|//	|从匹配选择的当前节点选择文档中的节点，而不考虑它们的位置。|
		|.	|选取当前节点。|
		|..	|选取当前节点的父节点。|
		|@	|选取属性。|
		
		范例
		
			bookstore	选取 bookstore 元素的所有子节点(如果只有一个的话)。
			/bookstore	选取根元素 bookstore。注释：假如路径起始于正斜杠( / )，则此路径始终代表到某元素的绝对路径！
			bookstore/book	选取属于 bookstore 的直接子元素的所有 book 元素。
			//book	选取所有 book 子元素，而不管它们在文档中的位置。
			bookstore//book	选择属于 bookstore 元素的后代的所有 book 元素，而不管它们位于 bookstore 之下的什么位置。
			bookstore//book/@lang	选取book元素的lang属性值。
			bookstore//book[@class="book-css"]/title	选取class属性值为“book-css”的book元素的title。
			//*[@class="bold"] 获取 class 值为 bold 的标签名
		
		**使用属性时，不要忘记@符号**
		> /表示直接子元素，//表示所有子孙元素
		
		
		读取案例-xml
		
			#from lxml import etree #这样写后面会出现红色波浪线
			
			import lxml.html
			etree = lxml.html.etree
			# 读取文件：这个时候只时候读取xml格式的文件，显然局限性太强！！！！！
			html = etree.parse('data.xml')
			# 转化为字节字符串
			# result = etree.tostring(html, pretty_print=True)
			# print(type(html))  # 显示etree.parse() 返回类型
			# print(result)
			titles = html.xpath('/bookstore/book/title')
			
			for tt in titles:
			    print(tt.text)
			
			# 如果不是直接子元素就要用//
	
			titles = html.xpath('/bookstore//title')
			
			for tt in titles:
			    print(tt.text)
	6. lxml读取html文件
		​	
		自己创建html解析器，增加parser参数
		
			import lxml.html
			etree = lxml.html.etree
			parser = etree.HTMLParser(encoding="utf-8")
			htmlelement = etree.parse("liepin.html", parser=parser)
			print(htmlelement)
			html_string=etree.tostring(htmlelement, encoding="utf-8").decode("utf-8")
			
			#读取innerText
			links=htmlelement.xpath('//div/div/span/a')
	
			for link in links:
			    print(link.text)
			    
			#读取属性的值
			
			with open('liepin.html','r+') as fp:
			    content=fp.read()
			    html=etree.HTML(content)
			    links = html.xpath('//div/div/span/@title')
			    for title in titles:
			        print(title)


3. BeautifulSoup4

	lxml 只会局部遍历，而Beautiful Soup 是基于HTML DOM的，会载入整个文档，解析整个DOM树，因此时间和内存开销都会大很多，所以性能要低于lxml。

	BeautifulSoup 用来解析 HTML 比较简单，API非常人性化，支持CSS选择器、Python标准库中的HTML解析器，也支持 lxml 的 XML解析器。

	Beautiful Soup 3 目前已经停止开发，推荐现在的项目使用Beautiful Soup 4。使用 pip 安装即可：pip install beautifulsoup4

	> 安装 

		pip install beautifulsoup4

	2. tag (可以使用文档对象直接.标签名获取)

			from bs4 import BeautifulSoup

			# html='....'
			#创建 Beautiful Soup 对象
			# soup = BeautifulSoup(html)
			
			#打开本地 HTML 文件的方式来创建对象
			soup = BeautifulSoup(open('data.xml'),"lxml")
			
			#格式化输出 soup 对象的内容
			# print(soup.prettify())
			print(soup.book) 
		
		>我们可以利用 soup 加标签名轻松地获取这些标签的内容，这些对象的类型是bs4.element.Tag。但是注意，它查找的是在所有内容中的第一个符合要求的标签。
print(soup.book)
	3. 对于 Tag，它有两个重要的属性，是 name 和 attrs

			from bs4 import BeautifulSoup
			
			# html='....'
			#创建 Beautiful Soup 对象
			# soup = BeautifulSoup(html)
			
			#打开本地 HTML 文件的方式来创建对象
			soup = BeautifulSoup(open('liepin.html'),"lxml")
			
			#格式化输出 soup 对象的内容
			# print(soup.prettify())
			
			nodes=soup.select('div.company-info p a')
			
			nodes=soup.select('div#div01 div.company-info > p[name="pr"] a')
			
			for node in nodes:
			    #获取节点名称
			    print(node.name)
			
			    #获取节点所有属性
			    print(node.attrs)
			
			    #获取节点href属性的值
			    print(node['href'])
			    # print(node.get('href'))

			    
			    #获取节点的值
			    print(node.string)		