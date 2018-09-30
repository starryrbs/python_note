##Python项目-Day37-DOM
[详细的DOM讲解](http://www.w3school.com.cn/htmldom/dom_nodes.asp)

1. 什么是DOM?

	文档对象模型(Document Object Model),通过DOM可以动态改变文档内容

2. 动态改变文档内容的原理

	1. 解析文档(如HTML)并生成DOM树
	2. 通过DOM标准接口+编程语言改变文档内容


3. DOM节点

	在 HTML DOM 中，所有事物都是节点。DOM 是被视为节点树的 HTML。

	整个文档是一个文档节点

	每个 HTML 元素是元素节点

	HTML 元素内的文本是文本节点

	每个 HTML 属性是属性节点

	注释是注释节点
		
	![](https://i.imgur.com/k5cCoke.jpg)


	* 节点父、子和同胞

		* 父（parent）
		* 子（child)
		* 同胞（sibling）
		
4. DOM节点对象属性

	1. nodeName
		
		* nodeName是只读的
		* 元素节点的nodeName与标签名相同
		* 属性节点的nodeName与属性名相同
		* 文本节点的nodeName始终是#text
		* 文档节点的nodeName始终是#document

	2. nodeValue

		* 元素节点的nodeValue是undenfined或null
		* 文本节点的nodeValue是文本本身
		* 属性节点的nodeValue是属性值
	3. nodeValue

		节点类型|nodeType
		--|--|
		元素|1
		属性|2
		文本|3
		注释|8
		文档|9


5. DOM的操作

	1. 查看节点
		
		* 获取指定元素节点的方法

			1. getElementById()
			2. getElementsByName()
			3. getElementsByTagName()
			4. getElementsByClassName()

		* 元素节点的常用属性

			1. tagName
			2. innerHTML/innerText
			3. id
			4. style
			5. className


		* 访问某个元素的子元素节点


			1. childNodes访问所有的节点,包括元素节点文本节点

			2. children访问元素节点


		* 访问父节点下的第一个节点对象

			1. firstChild第一个节点,包括元素节点和文本节点
			2. firstElementChild:第一个元素节点

		* 访问父节点下的最后一个节点对象

			同上一个

		* 获取前一个兄弟节点对象

			1. previousSibling获取前一个兄弟节点,包括元素节点和文本节点
			2. previousElementChild获取前一个兄弟元素节点

		* 获取父元素，不存在兼容性问题

			parentNode

		* offsetParent：获取第一个设置定位的父元素；

     	* offsetLeft：获取离第一个定位父元素的左距离；

     	* offsetTop：获取离第一个定位父元素的上距离；

		[查看节点的兼容性问题](https://www.cnblogs.com/ilovexiaoming/p/6853176.html)

	
		> 属性节点

		* 获取属性节点.attributes['type']
		* 查看属性节点值 getAttribute('type')
		* 修改属性节点值 setAttribute('type','button')

		> 文本节点

		* 获取文本节点的值childNodes[0]

	2. 创建和增加节点

		1. createElement（）：创建节点
		2. createTextNode（）：创建文本节点
		3. appendChild（）：末尾追加方式插入节点
		4. insertBefore（）：在指定节点前插入新节点
		5. cloneNode（true）：克隆节点,true表示深度复制

		举例:

			var container = document.querySelector('.container');
			var div = document.querySelector('.container>div');
			//    创建一个元素节点
			var input = document.createElement('input');
			//创建文本节点
			var text = document.createTextNode('11');
			//将文本节点添加到元素节点中
			input.appendChild(text);
			//将元素节点添加到div中
			div.appendChild(input);
			//克隆节点,参数为true,表示里面的内容也复制,其他表示只复制节点,也就是复制了div
			var div_2 = div.cloneNode(true);
			//在div前面插入input,必须要知道父节点container
			container.insertBefore(input, div);
			container.appendChild(div_2);

	3. 删除和替换节点

		* removeChild（）：删除节点  
		
		
				container.removeChild(div)

		* replaceChild():替换节点

				parent.replaceChild(para,child);
				//para替换child

6. DOM优化

	减少DOM和JS的交互次数


	innerHTML和appendChild的比较

	利用节点克隆提高性能

	遍历节点数组时采用局部变量
