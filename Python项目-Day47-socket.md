##Python项目-47-socket
1. socket介绍

	Socket 是任何一种计算机网络通讯中最基础的内容.

	第一个是 Socket，它提供了标准的 BSD Sockets API。

	第二个是 SocketServer， 它提供了服务器中心类，可以简化网络服务器的开发。

2. socket类型

	导入socket

		from socket import *

	创建一个套接字

		sock= socket(family,type[,protocal]),使用给定的地址族、套接字类型、协议编号（默认为0）来创建套接字。

	socket类型|描述
	--|--|
	socket.AF_UNIX|只能够用于单一的Unix系统进程间通信
	socket.AF_INET|服务器之间网络通信
	socket.AF_INET6|IPv6
	socket.SOCK_STREAM|流式socket , for TCP
	socket.SOCK_DGRAM|数据报式socket , for UDP
	socket.SOCK_RAW|原始套接字，普通的套接字无法处理ICMP、IGMP等网络报文，而SOCK_RAW可以；其次，SOCK_RAW也可以处理特殊的IPv4报文；此外，利用原始套接字，可以通过IP_HDRINCL套接字选项由用户构造IP头。
	socket.SOCK_SEQPACKET|可靠的连续数据包服务
	创建TCP Socket：|s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
	创建UDP Socket：|s=socket.socket(socket.AF_INET,socket.SOCK_DGRAM)

3. socket函数

	1. TCP发送数据时，已建立好TCP连接，所以不需要指定地址。UDP是面向无连接的，每次发送要指定是发给谁。
	2. 服务端与客户端不能直接发送列表，元组，字典。需要字符串化repr(data)。
	

	socket函数|描述
	--|--
	server函数|
	s.bind(address)|将套接字绑定到地址, 在AF_INET下,以元组（host,port）的形式表示地址.
	s.listen(backlog)|开始监听TCP传入连接。backlog指定在拒绝连接之前，操作系统可以挂起的最大连接数量。该值至少为1，大部分应用程序设为5就可以了。
	s.accept()|接受TCP连接并返回（conn,address）,其中conn是新的套接字对象，可以用来接收和发送数据。address是连接客户端的地址。
	client函数|
	s.connect(address)|连接到address处的套接字。一般address的格式为元组（hostname,port），如果连接出错，返回socket.error错误。
	s.connect_ex(adddress)|功能与connect(address)相同，但是成功返回0，失败返回errno的值。
	公共socket函数|
	s.recv(bufsize[,flag])|接受TCP套接字的数据。数据以字符串形式返回，bufsize指定要接收的最大数据量。flag提供有关消息的其他信息，通常可以忽略。
	s.send(string[,flag])|发送TCP数据。将string中的数据发送到连接的套接字。返回值是要发送的字节数量，该数量可能小于string的字节大小。
	s.sendall(string[,flag])|完整发送TCP数据。将string中的数据发送到连接的套接字，但在返回之前会尝试发送所有数据。成功返回None，失败则抛出异常。
	s.recvfrom(bufsize[.flag])|接受UDP套接字的数据。与recv()类似，但返回值是（data,address）。其中data是包含接收数据的字符串，address是发送数据的套接字地址。
	s.sendto(string[,flag],address)|发送UDP数据。将数据发送到套接字，address是形式为（ipaddr，port）的元组，指定远程地址。返回值是发送的字节数。
	s.close()|关闭套接字。
	s.getpeername()|返回连接套接字的远程地址。返回值通常是元组（ipaddr,port）。
	s.getsockname()|返回套接字自己的地址。通常是一个元组(ipaddr,port)
	s.setsockopt(level,optname,value)|设置给定套接字选项的值。
	s.getsockopt(level,optname[.buflen])|返回套接字选项的值。
	s.settimeout(timeout)|设置套接字操作的超时期，timeout是一个浮点数，单位是秒。值为None表示没有超时期。一般，超时期应该在刚创建套接字时设置，因为它们可能用于连接的操作（如connect()）
	s.gettimeout()|返回当前超时期的值，单位是秒，如果没有设置超时期，则返回None。
	s.fileno()|返回套接字的文件描述符。
	s.setblocking(flag)|如果flag为0，则将套接字设为非阻塞模式，否则将套接字设为阻塞模式（默认值）。非阻塞模式下，如果调用recv()没有发现任何数据，或send()调用无法立即发送数据，那么将引起socket.error异常。
	s.makefile()|创建一个与该套接字相关连的文件

