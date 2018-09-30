##Python项目-Day30-font-background-浮动
1. font属性

	1. font-family 设置字体类型  font-family:"隶书";
	2. font-size	设置字体大小	font-size:12px;
	3. font-style	设置字体风格	font-style:italic;#斜体
	4. font-weight	设置字体的粗细	font-weight:bold;

			normal	默认值，定义标准的字体。
			bold	粗体字体。
			bolder	更粗的字体。
			lighter	更细的字体。
			100、200、300、400、500、600、700、800、900	定义由细到粗的字体。
			400等同于normal，700等同于bold。
	5. font	在一个声明中设置所有字体属性	font:italic bold 36px "宋体";


		字体属性的顺序：字体风格→字体粗细→字体大小/行高→字体类型
		
		p span{font:oblique bold 12px/20px "楷体";}


2. 文本属性

	

	![](https://i.imgur.com/iZTKHhO.png)


3. 文本装饰

	text-decoration属性

	none	默认值，定义的标准文本。

	underline	设置文本的下划线。

	overline	设置文本的上划线。

	line-through	设置文本的删除线。

4. a伪类


	a:link	未单击访问时超链接样式	a:link{color:#9ef5f9;}

	a:visited	单击访问后超链接样式	a:visited {color:#333;}

	a:hover	鼠标悬浮其上的超链接样式	a:hover{color:#ff7300;	

	a:active	鼠标单击未释放的超链接样式	a:active {color:#999;}

	按照顺序:lvha



5. 设置鼠标形状


	![](https://i.imgur.com/yltyS01.png)


6. 列表样式

	list-style-type

	![](https://i.imgur.com/JQm1lKa.png)


7. background

	1. 背景颜色

		background-color


	2. 背景图片


		background-image

			background-image:url(图片路径)

	3. 背景重复属性

		background-repeat属性

		repeat：沿水平和垂直两个方向平铺

		no-repeat：不平铺，即只显示一次

		repeat-x：只沿水平方向平铺

		repeat-y：只沿垂直方向平铺
	4. 背景定位

		 background-position属性

	其他属性

	![](https://i.imgur.com/vty4HbN.png)

8. 盒子模型

	所有html元素都可以看做盒子

	CSS盒模型本质上是一个盒子，封装周围的HTML元素，它包括：边距，边框，填充，和实际内容。
	
	盒模型允许我们在其它元素和周围元素边框之间的空间放置元素

	Margin(外边距) - 清除边框外的区域，外边距是透明的。

	Border(边框) - 围绕在内边距和内容外的边框。

	Padding(内边距) - 清除内容周围的区域，内边距是透明的。

	Content(内容) - 盒子的内容，显示文本和图像。

	* padding属性:	

		padding-left 

		padding-right

		padding-top

		padding-bottom

		padding

	* border三要素

		
		border-color 

		border-width

		border-style


	![](https://i.imgur.com/hYefjMq.png)

	border-style:dotted solid double dashed;
 

	上边框是点状

	右边框是实线

	下边框是双线

	左边框是虚线

	* margin属性

		margin

		margin-top

		margin-right

		margin-bottom

		margin-left

		margin

	盒子模型总尺寸=border+width+padding+margin


9. 标准文档流


	标准文档流组成

	块级元素（block  level）

	\<h1>…\<h6>、\<p>、\<div>、列表

	独占一行，可设置宽高，宽度默认和父级元素相同

	内联元素（inline）
	\<span>、\<a>、\<img/>、\<strong>...
	水平排列，不可设置宽高，宽度根据内容而定


10. 浮动元素

	float:left/right;
	
	浮动元素脱离标准文档流

	浮动元素的位置空出来，由非浮动元素占据

	浮动元素不论是块级还是行级元素，都可以水平排列，同时设置宽度和高度

	浮动元素具有相互贴靠特点

	浮动元素具有文字围绕特点

	浮动元素不设置宽度时具有收缩特点

	父级元素的宽度是所有浮动子元素的宽度之和

	* 浮动带来的问题

	浮动元素使父容器失去高度，影响了后续元素


	1. 在浮动元素后加一个div

		class为  clear:both


	2. 使用overflow属性

	![](https://i.imgur.com/Cz1McGH.png)