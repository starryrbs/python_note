##Python项目-Day40-JQuery
1. JQuery

	JQuery库分为开发板和发布版

	名称|大小|说明
	--|--|--
	jquery-1.版本号.js(开发版)|约268KB|完整无压缩版本，主要用于测试、学习和开发
	jquery-1.版本号.min.js|约91KB|经过工具压缩或经过服务器开启Gzip压缩,主要应用于发布的产品和项目

	引用JQuery

	    <script src="js/jquery-3.3.1.js"></script>

	$(document).ready()与window.onload类似，但也有区别


	 |window.onload|$(document).ready()
	--|--|--|
	执行时机|必须等待网页中所有的内容加载完毕后(包括图片、flash,视频等)才能执行|网页中所有DOM文档结构绘制完毕后即刻执行,可能与DOM元素关联的内容(图片,flash,视频等)并没有加载完
	编写个数|同一页面不能编写多个|同一页面能编写多个
	简写写法|无|$(function(){//执行代码});


2. JQuery语法

	$ 等同于 JQuery

		$(document).ready=JQuery(document).ready()

		$(document).ready(function () {
		
		});
		//等同于下面的
		$(function () {
		
		});

	1. JQuery选择器

		基础语法:$(selector).action()
		
			* 美元符号定义JQuery
			* 选择符(selector)"查询"和"查找"HTML元素
			* JQuery的action()执行对元素的操作

		举例:

			$(this).hide()//隐藏当前元素
			$("p").hide()//隐藏所有段落
			$(".test").hide()//隐藏所有class="test"的所有元素
			$("#test").hide()//隐藏所有id="test"的元素

	
	2. JQuery元素选择器

		* $("p")选取p元素
		* $("p.test")选取所有class="test"的p元素

	3. JQuery属性选择器

		* $("[href]")选取所有带有href属性的元素
		* $("[href='#']")选取所有带有href值等于"#"的元素
		* $("[href!='#']") 选取所有带有 href 值不等于 "#" 的元素。
		* $("[href$='.jpg']") 选取所有 href 值以 ".jpg" 结尾的元素。

	4. css选择器

		jQuery CSS 选择器可用于改变 HTML 元素的 CSS 属性

			$("p").css("background-color","red");

	[JQuery选择器详细](http://www.w3school.com.cn/jquery/jquery_ref_selectors.asp)

3. JQuery事件函数

	* 格式:

		$("[href='#']").click(function () {
            $("p").hide()
        })


	* JQuery名称冲突:

		某些其他 JavaScript 库中的函数（比如 Prototype）同样使用 $ 符号。

		解决方法:

			var jq=jQuery.noConflict()，帮助您使用自己的名称（比如 jq）来代替 $ 符号。
			let jq=jQuery.noConflict();
	
	        jq("[href='#']").click(function () {
	            jq("p").hide()
	        })

		* bind()  绑定一个事件

				$("button").bind('click',function () {
	            $("[href='#']").slideToggle();
	        	})

		* blur()  失去焦点

				$("input").blur(function () {
				            $("input").css("color","red")
				        })

		* focus() 获得焦点

				 $("input").focus(function () {
				            $("input").css("background","red")
				        })

		* change() 当发生变化时
		* click()点击事件

		* keypress()
		完整的 key press 过程分为两个部分：1. 按键被按下；2. 按键被松开。
		* keyup()
		* keydown()

		* mousedown()	
		* mouseenter()
		* mouseleave()	
		* mousemove()	
		* mouseout()	
		* mouseover()	
		* mouseup()	
		* toggle()点击时,在两个函数或者多个函数之间进行切换

				$("button").toggle(function(){
				                $("body").css("background-color","green");},
				            function(){
				                $("body").css("background-color","red");},
				            function(){
				                $("body").css("background-color","yellow");}
				        );


4. JQuery隐藏/显示

		$("#hide").click(function(){
		  $("p").hide();
		});
		
		$("#show").click(function(){
		  $("p").show();
		});

		hide()和show()方法用来隐藏和显示HTML元素

	语法:

		$(selector).hide(speed,callback);
		
		$(selector).show(speed,callback);

5. JQuery淡入/淡出

		$("button").click(function (event) {
		            $("input").fadeIn(1000,function () {
		                alert(1)
		            })
		
		        })

	* jQuery fadeIn()淡入
	* jQuery fadeOut()淡出
	* jQuery fadeToggle()淡入淡出
	* Jquery 演示带有不同参数的 fadeTo() 方法

			 $("button").click(function(){
			    $("#div1").fadeTo("slow",0.15);
			    $("#div2").fadeTo("slow",0.4);
			    $("#div3").fadeTo("slow",0.7);
			  });

	* jQuery slideDown()下划
	* jQuery slideUp()上划
	* jQuery slideToggle()上下划


6. JQuery动画

	 animate() 方法用于创建自定义动画.

	语法:

		$(selector).animate({params},speed,callback);
	
	必需的 params 参数定义形成动画的 CSS 属性。
	
	可选的 speed 参数规定效果的时长。它可以取以下值："slow"、"fast" 或毫秒。
	
	可选的 callback 参数是动画完成后所执行的函数名称。


		$("button").click(function () {
		            $(".dong").animate({left:'250px'},"slow",function () {
		                $(".dong").css("background","red")
		            })
		        })

	希望在彼此之后执行不同的动画,可以使用队列功能

		$("button").click(function(){
		            var div=$("div");
		            div.animate({height:'300px',opacity:'0.4'},"slow");
		            div.animate({width:'300px',opacity:'0.8'},"slow");
		            div.animate({height:'100px',opacity:'0.4'},"slow");
		            div.animate({width:'100px',opacity:'0.8'},"slow");
		        });


	* stop()方法停止动画

			$("button").click(function () {
		            $(".dong").animate({left:'250px'},1000,function () {
		                $(".dong").css("background","red")
		            })
		        });

		        $("input[type='button']").click(function () {
		            $(".dong").stop()
		        })

		stop() 方法适用于所有 jQuery 效果函数，包括滑动、淡入淡出和自定义动画。


7. jQuery 方法链接


	直到现在，我们都是一次写一条 jQuery 语句（一条接着另一条）。

	不过，有一种名为链接（chaining）的技术，允许我们在相同的元素上运行多条 jQuery 命令，一条接着另一条。
		$(".dong").css("background","red").slideUp(2000).slideDown(2000);


8. jquery获取

	获得内容 - text()、html() 以及 val()

	* text() - 设置或返回所选元素的文本内容
	* html() - 设置或返回所选元素的内容（包括 HTML 标记）
	* val() - 设置或返回表单字段的值
	* attr() 方法用于获取属性值

			$("button").click(function(){
			  alert($("#w3s").attr("href"));
			});

	带有回调函数的text()和html()


9. 添加新的HTML内容

	* append() - 在被选元素的**结尾**插入内容
	* prepend() - 在被选元素的开头插入内容
	* after() - 在被选元素**之后**插入内容
	* before() - 在被选元素之前插入内容

		实例:

			$("p").append("Some appended text.");


	通过append()和prepend()方法添加若干新元素

		function appendText()
		{
		var txt1="<p>Text.</p>";               // 以 HTML 创建新元素
		var txt2=$("<p></p>").text("Text.");   // 以 jQuery 创建新元素
		var txt3=document.createElement("p");  // 以 DOM 创建新元素
		txt3.innerHTML="Text.";
		$("p").append(txt1,txt2,txt3);         // 追加新元素
		}

10. 删除元素

		$(".dong").remove()//删除所有.dong
		$(".dong").empty()//清空内容子元素
        $("p").remove('.dd')//删除所有.dd的p元素


11. 操作CSS

	addClass() - 向被选元素添加一个或多个类
	
		$('.dong').addClass('div-2')
	removeClass() - 从被选元素删除一个或多个类
	
		$('.dong').removeClass('dong')
	toggleClass() - 对被选元素进行添加/删除类的切换操作
	
		$('.dong').toggleClass('div-2')
	css() - 设置或返回样式属性

		返回指定属性的值
		$("p").css("background-color");
		设置指定的css属性
		$("p").css("background-color","yellow");
		设置多个css属性
		$("p").css({"background-color":"yellow","font-size":"200%"});

        $('.dong').css({'background':"red","color":"white"})


12. JQuery尺寸

	width()设置或返回元素的宽度（不包括内边距、边框或外边距）。

	height()设置或返回元素的高度（不包括内边距、边框或外边距）。

	innerWidth()方法返回元素的宽度（包括内边距）。

	innerHeight() 方法返回元素的高度（包括内边距）。

	outerWidth()方法返回元素的宽度（包括内边距和边框）。

	outerHeight()方法返回元素的高度（包括内边距和边框）


13. JQuery遍历

	1. 祖先

			parent()方法返回被选元素的直接父元素
			parents()方法返回被选元素的所有祖先元素，它一路向上直到文档的根元素 (<html>)。
			parentsUntil()方法返回介于两个给定元素之间的所有祖先元素。

	2. 后代

		children()方法返回被选元素的所有直接子元素。

		下面的例子返回每个 <div> 元素的所有直接子元素：

	 		$("div").children();

		下面的例子返回类名为 "1" 的所有 <p> 元素，并且它们是 \<div> 的直接子元素：

			$("div").children("p.1");
		find() 方法返回被选元素的后代元素，一路向下直到最后一个后代。

			$("div").find("*");

	3. 同胞

			siblings()方法返回被选元素的所有同胞元素。
			next()方法返回被选元素的下一个同胞元素。
			nextAll()方法返回被选元素的所有跟随的同胞元素
			nextUntil()方法返回介于两个给定参数之间的所有跟随的同胞元素。
			prev()与上面的类似，是前一个
			prevAll()
			prevUntil()

	4. 过滤

		三个最基本的过滤方法是：first(), last() 和 eq()



			$("div p").first();
			$("div p").last();
			$("p").eq(1);
			$("p").filter(".intro");//过滤
			$("p").not(".intro");//与not相反

14. ajax

		$.ajax({
		  url:'test.do', 
		  data:{id:123,name:'xiaoming'}, 
		  type:'post', 
		  dataType:'json', 
		  success:function(data){
		   alert(data);//弹窗 
		   //TODO ........
		  
		  },
		  
		  error:function(data){
		    alert(data);//弹窗
		    //TODO ........
		  }
		 
		 })


	url: 要求为String类型的参数，（默认为当前页地址）发送请求的地址。
	
	type: 要求为String类型的参数，请求方式（post或get）默认为get。注意其他http请求方法，例如put和delete也可以使用，但仅部分浏览器支持。 
     
	timeout: 要求为Number类型的参数，设置请求超时时间（毫秒）。此设置将覆盖$.ajaxSetup()方法的全局设置。 
        
	async：要求为Boolean类型的参数，默认设置为true，所有请求均为异步请求。 如果需要发送同步请求，请将此选项设置为false。注意，同步请求将锁住浏览器，用户其他操作必须等 待请求完成才可以执行。 
    
	cache：要求为Boolean类型的参数，默认为true（当dataType为script时，默认为false）。设置为false将不会从浏览器缓存中加载请求信息。  
     
	data: 要求为Object或String类型的参数，发送到服务器的数据。如果已经不是字符串，将自动转换为字符串格式。get请求中将附加在url后。防止这种自动转换，可以查看processData选项。对象必须为key/value格式，例如{foo1:"bar1",foo2:"bar2"}转换为&foo1=bar1&foo2=bar2。如果是数组，JQuery将自动为不同值对应同一个名称。例如{foo:["bar1","bar2"]}转换为&foo=bar1&foo=bar2。 
        
	dataType: 要求为String类型的参数，预期服务器返回的数据类型。如果不指定，JQuery将自动根据http包mime信息返回responseXML或responseText，并作为回调函数参数传递。