4. socket编程思路
	
	导入socket

		from socket import *
		
	TCP服务端:
	
	1. 创建套接字,绑定套接字到本地IP与端口

			sock=socket(AF_INET,SOCK_STREAM)
			ip_port=("127.0.0.1",8080)
			sock.bind(ip_port)

	2. 开始监听连接

			sock.listen(5)

	3. 进入循环,不断接收客户端的请求

			sock.accept()

	4. 然后接收传来的数据,并返回数据给对方
			
			#1024表示一次接收多少字节
			sock.recv(1024)
			#接收的返回值是一个元组,第一个值是ip:port,第二个值是:接收的消息
			sock.recvfrom(1024)
			#sendto有两个参数,第一个是要发送的信息,第二个参数是一个元组(ip,port),例如("127.0.0.1",8080)
			sock.sendto("哈哈".encode(),("127.0.0.1",8080))
	
	TCP客户端:

	1. 创建套接字,连接远端地址

			sock=socket(AF_INET,SOCK_STREAM)
			sock.connect(('127.0.0.1',8097))

	2. 连接后发送数据和接收数据

			sock.recvfrom(1024)
			sock.sendto("哈哈".encode(),("127.0.0.1",8080))

	3. 传输完毕后,关闭套接字

			sock.close()

5. socket流程图

	![](https://i.imgur.com/8duygnn.jpg) 

6. socket-Demo

	socket-client.py

		from socket import *
		
		udpSocket=socket(AF_INET,SOCK_DGRAM)
		
		udpSocket.connect(('127.0.0.1',8097))
		while True:
		    input_text=input("请输入----")
		    udpSocket.send(input_text.encode())

	socket-server.py


		from socket import *
		
		udpSocket=socket(AF_INET,SOCK_DGRAM)
		ip_port=("127.0.0.1",8097)
		udpSocket.bind(ip_port)
		while True:
		    recvInfo= udpSocket.recvfrom(1024)
		    print("{}:{}".format(str(recvInfo[1]),recvInfo[0].decode()))
		    udpSocket.sendto(recvInfo[0],recvInfo[1])

7. 模仿QQ-多线程

		from threading import Thread
		from socket import *
		
		udpSocket=None
		desIp=""
		desPort=0
		port=0
		# 收数据,然后打印
		def recvData():
		    while True:
		        recvInfo = udpSocket.recvfrom(1024)
		        # 第一个值是发送过来的ip:port,第二个值是发送过来的消息
		        print("{}<<:{}".format(recvInfo[1], recvInfo[0].decode()))
		
		def sendData():
		    while True:
		        sendInfo=input(">>")
		        udpSocket.sendto(sendInfo.encode(),(desIp,desPort))
		
		def main():
		    global udpSocket
		    global desIp
		    global desPort
		    udpSocket = socket(AF_INET, SOCK_DGRAM)
		
		    port=int(input("请输入本机的端口"))
		    desIp=input("请输入对方的ip")
		    desPort=int(input("请输入对方的端口"))
		    ip_port = ("127.0.0.1", port)
		    udpSocket.bind(ip_port)
		
		    tr=Thread(target=recvData)
		    ts=Thread(target=sendData)
		    tr.start()
		    ts.start()
		
		    # 等待线程结束
		    tr.join()
		    ts.join()
		
		if __name__ == '__main__':
		    main()

