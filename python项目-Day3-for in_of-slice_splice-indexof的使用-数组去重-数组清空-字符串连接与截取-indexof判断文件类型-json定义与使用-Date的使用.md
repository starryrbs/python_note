1. 数组
 ####数组的遍历:
1.for in得到数组的索引
	```
	for (var index in arr01){//index为arr01的长度
	console.log(index);
	console.log(arr01[index]);
	```
	2.for of得到数组的值
	```
	for (var item of arr01){//item为得到的值
	        item*=3;
	    }	    
	```


	#####数组的应用

	1. slice
			```
			var new_arr=arr01.slice(0,2);//截取数组包括0不包括2,slice并不改变原数组
			```	
	2. splice

	删除:用于删除元素,两个参数,第一个参数(要删除的第一项的位置),第二个参数(要删除的项数)
    插入:向数组指定位置插入任意项元素.三个参数,第一个参数(插入的起始位置),第二个参数(0),第三个参数(插入的项)
    替换:将数组指定位置到指定位置的元素替换为任意项元素,三个参数,第一个参数(替换的起始位置),第二个参数(替换的终止位置),第三个参数(要替换的元素)
	```
	//0表示起始位置，3表示截取个数
	var new_arr02=arr01.splice(0,3,"a","b");//slice不该变原数组，splice改变原数组
	```
	3. indexof
	```
	var arr01=[1,3,4,5,32,2,1,3,4,6];
	   var new_arr=[];
	//indexof判断元素是否在数组中，如果存在元素则返回该元素的位置，否则返回-1
	   // alert(arr01.indexOf(32))
	```
	4. 数组去重

		```
		for (var item of arr01){
		if (new_arr.indexOf(item)==-1){//判断在这个数组中有没有这个数，如果有，
		  // 就不将这个数据添加到新数组，如果没有就添加到新数组，以达到数组去重复的效果
		            new_arr.push(item);
		        }
		    }
		```

	5. 数组清空

	```
	arr01.splice(0,arr01.length);//第一种方式
    arr01=[];//第二种方式
	```
2. String

######字符串连接
```
	var s1='hello world';
    var  s2='world';
    console.log(s1 + s2);//第一种连接,直接用+号
    var s3=s1.concat(s2);//第二种连接使用concat,效果是一样的
```
######字符串截取
```
var new_s1=s1.substr(6,5);//6开始位置,5表示截取几个

var date='2018-07-01';
var arr=date.split('-');    //split按指定分隔符截取字符串,结果为数组

```
substr和split两种方式截取字符串都可以,前者根据位置,而后者根据分隔符截取

######将字符串全部转化为大写

```
console.log(s1.toUpperCase());//全部转化为大写
```
######判断字符串是否是邮箱
```
var email='lzhan@163.com.cn';
    var index_at=email.indexOf('@');
    var  index_point=email.lastIndexOf('.');
    console.log(index_at);
    console.log(index_point);
		//1.判断@的位置大于0
		//2..的位置要在@的后面,也就是.的下标大于@的下标
		//3.判断.后面至少有两个字符
    if (index_at>0&&index_point-index_at>1&&index_point<email.length-2){
        alert("yes");
        } else {
        alert("no");
}
```
######判断文件类型
```
	var file='user.png.jpg';
    var file_type=file.split('.').pop();//pop用于删除并返回数组的最后一个元素
```

3.json

json是一种轻量级的数据交换格式

######json的定义
```
 var goods=[
        {"id":"001","name":"iphone6","color":["grey","black"]},
        {"id":"002","name":"iphone6s","camara":{"productor":"sony"}},
        {"id":"003","name":"iphone7"},
        {"id":"004","name":"iphone8"},
        {"id":"005","name":"iphone10"},
    ];
```
######json的遍历
```
for (var good of  goods) {
	console.log(good.name);
}



//1.将json转化为字符串
var str_user=JSON.stringify(user);//将json转化为字符串
//2.将字符串转化为json
var json_user=JSON.parse(str_user);
```
#####json的小示例
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<style>
    .container{
        width: 600px;
        height: 300px;
        background: #b3ff8d;
        margin: 0 auto;
    }
    table{
        width: 100%;
    }
    td{
        width: 25%;
    }
</style>
<body>
<div class="container">
    <table id="con_goods">
        <tr>
            <td>序号</td>
            <td>名称</td>
            <td>价格</td>
            <td>销量</td>
        </tr>
    </table>
</div>
<script type="text/javascript">
    var goods=[
        {"id":"001","name":"iphone6","price":1221},
        {"id":"002","name":"iphone6s","price":1221},
        {"id":"003","name":"iphone7","price":1221},
        {"id":"004","name":"iphone8","price":1221},
        {"id":"005","name":"iphone10","price":1221},
    ];

	//  1.获取容器(table的id,要装在table里面)
    var con=document.querySelector('#con_goods');
   
    //2.遍历数据
    for(var item of goods){
        con.innerHTML+=`//使用+=,先获取原有的数据,在将现有数据加到界面上
        <tr onclick="show(${item.id})">
            <td>${item.id}</td>
            <td>${item.name}</td>
            <td>${item.price}</td>
        </tr>


        `
    }
    function show(id) {
        alert(id);
    }
</script>
</body>
</html>
```
4.Date()
#####Date的应用
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<style></style>
<body>
<div id="show_time"></div>
<script type="text/javascript">
//计算两个时间的相差时间
    function timeFormat(start_time,end_time) {
        var time=(new Date(end_time)-new Date(start_time))/1000;
        var days=parseInt(time/(60*60*24));
        var hour=parseInt(time%(60*60*24)/(60*60));
        var minute=parseInt(time%(60*60)/60);
        var seconds=parseInt(time%60);

        return `${days}天${hour}小时${minute}分钟${seconds}秒`
        // return time;
    }
// setInterval(function () {
//     console.log(timeFormat(new Date(),'2018-8-7'));
//
// },1000);
console.log(new Date());

    function curruentTime() {
        var time=new Date();
        var year=time.getFullYear();
        var month=time.getMonth()+1;
        var days=time.getDate();
        var hour=time.getHours();
        var minute=time.getMinutes();
        var second=time.getSeconds();
        console.log(`${year}年${month}月${days}日${hour}时${minute}分${second}秒`);
    }
curruentTime();


    
	// var a=10;
    // var f=a>93?a:'0'+a;
    // console.log(f);

    
</script>
</body>
</html>
```

####练习:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>数组排序</title>
</head>
<body>


<script type="text/javascript">
    //用冒泡排序和选择排序实现数组排序
    var a=[2,1,5,3,9,4,121,21,32,43,2,1,312,21];

    //冒泡排序
    function maopao(a) {
        var t;

        for (var j=0;j<a.length;j++) {
            for (var i=0;i<a.length-1;i++){

                if (a[i]<a[i+1]){
                    t=a[i+1];
                    a[i+1]=a[i];
                    a[i]=t;

                }


            }}
            return a;
    }

    // console.log(maopao(a));

    //选择排序
    function xuanze(a) {
        var t;
        for (j=0;j<a.length;j++){
            for (var i=0;i<a.length-j;i++){
                if (a[i]<a[a.length-1-j]){
                    t=a[a.length-1-j];
                    a[a.length-1-j]=a[i];
                    a[i]=t;

                }
            }}
            return a;
    }

    console.log(xuanze(a));
</script>
</body>
</html>

```
	

