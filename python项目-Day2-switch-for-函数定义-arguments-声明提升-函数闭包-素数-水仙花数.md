1. switch语句

	代码举例:

	```
	switch (num){
		        //num等于1 或者等于2 都显示IT
		        case '1':
		            // alert("IT");//如果没有加break语句,switch语句是按顺序执行的,
		        case '2':
		            alert("IT");
		            break;//表示跳出switch语句
		        case '3':
		        case '4':
		        case '5':
		            alert("Chinese");
		        case '6':
		        case '7':
		            break;
		        default:
		    }
	```

2. for循环语句

	```
		//for循环的执行步骤:
	//1.i=1
    //2.i<=100?
    //3.console.log(i);执行循环体
    //4.i++
    //循环执行2,3,4最后一次执行2
    var flag=false;
    //循环体没有作用域
    for (var i=1;i<=100;i++){
        var b=1000;
        console.log(i);
    }
    //for循环中的i 此时是一个全局变量
	```
	for循环中的i可以在for循环外被调用,而且值会变(例如上面的例子i会i++)
	 如果在for循环中使用break跳出,值并不会变

	
	 
3. 函数

* 关键字function定义函数 例如:function add(){}
* 定义函数的函数名,注意与关键字重名
* m,n形参,注意:形参没有类型
* return返回值;跳出函数体

	######isNaN判断参数是否**不是**数字(not a number),(NaN==NaN)不相等,不是类型,也不是值,不能相比较
	
	######parseInt和parseFloat函数
	
	######在js中没有重载,可以用arguments

	```
function _add_number() {
    // var  a=arguments[0];//arguments是一个伪数组对象
    // var  b=arguments[1];
    // var  c=arguments[2];
    // console.log(`a=${a},b=${b},c=${c}`)
   var total=0;
  for (var i=0;i<arguments.length;i++){
      total=total+arguments[i];
  }
  return total;
}
var res=_add_number(10,20,30);//你可以不写在函数定义的时候不写参数，在你函数调用的,
//时候去写,arguments可以获取到你调用的时候添加的参数
console.log(res);
	```
	1. Javascrip中每个函数都会有一个Arguments对象实例arguments，它引用着函数的实参，可以用数组下标的方式"[]"引用arguments的元素。
	2. arguments对象和Function是分不开的,arguments对象只有函数开始时才可用。
	3. 定义函数与匿名函数的区别：匿名函数只适用于使用一次，而定义函数适用于使用多次
	4. 在调用函数时加（）与不加（）的区别 例如display与display（）的区别，前者相当于是**注册**语句，a指向的是函数体所在的地址位置，反观后者则直接运行函数，再将值复制给a

		```
		function display() {
		return 5;
        alert('this is a button');
         }
         var a= display;
         var a= display();
		```


4. 声明提升的概念
	例如：
	```
	a=12
	var a;
	```
	
	首先，这两行是对的，在运行时，会变成


	```
	var a;
	a = 12;
	```

	更例如：

```
	var a=12
	function test(){
	console.log(a)
	a="123";
	var a;
	}
	test();
```
这段代码执行的结果是undenfined，因为声明提升会将var a提升到函数的最前面，当显示a的值a是未初始化的，所以是undenfined。
	
5. [函数闭包的概念](https://www.cnblogs.com/gylhaut/p/5155004.html)

6. 素数与水仙花数的实现

```

    function getSushu(m,n) {
        var result=[];
        for (num=m;num<n;num++){
            for (var i=2;i<=num/2;i++){
                if (num%i==0){
                    break;
                }
            }
            if (i>num/2){
                result.push(num);
            }

        }
        console.log(result);
    }
// getSushu(2,1000);//素数的实现
    function getShuixianhuashu(m,n) {
        var result=[];
        for (var i=m;i<n;i++){
            var g=i%100%10;
            var s=parseInt(i%100/10);
            var b=parseInt(i/100);
            if (g*g*g+s*s*s+b*b*b==i){

                result.push(i);
            }
        }
        console.log(result);
    }

    getShuixianhuashu(100,1000);//水仙花数的实现

```
