##Python项目-Day39-ajax
1. 什么是ajax?

	ajax 即“Asynchronous JavaScript and XML”（异步 JavaScript 和 XML），也就是无刷新数据读取。

2. 创建ajax对象

		if(window.XMLHttpRequest){//ie6以上支持
		      oAjax = new XMLHttpRequest();
		  }else{
		      oAjax = new ActiveXObject('Microsoft.XMLHTTP');//ie6以下支持
		  }

3. 连接到服务器

 	在这里会用到 open() 方法。启动一个请求以备发送。open() 方法有三个参数

	* 第一个参数是连接方法即 GET 和 POST，
	* 第二个参数是 URL 即所要读取数据的地址，
	* 第三个参数是否异步，它是个布尔值，true 为异步，false 为同步。


	如果您希望通过 GET 方法发送信息，请向 URL 添加信息
   但是url加的查询字符串必须使用 encodeURICompent()进行编码才能加入。
	* encodeURI()和encodeURIComponent()的区别

	其中encodeURI()主要用于整个URI(例如，http://www.jxbh.cn/illegal value.htm)，而encode-URIComponent()主要用于对URI中的某一段(例如前面URI中的illegal value．htm)进行编码。它们的主要区别在于，encodeURI()不会对本身属于URI的特殊字符进行编码，例如冒号、正斜杠、问号和井字号；而encodeURIComponent()则会对它发现的任何非标准字符进行编码。

		//encodeURIComponent
		function addURLParam(url,name,value) {
		                   url+=(url.indexOf("?")==-1)?"?":"&";
		                   url+=encodeURIComponent(name)+"="+encodeURIComponent(value);
		                   return url;
		               }

		//encodeURI
		function addURLPararm(url,data) {
		    for (let k in data){
		
		        console.log(data.k);
		        url+=url.indexOf('?')<0?'?'+k+'='+data.k:'&'+k+'='+data.k;
		        console.log(url);
		    }
		    console.log(url);
		    url=encodeURI(url);
		    return url
		}