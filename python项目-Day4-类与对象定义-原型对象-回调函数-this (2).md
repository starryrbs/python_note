##JavaScript 定义类或对象
1. 第一种方法创建一个对象,给这个对象以color属性
```
	var obj=new Object();
	obj.color="red";
```
2.第二种方式是使用function(){}来创建createCar类
```
function createCar(id,name){
this.id=id;
this.name=name;
this.show=function(){
console.log(this.id+this.name);

}

}
var car1=new creatCar("123","奔驰");
car1.
```

3.原型对象,是用来解决构造函数在创建实例的时候，防止重复执行所导致的性能的降低
![这里写图片描述](https://img-blog.csdn.net/20180712194501289?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM3ODkyMjIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
关键字prototype
定义方法:
```
 function User(id,name) {
        this.id=id;
        this.name=name;
        this.show=function () {
            console.log(this.id+this.name)
        }
    }

    //定义原型对象
    User.prototype.nation='usa';
```
属性放在类里面,公有属性放在原型里,所有的行为放在原型里
类的属性和原型对象时一开始定义对象的时候就有的,但是属性可以被对象修改,原型对象不可以被修改,因为原型对象是公有的.
```
 var u1=new User('sa','dada');
 u1.name="ddd";//这样是可以的,因为name是它的属性值
 u1.nation="china";//这样虽然是可以的,但是这里的nation不是它的原型对象,而是给了u1这个对象一个nation属性,当系统尝试去输出u1.nation时,会先在u1中寻找有没有nation这个属性,如果有,就输出nation属性,如果没有,就会到u1的原型对象中去寻找有没有nation属性.
```
另外,原型对象可以是属性也可以是行为.
```
	User.prototype.getColor=function () {
	    console.log(1111)
	}
	u1.getColor();
```

4.setTimeout和setInterval的区别
setTimeout是隔多少秒执行一次,只执行一次
```
var timeout=setTimeout(show,2000);
```
setInterval是每隔多长时间执行一次,循环执行
```
var inter=setInterval(show,2000)

```
5.[回调函数](https://www.cnblogs.com/lishuxue/p/5999682.html)
上面这个链接讲的比较详细

6.this的使用
this就是被谁调用谁就是this

