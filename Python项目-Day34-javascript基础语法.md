##Python项目-Day34-javascript基础语法
1. 什么是javascript?

	JavaScript一种直译式脚本语言，是一种动态类型、弱类型、基于原型的语言，内置支持类型。它的解释器被称为JavaScript引擎，为浏览器的一部分，广泛用于客户端的脚本语言，最早是在HTML（标准通用标记语言下的一个应用）网页上使用，用来给HTML网页增加动态功能。

2. javascript的作用

	* 表单验证－减轻服务器端压力
	* 页面动态效果
	* H5大量框架采用Javascript开发完成

3. javascript的组成

	![](https://i.imgur.com/mNIsGae.png)


4. 网页中使用javascript的方式

	* 使用\<script>标签,直接在html内部写
	* 外部JS文件

			<script src="hello.js" language="javascript"></script>
	* 直接在HTML标签中
	
			<a href="javascript:alert('hello js!')">click me!</a>

##javascript基础语法
1. 输入与输出

	* alert(“提示信息”);

	一般用来代码测试


	* prompt()


			prompt(“提示信息”, “输入框的默认信息”);
			prompt(“请输入姓名”, “张三”);

	* console

		使用方式|作用
		--|--|
		console.log()|控制台输出  普通输出语句
		console.warn()|控制台警示
		console.error()|错误提示
	
	console主要用于开发人员进行调试，对用户不可见

2. 变量

	变量是一个标识符，在程序运行过程中用于保存临时数据

	js声明变量的方式:let var const

	三者的区别:

	1. const定义的变量不可以修改，而且必须初始化。

			1 const b = 2;//正确
			2 // const b;//错误，必须初始化 
			3 console.log('函数外const定义b：' + b);//有输出值
			4 // b = 5;
			5 // console.log('函数外修改const定义b：' + b);//无法输出

	2. var定义的变量可以修改，如果不初始化会输出undefined，不会报错。相当于是全局变量

			var a = 1;
			// var a;//不会报错,输出是undefined
			console.log('函数外var定义a：' + a);//可以输出a=1
			function change(){
			a = 4;
			console.log('函数内var定义a：' + a);//可以输出a=4
			} 
			change();
			console.log('函数调用后var定义a为函数内部修改值：' + a);//可以输出a=4

	3. 3.let是块级作用域，函数内部使用let定义后，对函数外部无影响。作用是{}之内

			let c = 3;
			console.log('函数外let定义c：' + c);//输出c=3
			function change(){
			let c = 6;
			console.log('函数内let定义c：' + c);//输出c=6
			} 
			change();
			console.log('函数调用后let定义c不受函数内部定义影响：' + c);//输出c=3

	* 变量命名语法规定


		必须是字母、数字、下划线和$组成

		首字母不能是数字

		不能使用Javascript保留字

		命名区分大小写


3. 数据类型

	![](https://i.imgur.com/SefIc6b.png)

	使用typeof检测变量的返回类型值

	typeof运算符返回值如下：

	undefined：变量被声明后，但未被赋值

	string：用单引号或双引号来声明的字符串

	boolean：布尔值

	number：整数或浮点数

	object：javascript中的对象、数组和null

4. 运算符号

	![](https://i.imgur.com/I9jiOPI.png)

	* 属性,值都相等使用  ===
	* 逻辑运算符的优先级！ > && > ||

5. javascript可以使用连字符+输出

		console.log('11'+12)
		//结果为1122

6. if for while break continue

	* if

			if (2>1){
			        alert('yes')
			    } else {
			        alert('no')
			    }
	* for

			for (var i=1;i<=100;i++){
			       console.log(i);
			   }

	* while

			var i=1;
			    while (i<10){
			        i++;
			        alert(i)
			    }

	* break 

	跳出循环

	* continue

	结束本次循环,还会继续后面的循环


7. 函数

	函数的含义：是将相关代码封装在一起，能完成特定任务的代码块

	函数的作用：重复调用、简化程序

	函数分类：系统函数和自定义函数


	函数的定义与调用:

		function show(a) {
		        alert(a);
		    }
		    show(1);


8. 常用的系统函数

	1. parseInt ("字符串")
	
		将数据类型转换为整型数字,有向下取整的效果

	2. parseFloat("字符串")


		将数据类型转换为浮点型数字 

	3. isNaN()

		用于检查其参数是否是非数字


9. 函数作用域


	全局作用域：(var)

	在代码的任何位置都可以访问

	最外层的函数

	最外层函数外定义的变量

	隐式全局变量

	局部作用域：(let)

	在指定的代码段范围中可以访问

	函数内部定义的变量


10. 声明提升的概念

		n=12;
	    var n;

	上面的例子就是声明提升,可以先给变变量赋值,后声明,注意只有var可以.

		var a = 18;
		fun1();
		function fun1(){
		    var b = 9;
		    console.log(a);
		    console.log(b);
		    var a = '123';
		}

	上面这段代码中 a为undenfined b为9,因为声明提升会将var a提升到作用域最前面

11. javascript内置对象


	对象是一种复杂的数据类型


	Javascript提供了大量的内置对象

	Array

	String

	Math

	Date

	Arguments 

	RegExp

12. 数组

	数组是同类数据的有序集合

	1. 数组的声明:

		    let arr=[1,3,5];
		    let arr02=new Array([1,2,3]);


	2. 数组的常用属性和方法


	![](https://i.imgur.com/C8DopfX.png)

	    let arr1=[1,2,3,4,1,2];
		//splice(start,deletecount):删除原数组指定的位置,返回被删除的子数组
	    let delete_arr1=arr1.splice(4,2,88);


		//    slice(start,end)  截取到end之前的位置,不包含end


13. string类型的常用方法

	String是Javascript提供的描述字符串的对象

	![](https://i.imgur.com/HAVcPZr.png)

14. Math

	Math是用于执行数学运算的对象，提供了大量的数学运算函数

	![](https://i.imgur.com/hM9ZVXa.png)


15. 分页的实现

	   let books=new Array(100);
	    for (let i=0;i<books.length;i++){
	        books[i]='第'+i+'本书';
	    }
	
	    // console.log(books);
		//分页
	    let size=8;
	    let pages_acount=books.length%size==0?books.length/size:parseInt(books.length/size+1);
	    // alert(pages_acount);
	
	    let index=prompt("请输入页码");
	    if (!isNaN(index)&&index<=pages_acount&&index>=1){
	        let start=(index-1)*size;
	        let end=index*size-1;
	        for (let i=start;i<=end;i++){
	            console.log(books[i]);
	        }
	    }else {
	        alert('错误')
	    }




16. map,every,some,filter

	every测定数组的所有项满足一定条件.true

	some 测定数组至少有一项满足条件,true

	filter筛选满足条件的数组项

	map 处理数组的每一项

	例子:

	    var res=arr.every(function (item,index,array) {
	        return item>=3;
	    });

17. 三元运算符

		let a=5;
		res=a>0?'yes':'no';
		alert(res);
		//前面运算为true,res为'res',否则为'no'

