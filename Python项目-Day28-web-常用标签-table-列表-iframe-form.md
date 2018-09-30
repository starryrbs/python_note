##Python项目-Day28-web-常用标签-table-列表-iframe-form

1. webstorm快捷键

		<!--注释  ctrl + /-->
		<!--复制当前行 ctrl + D-->
		<!--删除当前行ctrl + X-->
		<!--功能键-->
		
		<!--查找 ctrl + F-->
		<!--查找替换: ctrl+r-->
		<!--折叠代码ctrl +   '-/+'-->
		<!--折叠所有代码ctrl+shift+'+/-'-->
		

2. h5标签

	* 标题标签

			<!--标题标签 标题独占一行,行间距大于普通间距 -->
			<h1>一级标题</h1>
			<h1>一级标题</h1>
			<h1>一级标题</h1>
			<h2>二级标题</h2>

	* 段落标签

			
			<!--不要出现 <h1><p></p></h1>-->
			<p>段落一</p>
			<p>段落二</p>

	* 换行标签

			<!--换行标签    换行没有结束符-->
			<br/>

	* 水平线标签

			<hr>

	* 图片标签


			<!--图片标签-->
			<img src="../images/小头.jpg" alt="logo.jpg">

	* strong和em标签

			
			<!--strong加粗字体 em倾斜字体-->
			<em><strong>PYTHON&nbsp;&nbsp;&nbsp;WEB</strong></em>

	* 空格

			&nbsp

	* &gt; 表示大于号 >  &lt;表示小于号

	* img标签和四种常用的图片

			<img src="../images/小头.jpg" alt="">

			src表示图片地址,alt表示无法显示图片时的提示文字
		
		BMP：优点（无损压缩，图质最好），缺点（文件太大，不利于网络传输）

		GIF：优点（动画存储格式），缺点（最多256色，画质差）

		PNG：优点（可保存透明背景的图片），缺点（画质中等）

		JPG：优点（文件小，利于网络传输），缺点（画质损失）

	* a标签

			<!--target _blank在新界面打开,_self是默认值表示在当前页面实现跳转-->
			<a href="0-test.html?id=3" target="_blank">go       test</a>

			<!--a标签中 href 不写值 点击会刷新界面-->
			<!--a标签中 href #### 不发生跳转 -->

	* 锚点

			<h1 id="top">


			<a href="#top">回到top标签



3. 列表


	代码快速编写   

		ul*5>li[class="li_0$"]{txt03}*2
	
		[]中表示属性,{}表示标签内容,*2表示有几个,$表示从1开始
	
		<ul>
		    <li class="li_01">txt01</li>
		    <li class="li_02">txt02</li>
		</ul>
		<ul>
		    <li class="li_01">txt01</li>
		    <li class="li_02">txt02</li>
		</ul>
		<ul>
		    <li class="li_01">txt01</li>
		    <li class="li_02">txt02</li>
		</ul>
		<ul>
		    <li class="li_01">txt01</li>
		    <li class="li_02">txt02</li>
		</ul>
		<ul>
		    <li class="li_01">txt01</li>
		    <li class="li_02">txt02</li>
		</ul>


	* 无序列表


		1.无序列表独占一行

		2.ul标签有间距

		3.li有图标

		4.结构统一

		5.li同属一个整体


			<ul>
			    <li>txt01</li>
			    <li>txt02</li>
			    <li>txt03</li>
			    <li>txt04</li>
			    <li>txt05</li>
			</ul>
		<ul>
			<li>txt01</li>
			<li>txt02</li>
			<li>txt03</li>
			<li>txt04</li>
			<li>txt05</li>
		</ul>

	* 有序标题


			<ol>
			    <li>txt01</li>
			    <li>txt02</li>
			    <li>txt03</li>
			    <li>txt04</li>
			</ol>

		<ol>
		    <li>txt01</li>
		    <li>txt02</li>
		    <li>txt03</li>
		    <li>txt04</li>
		</ol>

	* 定义列表

			<!--dl>dt{title0$}*3+dd{txt00$}*5-->
			<!--  +   表示兄弟   > 表示父子  -->
	定义列表
	自定义列表不仅仅是一列项目，而是项目及其注释的组合。
	
	自定义列表以 \<dl> 标签开始。每个自定义列表项以 \<dt> 开始。每个自定义列表项的定义以\<dd> 开始。

