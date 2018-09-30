##Python项目-Day29-css
1. textarea标签(文本域)

		<textarea name="comment" id="area_comment" cols="30" rows="10">
		    innertext
		</textarea>

2. dataset的使用

		<a href="" id="aa" data-user-id="002" data-user-name="tom"></a>
		在html标签中定义一个属性时data-xx-xx格式,例如data-user-id
		<button onclick="show()">dataset</button>
		<script>
		    function show() {
		        var v=document.getElementById('aa').dataset.userId
				在js中可以用控件.dataser.userId驼峰法来获取到这个属性的值
		        alert(v)
		    }

3. 选择文件input

    	<input type="file" name="uoload_file">
		<input type="hidden" name="field＿name" value="value"> 
 
	作用： 
	 
	1 隐藏域在页面中对于用户是不可见的，在表单中插入隐藏域的目的在于收集或发送信息，以利于被处理表单的程序所使用。浏览者单击发送按钮发送表单的时候，隐藏域的信息也被一起发送到服务器。 
	 
	2 有些时候我们要给用户一信息，让他在提交表单时提交上来以确定用户身份，如sessionkey，等等．当然这些东西也能用cookie实现，但使用隐藏域就简单的多了．而且不会有浏览器不支持，用户禁用cookie的烦恼。 
	 
	3 有些时候一个form里有多个提交按钮，怎样使程序能够分清楚到底用户是按那一个按钮提交上来的呢？我们就可以写一个隐藏域，然后在每一个按钮处加上onclick="document.form.command.value="xx""然后我们接到数据后先检查command的值就会知道用户是按的那个按钮提交上来的。 
	 
	4 有时候一个网页中有多个form，我们知道多个form是不能同时提交的，但有时这些form确实相互作用，我们就可以在form中添加隐藏域来使它们联系起来。 
	 
	5 javascript不支持全局变量，但有时我们必须用全局变量，我们就可以把值先存在隐藏域里，它的值就不会丢失了。 
	 
	6 还有个例子，比如按一个按钮弹出四个小窗口，当点击其中的一个小窗口时其他三个自动关闭．可是IE不支持小窗口相互调用，所以只有在父窗口写个隐藏域，当小窗口看到那个隐藏域的值是close时就自己关掉。 
	 
4. 标签的一些属性

	readonly只读
	required该字段为必填字段
	checked	checked	规定此 input 元素首次加载时应当被选中。
	disabled	disabled	当 input 元素加载时禁用此元素。


5. 行内元素和块级元素

	h5标签一般分为行内元素和块级元素

	行内元素有: a img input (即可以与其他行内元素在同一行)
	
	块级元素: h1 p ul li table (独占一行,和页面等宽)

	块元素
	
	①、总是在新行上开始；
	
	②、高度，行高以及外边距和内边距都可控制；
	
	③、宽度缺省是它的容器的100%，除非设定一个宽度。
	
	④、它可以容纳内联元素和其他块元素
	
	行内元素
	
	①、和其他元素都在一行上；
	
	②、高，行高及外边距和内边距不可改变；
	
	③、宽度就是它的文字或图片的宽度，不可改变
	
	④、内联元素只能容纳文本或者其他内联元素


	*[行内元素与块级元素详细](https://blog.csdn.net/xoxo_x/article/details/75212460)*

3. css

	一个页面分为 结构层 样式层 行为层

	css(Cascading Style Sheets)

	css分为:

		* 内部样式  在html文件内写style
		* 外部样式  链接外部css文件
		* 在标签属性style上写css

	
	为什么使用@import
	
	大部分使用@import方式的人是因为旧的浏览器是不支持@import方式的,这意味着我们可以使用@import来引入只让现代浏览器解析的CSS样式

	link与@import区别与选择   -   TOP
	首页link和import语法结构不同，前者<link>是html标签，只能放入html源代码中使用，后者可看作为css样式，作用是引入css样式功能。import在html使用时候需要\<style type="text/css"\>标签，同时可以直接“@import url(CSS文件路径地址);”放如css文件或css代码里引入其它css文件。

4. 选择器

	1. 类选择器

			.btn-css {
			        width: 200px;
			        height: 50px;
			        background: blue;
			        color: white;
			    }

	2. 标签选择器

			input{
			        color: #b3ff8d;
			    }

	3. id 选择器

			#btn_register{
			            width: 200px;
			            height: 50px;
			            background: blue;
			            color: white;
			        }

	优先级 id选择器---->类选择器------>标签选择器

5. 选择器高级

	1. 子选择器(空格隔开)


			.div01-css p{
			            color: red;
			        }
			选择类div01-css下面的p标签

	2. 交集选择器(紧跟在后面) 满足相交的

			<style type="text/css">
			            p.xxx{
			                color: red;
			            }
			        </style>
			    </head>
			<body>
			 
	        <p>我是段落</p>
	        <p class="xxx">我是段落</p>
	        <p>我是段落</p>
	        <p class="xxx">我是段落</p>
	        <p>我是段落</p>

	3. 并集选择器(,隔开)
		
			 .xxx,.xxxx,.xxxxx{
	                color: red;
	            }
	        </style>
	    </head>
	<body>

	        <p class="xxx">我是段落</p>
	        <p class="xxxx">我是段落</p>
	        <p class="xxxxx">我是段落</p>

6. 权重

		<!--标签选择器-->
		<!--0001-->
		p{
		    color:red;
		
		}
		/*类选择器*/
		/*0010*/
		.p-css{
		    color: blue;
		}
		/*id选择器*/
		/*0100*/
		#p01{
		    color: green;
		}
		/*显示同一个元素,比较权重大小  id:100,class:10,标签:1 行内样式:1000
		!important权重最大
		*/
		/*id选择器--->类选择器------>标签选择器*/


4. font属性

		font-style
		font-variant
		font-weight
		font-size/line-height
		font-family

		/*3em 字体为系统默认字体的3倍*/


11. 伪类选择器

		a:link {color: #FF0000}		/* 未访问的链接 */
		a:visited {color: #00FF00}	/* 已访问的链接 */
		a:hover {color: #FF00FF}	/* 鼠标移动到链接上 */
		a:active {color: #0000FF}	/* 选定的链接 */

		注释：在 CSS 定义中，a:hover 必须位于 a:link 和 a:visited 之后，这样才能生效！
		
		注释：在 CSS 定义中，a:active 必须位于 a:hover 之后，这样才能生效！
