##Python项目-Day18-多线程
1. 多线程基础

	* 多线程:类似于同时执行多个不同的程序

	* 多线程的优点
		1. 多线程可以使占据长时间的程序放到后台去处理
		2. 程序的运行速度可能更快,但是如果是一个简单的操作,就没必要使用多线程
		3. 在一些等待的任务实现上如用户输入、文件读写和网络收发数据等，线程就比较有用。在这种情况下我们可以释放一些珍贵的资源，如内存占用。

	* 多线程的创建:
	

		导入threading包

		import threading

		创建一个线程对象,target执行的方法

		t = threading.Thread(target=action, args=(i,))
		args是将元组里面的值传到action函数中作为形参

			import time
			def action(n):
				time.sleep(1)
				print('i am action {}'.format(threading.current_thread))
				print('my name is',n)
			
			if __name__=='__main__':
				print("当前线程是:{}".format(threading.current_thread()))
				for i in range(10)
					tt=threading.Thread(target=action,args=(i,))
					tt.start()
				print("我是老板,开始干活")

	* 用类来封装线程对象

			import threading
			import time
			
			class MyThread(threading.Thread):
				def __init__(self,arg):
					super(MyThread,self).__init__()
					#注意:一定要显示的调用父类Thread的初始化函数
					self.arg=arg
				def run(self):
					#每个线程执行的函数
					time.sleep(1)
					print('the arg is :%s\r' self.arg)
				for i in range(10)
					t=MyThread(i)
					t.start()
					#调用线程对象的start方法,start方法会去调用对象的run方法

		>Thread类的构造方法的参数:

		* target: 线程要执行的方法

		* name:线程名

		* args/kwargs:要传入方法的参数

		> Thread类对象的实例方法

		* isAlive()返回线程是否正在运行。
		* get/setName(name):获取/设置线程名
		* start():线程准备就绪,等待cpu调度
		* join([timeout]):阻塞当前上下文环境的线程,直到调用此方法的线程终止或到达指定的timeout
		> threading模块常用的方法
		* threading.currentThread():返回当前正在运行的线程
		* threading.enumerate():返回一个包含所有正在运行进程的list,查看当前当前有多少线程正在运行,只需要求这个list的长度
		* threading.activeCount(): 等于len(threading.enumerate)

		>  后台线程和前台线程
		
		is/setDaemon(bool)

		False(默认):获取/设置是前天线程,True:获取/设置后台线程

		即:	设置为False线程是在前台运行的,主线程需要等待子线程运行完才结束,
			设置为True,线程是在后台运行的,主线程一旦运行完,会直接关闭程序,而这些后台线程也会被相应的关闭.

	* join方法:
		
		join方法阻塞上下文环境的线程,知道调用此方法的线程终止或到达指定的timeout,即使设置了setDeamon(True)主线程依然要等待子线程结束。简单点说就是先让子线程全部执行完，在让主线程去执行

		与setDeamon方法不同的调用步骤

		setDeamon（）=>start()

		start()=>join

		执行步骤不能错误

2. 多线程的应用

	未完待续

