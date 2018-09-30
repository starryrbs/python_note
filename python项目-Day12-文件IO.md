##Python项目-Day12-文件IO

1. 读取文件和写入文件

	* 建立通道
	
			file object = open(file_name [, access_mode][, buffering])

	各个参数的细节如下：
	
	file_name：file_name变量是一个包含了你要访问的文件名称的字符串值。

	access_mode：access_mode决定了打开文件的模式：只读，写入，追加等。所有可取值见如下的完全列表。这个参数是非强制的，默认文件访问模式为只读(r)。

	![](https://i.imgur.com/ws8gFTF.png)
	![](https://i.imgur.com/kEZ0WpV.png)

	buffering:如果buffering的值被设为0，就不会有寄存。如果buffering的值取1，访问文件时会寄存行。如果将buffering的值设为大于1的整数，表明了这就是的寄存区的缓冲大小。如果取负值，寄存区的缓冲大小则为系统默认。

4. 目录

	1. ./ 当前目录
	2. ../上一级目录
	3. /下一级目录


3. seek

	语法

		fileObject.seek(offset[, whence])

	参数

	* offset -- 开始的偏移量，也就是代表需要移动偏移的字节数

	* whence：可选，默认值为 0。给offset参数一个定义，表示要从哪个位置开始偏移；0代表从文件开头开始算起，1代表从当前位置开始算起，2代表从文件末尾算起。

4. flush()

    flush() 方法是用来刷新缓冲区的，即将缓冲区中的数据立刻写入文件，同时清空缓冲区，不需要是被动的等待输出缓冲区写入。

    一般情况下，文件关闭后会自动刷新缓冲区，但有时你需要在关闭前刷新它，这时就可以使用 flush() 方法。


5. 内存读写

	1. StringIO在内存中读写str

			from io import StringIO
	
			f = StringIO()
			# f.write('hello')
			# f.write('python')
			f.write('!')
			
			print(f.getvalue())
			
			
		写入多行语句
		
			f = StringIO('Hello!\nHi!\nGoodbye!')
			
			for line in f:
				print(line)
				
	2. 二进制数据，就需要使用BytesIO

				from io import BytesIO
				f = BytesIO()
				f.write('中文'.encode('utf-8'))
				print(f.getvalue())
				
				f = BytesIO(b'\xe4\xb8\xad\xe6\x96\x87')
				
				f.read()