3. table
	
	表格

		<table border="1px" align="center">
		    <tr height="30%">
		        <td>1</td>
		        <td colspan="2">2</td>
		    </tr>
		    <tr>
		        <td rowspan="2">1</td>
		        <td>2</td>
		        <td>3</td>
		    </tr>
		    <tr>
		        <td>2</td>
		        <td>3</td>
		    </tr>
		</table>
	<table border="1px" align="center">
	    <tr height="30%">
	        <td>1</td>
	        <td colspan="2">2</td>
	    </tr>
	    <tr>
	        <td rowspan="2">1</td>
	        <td>2</td>
	        <td>3</td>
	    </tr>
	    <tr>
	        <td>2</td>
	        <td>3</td>
	    </tr>
	</table>

	table标签属性 border边界  aling对齐方式 

	tr标签表示行,内部嵌套标签td

	属性rowspan行合并

	属性colspan列合并

	table案例:
		<table border="2px" width="600px" height="500px">
		    <tr>
		        <td>星期</td>
		        <td>一</td>
		        <td>二</td>
		        <td>三</td>
		        <td>四</td>
		        <td>五</td>
		    </tr>
		    <tr>
		        <td>一</td>
		        <td>数学</td>
		        <td>语文</td>
		        <td>数学</td>
		        <td>语文</td>
		        <td>数学</td>
		    </tr>
		    <tr>
		        <td>二</td>
		        <td>数学</td>
		        <td>写字</td>
		        <td>数学</td>
		        <td>数学</td>
		        <td>数学</td>
		    </tr>
		    <tr>
		        <td colspan="6" align="center">大课间活动(30分钟)</td>
		
		    </tr>
		    <tr>
		        <td>三</td>
		        <td>语文</td>
		        <td>数学</td>
		        <td>体育与健康</td>
		        <td>美术</td>
		        <td>口语交际</td>
		    </tr>
		    <tr>
		        <td>四</td>
		        <td>语文</td>
		        <td>数学</td>
		        <td>语文</td>
		        <td>数学</td>
		        <td>语文</td>
		    </tr>
		    <tr>
		        <td>一</td>
		        <td>体育与健康</td>
		        <td>音乐</td>
		        <td>语文</td>
		        <td>音乐</td>
		        <td>数学</td>
		    </tr>
		    <tr>
		        <td>二</td>
		        <td>语文</td>
		        <td>品德与生活</td>
		        <td>美术</td>
		        <td>语文</td>
		        <td>语文</td>
		    </tr>
		    <tr>
		        <td>三</td>
		        <td></td>
		        <td>数学</td>
		        <td>体育活动健康安全</td>
		        <td>数学</td>
		        <td>少先队活动课</td>
		    </tr>
		</table>
	<table border="2px" width="600px" height="500px">
	    <tr>
	        <td>星期</td>
	        <td>一</td>
	        <td>二</td>
	        <td>三</td>
	        <td>四</td>
	        <td>五</td>
	    </tr>
	    <tr>
	        <td>一</td>
	        <td>数学</td>
	        <td>语文</td>
	        <td>数学</td>
	        <td>语文</td>
	        <td>数学</td>
	    </tr>
	    <tr>
	        <td>二</td>
	        <td>数学</td>
	        <td>写字</td>
	        <td>数学</td>
	        <td>数学</td>
	        <td>数学</td>
	    </tr>
	    <tr>
	        <td colspan="6" align="center">大课间活动(30分钟)</td>
	
	    </tr>
	    <tr>
	        <td>三</td>
	        <td>语文</td>
	        <td>数学</td>
	        <td>体育与健康</td>
	        <td>美术</td>
	        <td>口语交际</td>
	    </tr>
	    <tr>
	        <td>四</td>
	        <td>语文</td>
	        <td>数学</td>
	        <td>语文</td>
	        <td>数学</td>
	        <td>语文</td>
	    </tr>
	    <tr>
	        <td>一</td>
	        <td>体育与健康</td>
	        <td>音乐</td>
	        <td>语文</td>
	        <td>音乐</td>
	        <td>数学</td>
	    </tr>
	    <tr>
	        <td>二</td>
	        <td>语文</td>
	        <td>品德与生活</td>
	        <td>美术</td>
	        <td>语文</td>
	        <td>语文</td>
	    </tr>
	    <tr>
	        <td>三</td>
	        <td></td>
	        <td>数学</td>
	        <td>体育活动健康安全</td>
	        <td>数学</td>
	        <td>少先队活动课</td>
	    </tr>
