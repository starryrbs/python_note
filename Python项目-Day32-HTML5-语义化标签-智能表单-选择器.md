##Python项目-Day32-HTML5-语义化标签-智能表单-选择器
1. HTML5是什么?

	HTML5是一个新的网络标准，目标是取代现有的HTML 4.01和XHTML 1.0 标准。它希望能够减少互联网富应用（RIA)对Flash、Silverlight、JavaFX等的依赖，并且提供更多能有效增强网络应用的API。

	HTML5的标识

		<!DOCTYPE html>#该句为HTML5标识
		<html lang="en">
		<head>
		    <meta charset="UTF-8">


2. meta标签

	* meta标签的作用


		\<meta> 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。
		
		\<meta> 标签位于文档的头部，不包含任何内容。<meta> 标签的属性定义了与文档相关联的名称/值对。
	

	* HTML 与 XHTML 之间的差异

		在 HTML 中，<meta> 标签没有结束标签。
		
		在 XHTML 中，<meta> 标签必须被正确地关闭。


	* 提示和注释：


		注释：<meta> 标签永远位于 head 元素内部。
		
		注释：元数据总是以名称/值的形式被成对传递的。


	* 必需的属性


		| 属性 | 值 | 描述 |
		| ------ | ------ | ------ |
		| content | some_text | 定义与 http-equiv 或 name 属性相关的元信息 |
		

	* [meta详细讲解](http://www.w3school.com.cn/tags/tag_meta.asp)

	* meta举例

			<meta name="Keywords" content="网易,邮箱,游戏,新闻,体育,娱乐,女性,亚运,论坛,短信,数码,汽车,手机,财经,科技,相册" />
			<meta name="Description" content="网易是中国领先的互联网技术公司，为用户提供免费邮箱、游戏、搜索引擎服务，开设新闻、娱乐、体育等30多个内容频道，及博客、视频、论坛等互动交流，网聚人的力量。" />

3. HTML5语义化标签

	作用:创建结构清晰的页面可以建立良好的语义化基础，也降低了使用css的难度,也能针对搜索引擎和更新频度的描述和关键词。

	![](https://i.imgur.com/oKlsdnk.png)


	* header标签

		header标记一般放置在页面的顶部，或者页面中某个区块元素的顶部，包含整个页面或区块的标题、简介等信息。

		一篇文档中可以包含多个header标记

		可以为body、article、section、aside标记增加header标记

		header标记未必位于页面的顶部


	* footer标签

		footer标记一般放置在页面的底部，或者页面中某个区块元素的底部。


	* nav标签

		nav标记表示页面的导航，可以通过导航连接到网站的其它页面，或当前页面的其它部分。

	* aside标签

		aside包含的内容不是页面的主要内容，具有独立性，是对页面内容的补充。

		应用:

		页面的侧边栏

		文章引语（内容摘要）

		广告

		友情链接

	* article

		article标签表示的是一个独立完整的内容区域，比如一张报纸的某个独立版块。

		应用:

		一篇博客

		一个论坛帖子

		一片新闻报道

		一个用户论坛

	* section标签

		section表示一个主题性的内容分组，通常包含一个头部（header），可能还会有一个尾部（footer）。

	* figure标签

		figure表示页面中的插图，通常结合figcaption一起使用。

	* time标签

		time表示一个日期、时间，或日期和时间值。
		可以被搜索引擎、屏幕阅读器等识别。

	* main标签

		main标签定义一个页面的主要内容，在一个页面中只能使用一次。
	* html语义化示例

			<div class="container">
			    <header>
			        <div class="logo"></div>
			        <nav></nav>
			    </header>
			    <div class="main">
			        <aside></aside>
			        <section>
			            <article>
			                <header></header>
			                <div class="content"></div>
			                <h6></h6>
			            </article>
			        </section>
			
			    </div>
			    <footer></footer>
			</div>

	* [H5中section和article标签之间的区别](https://www.cnblogs.com/web-cxn/p/5473223.html)

	[详细的HTML5语义化标签](https://blog.csdn.net/coco379/article/details/52938071)

4. 智能表单

	H5新增input的form属性，用于指向特定form表单的id，实现input无需放在form标签之中，即可通过表单进行提交。

	    <FORM id=foo>
	        …
	    </FORM>
	
	    <INPUT … form="foo">


	input标签有:button 
checkbox 
color 
date 
datetime 
datetime-local 
email 
file 
hidden 
image 
month 
number 
password 
radio 
range 
reset 
search 
submit 
tel 
text 
time 
url 
week

	![](https://i.imgur.com/7Tov0WS.png)
	![](https://i.imgur.com/xcRxpU8.png)

	[HTML：Input元素标签的详细介绍](https://www.cnblogs.com/XYQ-208910/p/5831497.html)
	
	input标签配合datalist标签，能实现自动补全的效果

		<input type="search" list="search">
		<datalist id="search">
		    <option >黑老师的由来</option>
		    <option >男人缘何肾虚</option>
		    <option >佳佳婕婕不得不说的故事</option>
		</datalist>

5. HTML5的选择器

	1. 属性选择器


	        /*<!--属性选择器-->*/
	        .container [id^='book00']{
	            color: #0d78ff;
	        }
	        .container [id='book001']{
	            color: red;
	        }
	        .container [id$='4']{
	            color: black;
	        }
	        .container [id*='5']{
	            color: #4C4C4C;
	        }
	
	        /* =直接相等 ^以什么开头 $以什么结尾 *包含什么内容  */


		Element[attr]
		
		Element[attr = "value"]
		
		Element[attr ^= "value"]：以value开头
		
		Element[attr $= "value"]：以value结尾
		
		Element[attr *= "value"]：只要包含value
		
		Element[attr ~= "value"]：必须有value这个词，
		
		Element[attr |= "value"]： 属性值以value-开头，比如：zh-cn



			<p data-text="one web-js">不走寻常路？美国迈入“特朗普时代”的5大猜想</p>
			<p data-text="web-js one">不走寻常路？美国迈入“特朗普时代”的5大猜想</p>
			
			<p data-text="two web-css">河北一假信用点卷走500户村民2000余万存款</p>
			<p data-text="web-css two">河北一假信用点卷走500户村民2000余万存款</p>
			
			<p data-text="three web-html">马来西亚警方捣毁一组织中国籍残疾人行乞团伙</p>
			<p data-text="web-html three">马来西亚警方捣毁一组织中国籍残疾人行乞团伙</p>
			
			
			<p data-text="four xxx">揭秘四川巡山骑警：听狼嚎追马贼 每次任务都是玩命</p>
			<p data-text="five ccc xxx">成都地面沉降最快地方1.4厘米/年 专家剖析主因</p>
			<p data-text="six ccc ttt">成都地面沉降最快地方1.4厘米/年 专家剖析主因</p>



			p{ line-height: 24px; font-size: 12px;}
			p[data-text]{border-bottom: 1px solid #000;}
			p[data-text = "one"]{background: pink;}
			p[data-text ^= "t"]{background: green}
			p[data-text $= "x"]{background: grey}
			p[data-text *= "r"]{color: red}
			p[data-text ~= "ccc"]{color: blue}
			p[data-text |= "web"]{font-weight: bold; font-size: 20px;}
	2. 层级选择器

		* 子选择器

				.div-a>div

		* 相邻兄弟选择器

				.div-a+div

		* 后代选择器

				.div-a div

		* 通用选择器

				.div-a~div


		子选择器与后代选择器的区别:

		>作用于元素的第一代后代，空格作用于元素的所有后代

	3. 伪选择器

		![](https://i.imgur.com/Owu7JrP.png)

		befor选择器
		
		":before" 伪元素可以在元素的内容前面插入新内容。

			.container:before{
			            content: "";
			            display: block;
			            width: 200px;
			            height: 200px;
			            background-color: #1eff06;
			        }

		after选择器

		":after" 伪元素可以在元素的内容之后插入新内容。

			.container:after{
			            content: "";
			            display: block;
			            width: 200px;
			            height: 300px;
			            background-color: #4C4C4C;
			        }
		* 锚伪类

				a:link {color: #FF0000}		/* 未访问的链接 */
				a:visited {color: #00FF00}	/* 已访问的链接 */
				a:hover {color: #FF00FF}	/* 鼠标移动到链接上 */
				a:active {color: #0000FF}	/* 选定的链接 */
				a: focus{color: #0000FF}  匹配当前获得焦点的元素


		必须按照lvhc的顺序来写

		* 结构性伪类选择器

			* first-chile伪类

					.div01-css p:first-child


			* last-child伪类
			
				匹配最后一个字元素

			* only-child伪类

				子元素选择器，匹配父元素包含的唯一子元素
			* only-of-type

					.div01-css h1:only-of-type
					/*表示唯一的一个h1标签*/


			* : nth-child(n)

				匹配父元素中的第几个孩子

			* :nth-last-child(n)


				匹配父元素中倒数第几个孩子

			* : nth-of-type(n)
				
						.div01-css h1:nth-of-type(1)
				匹配顺数的第一个h1标签
			* : nth-last-of-type(n)
		
						.div01-css h1:nth-last-of-type(1)
				匹配顺数的第一个h1标签



		* UI伪类选择器

			\: enabled      匹配处于启用状态的元素

			\: disabled     匹配处于禁用状态的元素

			\: checked      匹配处于选中状态的元素

			\: default      匹配默认状态的元素



	![](https://i.imgur.com/EJP6YB3.png)

	[伪类选择器详细讲解](https://www.cnblogs.com/lvlina/p/6165468.html)