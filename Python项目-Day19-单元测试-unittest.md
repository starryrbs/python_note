##Python项目-Day19-单元测试-unittest
1. unittest(测试模块)

	unittest中最核心的四个概念是：test case, testsuite,testrunner,test fixture

	TestCase(测试用例):所有测试用例的基类,它是软件测试中最基本的组成单元。

	TestSuite(测试套件):多个测试用例testcase集合就是Testsuite,Testsuite可以嵌套Testsuite

	TestLoder:用来加载TestCase到TestSuite中,其中有几个loadTestForm()方法,就是从各个地方寻找TestCase,创建他们的实例,然后add到TestSuite,再返回一个TestSuite实例
	
	TextTestRunner:是来执行测试用例的,其中的run(test)会执行TestSuite/TestCase中的run(result)方法
	
	TextTestResult:测试结果会保存到TextTestResult实例中,包括运行了多少用例,成功与失败多少等信息
	
	TestFixture:又叫测试脚手,测试代码的运行环境,指测试准备前和执行后要做的工作,包括setUp和tearDown方法

2. 测试小示例

	新建一个py文件叫test_func1


		#导入unittest
		import unittest
		#导入要测试的方法所在的模块
		from unit16.单元测试.func1 import *
		#创建一个测试类Testfunc,继承unittest.TestCase
		class Testfunc1(unittest.TestCase):
			#写一个方法来测试
		    def test_add(self):
		        self.assertEqual(5,add(1,2))
		#在name=main运行
		if __name__ == '__main__':
		    unittest.main()
	
	一个类继承了unittest.TestCase,便是一个测试用例
	>注意:测试类里面的测试方法必须以test开头,例如test_add,写成
	>te_add是错误的,并不会执行这个方法.
	每一个方法都会生成一个TestCase实例
	
	通过运行unittest.main()执行时,会调用TextTestRunner中的run来执行,或者可以直接通过TextTestRunner来执行用例

3. TestSuite(测试套件)

	可以将多个TestCase放到TestSuite中测试
	
	使用TestSuite的原因

		1. 确定测试用例的顺序，哪个先执行哪个后执行？
		2. 如果测试文件有多个，怎么进行组织？

		import unittest
		from unit16.单元测试.func1 import *
		from unit16.单元测试.test_func1 import Testfunc1
		if __name__ == '__main__':
		    suite=unittest.TestSuite()
		    tests=[Testfunc1("test_add")]
			#使用addTests方法将TestCase列表添加,可以确定case的执行顺序
		    suite.addTests(tests)
		    runner=unittest.TextTestRunner(verbosity=2)
		    runner.run(suite)

	将测试报告写到文件中:

	    with open('report.txt','w',encoding='utf-8') as f:
	        runner = unittest.TextTestRunner(stream=f,verbosity=2)
	        runner.run(suite)

4. unittest中的参数化

		pip install nose_parameterized



		import unittest
		from unit16.单元测试.func1 import *
		from parameterized import parameterized
		class Testfunc1(unittest.TestCase):
		    def test_decline(self):
		        self.assertEqual(3,decline(1,2))
		
		    @parameterized.expand(
		        [
		            ['xiaogang', '123456', True],  # 可以是list，也可以是元祖
		            ['', '123456', True],
		            ['xiaogang', '', False],
		            ['admin', '123', False]
		        ]
		    )#在测试方法上面加上装饰器,写上数据,然后在测试方法添加对应的参数
		    def test_login(self,user,password,base):
		        self.assertEqual(login(user,password),base)
		
		
		if __name__ == '__main__':
		    unittest.main()

5. setUp()和tearDown()方法

	setUp:用来为测试准备环境,测试开始前执行此方法
	tearDown:用来清理环境,以备之后的测试

	    def setUp(self):
	        print("开始准备环境")
	    def tearDown(self):
	        print("开始清理环境")
	这两个方法会被多次执行,即每次执行case案例都会执行这两个方法

	若指向执行一个
	可以使用setUpClass()方法和tearDownClass方法
	>注意,这两个方法使用前要加上装饰器@classmethod

		@classmethod
		    def setUpClass(cls):
		        print("开始准备环境")
		    @classmethod
		    def tearDownClass(cls):
		        print("开始清理环境")

6. 跳过某个case

	使用skip装饰器
		
	1. unittest.skip(reason)
	

			@unittest.skip("不想执行此方法")
			    def test_decline(self):
			        self.assertEqual(3,decline(1,2))

	2. unittest.skipIf(condition,reason)(满足条件执行skip)

			num=1
			    @unittest.skipIf(num>0,"不想执行此方法")
			    def test_decline(self):
			        self.assertEqual(3,decline(1,2))
	3. unittest.skipUnless(condition,reason)(不满足条件执行skip)


			num=1
			    @unittest.skipUnless(num<0,"不想执行此方法")
			    def test_decline(self):
			        self.assertEqual(3,decline(1,2))

7. 用HTMLTestRunner输出漂亮的HTML报告

	在工程目录导入HTMLTestRunner.py
	[Python3.x版本：](http://pan.baidu.com/s/1tp3Ts​)

	    with open('report1.html','w',encoding='utf-8') as f:
	        runner=HTMLTestRunner(
	            stream=f,
	            title='aa',
	            description='aaa',
	            verbosity=2,
	        )
	        runner.run(suite)

8. 总结

	1. unittest是Python自带的单元测试框架，我们可以用其来作为我们自动化测试框架的用例组织执行框架。
	2. unittest的流程：写好TestCase，然后由TestLoader加载TestCase到TestSuite，然后由TextTestRunner来运行TestSuite，运行的结果保存在TextTestResult中，我们通过命令行或者unittest.main()执行时，main会调用TextTestRunner中的run来执行，或者我们可以直接通过TextTestRunner来执行用例。
	3. 一个class继承unittest.TestCase即是一个TestCase，其中以 test 开头的方法在load时被加载为一个真正的TestCase。
	4. verbosity参数可以控制执行结果的输出，0 是简单报告、1 是一般报告、2 是详细报告。
	5. 可以通过addTest和addTests向suite中添加case或suite，可以用TestLoader的loadTestsFrom__()方法。
	6. 用 setUp()、tearDown()、setUpClass()以及 tearDownClass()可以在用例执行前布置环境，以及在用例执行后清理环境
	7. 我们可以通过skip，skipIf，skipUnless装饰器跳过某个case，或者用TestCase.skipTest方法。
	8. 参数中加stream，可以将报告输出到文件：可以用TextTestRunner输出txt报告，以及可以用HTMLTestRunner输出html报告。


