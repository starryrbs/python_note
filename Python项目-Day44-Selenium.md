##Python项目-Day44-Selenium
1. 什么是selenium?

	selenium 是一个用于Web应用程序测试的工具。Selenium测试直接运行在浏览器中，就像真正的用户在操作一样。支持的浏览器包括IE（7, 8, 9, 10, 11），Mozilla Firefox，Safari，Google Chrome，Opera等。这个工具的主要功能包括：测试与浏览器的兼容性——测试你的应用程序看是否能够很好得工作在不同浏览器和操作系统之上。测试系统功能——创建回归测试检验软件功能和用户需求。支持自动录制动作和自动生成 .Net、Java、Perl等不同语言的测试脚本。 
	selenium用于爬虫，主要是用来解决javascript渲染的问题 

	Selenium 可以根据我们的指令，让浏览器自动加载页面，获取需要的数据，甚至页面截屏，或者判断网站上某些动作是否发生。

	Selenium 自己不带浏览器，不支持浏览器的功能，它需要与第三方浏览器结合在一起才能使用。但是我们有时候需要让它内嵌在代码中运行，所以我们可以用一个叫 PhantomJS 的工具代替真实的浏览器。

	> 安装selenium

		pip install selenium

	[官方文档](https://selenium-python.readthedocs.io/index.html)

2. headless brower

	无头模式是运行浏览器的一种非常有用的方式。就像听起来一样，浏览器正常运行，减去任何可见的UI组件。虽然对网上冲浪不是那么有用，但它通过自动化测试自成一体。
	
	简单点说:就是不要浏览器的界面,就可以对网页进行操作.

	* windows启动无头模式

			chrome --headless --disable-gpu --dump-dom https://www.baidu.com/

	* 谷歌的无头模式

		1. 安装webdriver

			[下载地址](http://chromedriver.storage.googleapis.com/index.html)

		2. 将webdriver放入当前python代码运行的虚拟环境


3. selenium语法

	[参考网址](https://blog.csdn.net/qq_29186489/article/details/78661008)

	* 获取当前窗口

			window_1 = browser.current_window_handle


	* 获得打开的所有的窗口句柄

			windows = browser.window_handles

	* 切换到最新的窗口

		 
		    for current_window in windows:
		        if current_window != window_1:
		            browser.switch_to.window(current_window)