</table>

4. iframe框架

	iframe 元素会创建包含另外一个文档的内联框架（即行内框架）。

        <iframe src="../pages/top.html" frameborder="0"></iframe>
	
		src连接到top.html
	
	[iframe详细属性](http://www.w3school.com.cn/tags/tag_iframe.asp#maincontent)


5. form表单

	form属性  action 表示表单提交执行的动作,method表示 提交的方法 get,post

	* label 标签
	* input 标签

		* text 输入框
		* password 密码框
		* radio 单选框
		* submit 提交按钮
		* checkbox多选按钮
		* button 按钮
		* reset 重置按钮
	* select 下拉列表
	* button 标签

	form表单实例:

	<form action="" method="get">
	   <p> <label for="txt_id0">用户名</label>
	       <input type="text" name="user_name" id="txt_id0"  placeholder="请输入用户名"></p>
	<p>    <input type="password" name="user_password" id="txt_pass" placeholder="请输入密码" maxlength="6">
	</p>
	    <!--单选按钮 radio 一定要写value 服务器端才能获取到-->
	    <label for="sex_male">男</label>
	    <input type="radio" name="user_sex" id="sex_male" value="2" checked>
	    <label for="fe_male">女</label>
	    <input type="radio" name="user_sex" id="fe_male" value="1">
	<p>    <input type="submit"> </p>
	<!--多选框 checkbox-->
	    <input type="checkbox" name="sport" id="chk_spot" value="sport"><label for="chk_spot">运动</label>
	    <input type="button" value="button..">
	    <input type="reset" value="clear..">
	
	    <button onclick="alert('1')">BUTTON</button>
	
	
	    <select name="sel_province" id="province">
	        <option value="jiangsu">江苏</option>
	        <option value="shandong">山东</option>
	        <option value="zhejiang">浙江</option>
	        <option value="shanghai" selected>上海</option>
	    </select>
	    <label for="province">省</label>
	</form>
		<form action="" method="get">
		   <p> <label for="txt_id0">用户名</label>
		       <input type="text" name="user_name" id="txt_id0"  placeholder="请输入用户名"></p>
		<p>    <input type="password" name="user_password" id="txt_pass" placeholder="请输入密码" maxlength="6">
		</p>
		    <!--单选按钮 radio 一定要写value 服务器端才能获取到-->
		    <label for="sex_male">男</label>
		    <input type="radio" name="user_sex" id="sex_male" value="2" checked>
		    <label for="fe_male">女</label>
		    <input type="radio" name="user_sex" id="fe_male" value="1">
		<p>    <input type="submit"> </p>
		<!--多选框 checkbox-->
		    <input type="checkbox" name="sport" id="chk_spot" value="sport"><label for="chk_spot">运动</label>
		    <input type="button" value="button..">
		    <input type="reset" value="clear..">
		
		    <button onclick="alert('1')">BUTTON</button>
		
		
		    <select name="sel_province" id="province">
		        <option value="jiangsu">江苏</option>
		        <option value="shandong">山东</option>
		        <option value="zhejiang">浙江</option>
		        <option value="shanghai" selected>上海</option>
		    </select>
		    <label for="province">省</label>
		</form>


5. 纯html语言实现51job.com登录界面


<table width="100%" height="800px" >
    <tr height="15%"><td>
        <table>
            <tr>
                <td>
                    <img src="../images/前程无忧_logo.jpg" alt="">
                </td>
                <td>
                    <img src="../images/前程无忧.jpg" alt="">
                </td>
                <td width="50%">
                    <a href="#">欢迎登录</a>
                </td>
                <td width="5%">
                    <a href="#">首页</a>
                </td>
                <td>
                    <a href="#">帮助中心</a>
                </td>
            </tr>
        </table></td></tr>
    <tr height="80%"><td>
        <table width="100%" height="90%">
            <tr>
                <td>
                    <ul type="none">
                        <li><img src="../images/1.jpg" alt=""><br><a href="">便捷的简历填写</a><br><a href="">一份简历开启未来</a></li>
                        <li><img src="../images/2.jpg" alt=""><br><a href="">海量的职位优选</a><br><a href="">360行任你挑选</a></li>
                        <li><img src="../images/3.jpg" alt=""><br><a href="">快速的职位投递</a><br><a href="">分秒必争直达HR</a></li>
                        <li><img src="../images/4.jpg" alt=""><br><a href="">高效的投递反馈</a><br><a href="">谁看我简历早知道</a></li>
                    </ul>
                </td>
                <td>
                    <table width="300px" height="400px" border="1px">
                        <tr><td>登录</td></tr>
                        <tr><td>账号</td></tr>
                        <tr><td><input type="text" placeholder="请输入手机号码/邮箱/用户名"></td></tr>
                        <tr><td>密码</td></tr>
                        <tr><td><input type="text" placeholder="请输入密码"></td></tr>
                        <tr><td><input type="checkbox">自动登录&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;忘记密码?</td></tr>
                        <tr><td><input type="submit"  value="登录"></td></tr>
                        <tr><td>还没有账号?<a href="#">免费注册</a><img src="../images/z11111111111111111111111.jpg" alt=""></td></tr>
                        <tr><td>温馨提示：用人单位招聘人才，<br>以任何名义向应聘者收取费用都是不被法律允许的<br>，请应聘者提高警惕！求职者要时刻睁大眼睛，<br>谨防招聘骗局。 查看详情</td></tr>
                    </table></td>
            </tr>
        </table></td></tr>
    <tr height="5%"><td>未经51Job同意，不得转载本网站之所有招聘信息及作品 | 无忧工作网版权所有©1999-2018</td></tr>
</table>


	<table width="100%" height="800px" >
	    <tr height="15%"><td>
	        <table>
	            <tr>
	                <td>
	                    <img src="../images/前程无忧_logo.jpg" alt="">
	                </td>
	                <td>
	                    <img src="../images/前程无忧.jpg" alt="">
	                </td>
	                <td width="50%">
	                    <a href="#">欢迎登录</a>
	                </td>
	                <td width="5%">
	                    <a href="#">首页</a>
	                </td>
	                <td>
	                    <a href="#">帮助中心</a>
	                </td>
	            </tr>
	        </table></td></tr>
	    <tr height="80%"><td>
	        <table width="100%" height="90%">
	            <tr>
	                <td>
	                    <ul type="none">
	                        <li><img src="../images/1.jpg" alt=""><br><a href="">便捷的简历填写</a><br><a href="">一份简历开启未来</a></li>
	                        <li><img src="../images/2.jpg" alt=""><br><a href="">海量的职位优选</a><br><a href="">360行任你挑选</a></li>
	                        <li><img src="../images/3.jpg" alt=""><br><a href="">快速的职位投递</a><br><a href="">分秒必争直达HR</a></li>
	                        <li><img src="../images/4.jpg" alt=""><br><a href="">高效的投递反馈</a><br><a href="">谁看我简历早知道</a></li>
	                    </ul>
	                </td>
	                <td>
	                    <table width="300px" height="400px" border="1px">
	                        <tr><td>登录</td></tr>
	                        <tr><td>账号</td></tr>
	                        <tr><td><input type="text" placeholder="请输入手机号码/邮箱/用户名"></td></tr>
	                        <tr><td>密码</td></tr>
	                        <tr><td><input type="text" placeholder="请输入密码"></td></tr>
	                        <tr><td><input type="checkbox">自动登录&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;忘记密码?</td></tr>
	                        <tr><td><input type="submit"  value="登录"></td></tr>
	                        <tr><td>还没有账号?<a href="#">免费注册</a><img src="../images/z11111111111111111111111.jpg" alt=""></td></tr>
	                        <tr><td>温馨提示：用人单位招聘人才，<br>以任何名义向应聘者收取费用都是不被法律允许的<br>，请应聘者提高警惕！求职者要时刻睁大眼睛，<br>谨防招聘骗局。 查看详情</td></tr>
	                    </table></td>
	            </tr>
	        </table></td></tr>
	    <tr height="5%"><td>未经51Job同意，不得转载本网站之所有招聘信息及作品 | 无忧工作网版权所有©1999-2018</td></tr>
	</table>