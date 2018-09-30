##Python项目-Day33-border-box-shadow-线性渐变-transition(过渡动画)-flex布局
1. border(边框圆角样式的设置)

		border-top-left-radius
		border-top-right-radius
		border-bottom-left-radius
		border-bottom-right-radius
		border-radius

	以上样式分别设置单边或者多边，半径大小可以使用px、百分比和em

		border-top-left-radius:10px
		border-top-left-radius:20px 10px;
		border-radius:50% 20px 25% 5em/25% 15px 40px 55%


2. border-image(边框图像的设置)

	将图片分割成为九个部分，四个角上的图像作为边框的四个顶点，其余部分作为边框的四边

	例如:

		border-image:url(/i/border.png) 30 30 stretch;

	![](https://i.imgur.com/IWe9BpS.png)


3. box-shadow(阴影样式的应用)

	格式:box-shadow：hoffset   voffset  blur  spread     
                                color    inset

	![](https://i.imgur.com/jYiNfmI.png)


	例如:

		box-shadow: 10px 10px 10px 50px red inset;

		/*阴影水平偏移10px 垂直偏移 模糊值10px  延伸速度/半径50px  阴影颜色为red 内嵌到盒子内部*/

4. text-shadow(文本阴影设置)

	例如:

		text-shadow: 5px 5px 5px grey;


5. text-overflow(文本裁剪)

	参数名|说明|
	--|--|--
	clip|不使用省略号作为结尾
	ellipsis|使用省略号作为结尾


	要想做到文本裁剪的效果,必须要满足:
	
	* 必须不换行(white-space)
	* 必须使用overflow控制溢出

	例如:

		text-overflow: ellipsis;
        white-space: nowrap;
        overflow: hidden;

6. text-stroke(文本描边)

	格式:text-stroke：描边宽度  描边颜色；

	注意:

	* 该样式不是所有的浏览器都支持
	* 需要添加前缀修饰符


	例如:

        -webkit-text-stroke: 1px yellow;
7. css前缀

	![](https://i.imgur.com/jQLKn38.png)

	* 优雅降级 -  先满足新的浏览器的设计方式
	* 逐渐增强 -  先满足普通浏览器的设计方式
	* 优雅降级适合新版本浏览器
    * 渐进增强适合老版本浏览器

	 [测试浏览器兼容的网站](https://caniuse.com/)

	例如:

 		//优雅降级

		-o-border-image: url("");
        -webkit-border-image: url("");
        border-image: url("");

		//主键增强

		border-image: url("");
		-o-border-image: url("");
		-webkit-border-image: url("");

8. 线性渐变

	格式:background：linear-gradient(方向，颜色1，颜色2 。。。)；

	例如:

		#grad1 {
		    height: 200px;
		    background: -webkit-linear-gradient(left, red , blue); /* Safari 5.1 - 6.0 */
		    background: -o-linear-gradient(right, red, blue); /* Opera 11.1 - 12.0 */
		    background: -moz-linear-gradient(right, red, blue); /* Firefox 3.6 - 15 */
		    background: linear-gradient(to right, red , blue); /* 标准的语法（必须放在最后） */
		}
       
	[关于颜色渐变](http://www.runoob.com/css3/css3-gradients.html)

9. transform属性

	![](https://i.imgur.com/jksjjzi.png)

	例如:

        transform:  translate(200px,202px) skew(45deg);
	

	tramsform-origin属性:

	该属性用于改变变形的基准点，默认在中心，用空格间隔

	![](https://i.imgur.com/G6bIgTx.png)


	例如:

        transform-origin: 0% 40%;

10. transition(过渡动画)

	过渡是一种js事件触发的动画效果的方式,例如click,hover,foucs,checked等事件

	格式:transition：控制的属性1   动画持续时间   动画效果  延迟时间；

	例如:

		transition：background-color  1s  ease 0s；
		transition：color  1s  linear  1.0s；
		transition：all  1s  ease 0s；

	![](https://i.imgur.com/9p14LWy.png)


11. 关键帧动画

	利用类似于Flash的关键帧进行控制的动画方式，比过渡动画功能更加强大

	动画原理

	利用@keyFrames创建关键帧动画

	利用animation调用关键帧动画

	代码举例:

		/*change是关键帧名*/
		@keyframes change {
		        0%{
		            background-color: red;
		        }
		        50%{
		            background-color: purple;
		        }
		        100%{
		            background-color: lime;
		        }
		
		    }
		    .div-02:hover{
			/*animation属性实现change效果*/
		        animation: change 2s linear;
		    }



[flex布局详解](https://www.cnblogs.com/xuyuntao/articles/6391728.html)