##Python项目-Day31-position-flex布局
1. position属性

	static：默认值，没有定位

	relative：相对定位

	absolute：绝对定位

	fixed：固定定位

	* relative

		relative属性值

		参考点是元素自己原来位置

		偏移设置：top、left、right、bottom

		代码举例:
			
			#third {
				background-color:#C5DECC;
				border:1px #395E4F dashed;
				position:relative;
				right:20px;
				bottom:30px;

		相对定位的实际应用

		1. 微调位置
		2. 和绝对定位配合,作为定位基准点

	* absolute

		absolute属性值

		偏移设置： left、right、top、bottom


	* fixed

	fixed属性值

	固定定位的参考点是浏览器窗口

	固定定位元素脱离标准文档流

	Ie低版本不支持


2. flex布局

	[flex布局详解  **重点**](https://www.cnblogs.com/xuyuntao/articles/6391728.html)
