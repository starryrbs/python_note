##Python项目-Day38-offsetWidth、offsetHeight-offsetLeft和offsetTop-js的事件冒泡和事件捕获

1. offsetWidth、offsetHeight

	这两个属性的值只与该元素有关， 与周围的元素（父级与子级元素无关）。
	
	offsetWidth=border-left+padding-left+padding-right+border-right+元素本身宽度

	offsetHeight=border-top+padding-top+padding-bottom+border-bottom+元素本身高度


2. offsetLeft和offsetTop

	这两个属性与该元素的offsetParent元素有关

	offsetParent是该元素的父元素,但是是第一个非static定位(position不等于static)的元素,一直往上找.

	offsetTop=margin-top+padding-top+border-top

	offsetLeft同理



3. scrollTop,scrollLeft

   	这两个属性是相对于滚动条,垂直位置，当滚动条不存在的时候，obj.scrollLeft 和obj.scrollTop的值为0，滚动条存在的时候， 不同位置值是不同的。
	
	简单点说,就是滚动条滚动的长度

	举例:

		window.onscroll=function () {
		        var scrollTop = document.documentElement.scrollTop || window.pageYOfset ||document.body.scrollTop;
		        console.log(scrollTop)
		    }

	[scrollTop的浏览器适配问题](https://blog.csdn.net/qq_40963664/article/details/78463286)
4. js的事件冒泡和事件捕获


	本文章转自:[地址](https://www.cnblogs.com/qq9694526/p/5653728.html)

	先上结论：他们是描述事件触发时序问题的术语。事件捕获指的是从document到触发事件的那个节点，即自上而下的去触发事件。相反的，事件冒泡是自下而上的去触发事件。绑定事件方法的第三个参数，就是控制事件触发顺序是否为事件捕获。true,事件捕获；false,事件冒泡。默认false,即事件冒泡。Jquery的e.stopPropagation会阻止冒泡，意思就是到我为止，我的爹和祖宗的事件就不要触发了。

	这是HTML结构

		<div id="parent">
		　　<div id="child" class="child"></div>
		</div>

	现在我们给它们绑定上事件
	
        document.getElementById("parent").addEventListener("click",function(e){
            alert("parent事件被触发，"+this.id);
        })
        document.getElementById("child").addEventListener("click",function(e){
            alert("child事件被触发，"+this.id)
        })
	结果：
	
	child事件被触发，child
	parent事件被触发，parent
	结论：先child，然后parent。事件的触发顺序自内向外，这就是事件冒泡。
	
	现在改变第三个参数的值为true
	
		document.getElementById("parent").addEventListener("click",function(e){
		                alert("parent事件被触发，"+e.target.id);
		            },true)
		document.getElementById("child").addEventListener("click",function(e){
		                alert("child事件被触发，"+e.target.id)
		            },true)



	结果：
	
	parent事件被触发，parent

	child事件被触发，child

	结论：先parent,然后child。事件触发顺序变更为自外向内，这就是事件捕获。
	
	貌似没什么卵用，上一个利用事件冒泡的案例，反正我是经常会用到。
	
	
	
		<ul>
            <li>item1</li>
            <li>item2</li>
            <li>item3</li>
            <li>item4</li>
            <li>item5</li>
            <li>item6</li>
        </ul>
	
	需求是这样的：鼠标放到li上对应的li背景变灰。
	
	利用事件冒泡实现：
	
		$("ul").on("mouseover",function(e){
            $(e.target).css("background-color","#ddd").siblings().css("background-color","white");
        })

	也许有人会说，我们直接给所有li都绑上事件也可以啊，一点也不麻烦，只要……

	
		$("li").on("mouseover",function(){
            $(this).css("background-color","#ddd").siblings().css("background-color","white");
        })

	是，这样也行。而且从代码简洁程度上，两者是相若仿佛的。但是，前者少了一个遍历所有li节点的操作，所以在性能上肯定是更优的。
	
	还有就是，如果我们在绑定事件完成后，页面又动态的加载了一些元素……
	
		$("<li>item7</li>").appendTo("ul");
	这时候，第二种方案，由于绑定事件的时候item7还不存在，所以为了效果，我们还要给它再绑定一次事件。而利用冒泡方案由于是给ul绑的事件……
	
	高下立判！