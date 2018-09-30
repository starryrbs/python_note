##pycharm或者webstorm的一些快捷键的设置
1.ctrl+/注释
2.删除当前行ctrl+x
 3.tab切换键
4.复制当前行ctrl+D
5.a.log按tab实现console.log(a)
##在面向对象中，函数被叫为行为或者方法
###例如:alert是window对象的一个行为
##弹窗的使用
####1.alert()
```
alert(a);
```
####2.prompt()
prompt() 方法用于显示可提示用户进行输入的对话框
```$xslt
 var res=prompt('1+1=?','请输入结果');//第一个值为提示内容，第二个为输入框默认值
    console.log(res);
```
获取到弹窗的值到res中,并打印
####js中变量的六种类型
1.number
2.string
3.boolean
4.object
5.undefined
6null
```
	a=3.12;
    s='hello';
    f=true;
    o=[];//空数组
    u=undefined;
    n=null;
```
测定变量的类型
```
console.log(typeof a);
```
######HTML连接js的两种方法
1.在内部加:
```
<script type="text/javascript">
```
2.连接外部文件:
```
<script src="../js/main.js"></script>
```
###重点:
 1.查找html元素使用querySelector方法,不要使用getElementById之类的方法
 2.判断相等时,尽量用'===',别用'==' ,恒等'==='是 **属性(值)**  **类型** 都相等,'==' 是属性(值)相等.
 3.null和undefined都是false,其中number类型中0为false,其他为true
 4.尽量别用i++这种形式,使用sec+=sec sec=sec+1,在python中是不能使用i++这种形式
 5.关系运算符的使用(优先级!>&&>||)

```
var  name="";
    name=name||'admin'//默认的用法
    name&&console.log(name);//从左往右运行,直到遇到false不运行
```
6.输出字符串加变量时使用`${变量名}`的形式
```
var a=12,b=13;
   console.log('a='+a+',b='+b)//+连接符使用  '字符串'+变量+'字符串' 例如:'a='+a+'前面是a' 结果是a=12前面是a
   console.log(`a=${a}aab=${b}`)//尽量用${}的形式输出变量+字符串
   // 别用++的形式来输出
```
7.判断变量不为空
	一般不用:
```
if(obj==''""){}
```
	而是用:
```
if(obj){}
```
