##Python项目-Day48-MongoDB
1. windows安装MongoDB

	1. 下载mongodb

		[下载地址](https://www.mongodb.com/download-center#community)
		
		直接下一步
	2. 创建数据目录 

		例如 C:\data\db 或者 D:\data\db

		一定要放在 根目录下

	3. 启动服务器

			C:\mongodb\bin\mongod --dbpath c:\data\db

	4. 连接服务器

				C:\mongodb\bin\mongo.exe
	5. 创建配置文件

		创建一个配置文件。该文件必须设置 systemLog.path 参数，包括一些附加的配置选项更好。
		
		例如，创建一个配置文件位于 C:\mongodb\mongod.cfg，其中指定 systemLog.path 和 storage.dbPath。具体配置内容如下：
		
			systemLog:
			    destination: file
			    path: c:\data\log\mongod.log
			storage:
			    dbPath: c:\data\db
		安装 MongoDB服务
		通过执行mongod.exe，使用--install选项来安装服务，使用--config选项来指定之前创建的配置文件。
		
			C:\mongodb\bin\mongod.exe --config "C:\mongodb\mongod.cfg" --install

2. 与关系型数据库的区别

	SQL术语/概念|	MongoDB术语/概念|	解释/说明|
	 ---|---|---|---|
    database|	database|	数据库|
    table|	collection|	数据库表/集合|
    row|	document|	数据记录行/文档|
    column|	field|	数据字段/域|
    index|	index|	索引|
    table joins|	 	表连接|MongoDB不支持|
    primary key|	primary key|	主键,MongoDB自动将_id字段设置为主键|

3. 集合

	集合就是 MongoDB 文档组，类似于 RDBMS （关系数据库管理系统：Relational Database Management System)中的表格。
    
	集合存在于数据库中，集合没有固定的结构，这意味着你在对集合可以插入不同格式和类型的数据，但通常情况下我们插入集合的数据都会有一定的关联性。


4. 数据库命名规则

    * 不能是空字符串（"")。
    * 不得含有' '（空格)、.、$、/、\和\0 (空宇符)。
    * 应全部小写。
    * 不能与关键字重名。


3. 数据库查看

        show dbs			//查看所有数据库
        use boke			//进入boke数据库
        db      			//查看当前的数据库名称

        show tables 		//查看所有表格
		show collections    //同上
5. 为数据库添加用户名和密码

	**mongodb的用户名和密码是基于特定数据库的，而不是基于整个系统的。所有所有数据库db都需要设置密码**


	1. show dbs

		在mongodb新版本里并没有admin数据库，但是并不妨碍第2步操作。
	2. use admin 进入admin数据库
	3. 创建管理员账户

			db.createUser({ user: "root", pwd: "admin_root", roles: [{ role: "userAdminAnyDatabase", db: "admin" }] })
			
		mongodb中的用户是基于身份role的，该管理员账户的 role是 		userAdminAnyDatabase。 ‘userAdmin’代表用户管理身份，’AnyDatabase’ 代表可以		管理任何数据库。

	4. 角色
			
		  	Built-In Roles（内置角色）：
			    1. 数据库用户角色：read、readWrite;
			    2. 数据库管理角色：dbAdmin、dbOwner、userAdmin；
			    3. 集群管理角色：clusterAdmin、clusterManager、clusterMonitor、hostManager；
			    4. 备份恢复角色：backup、restore；
			    5. 所有数据库角色：readAnyDatabase、readWriteAnyDatabase、userAdminAnyDatabase、dbAdminAnyDatabase
			    6. 超级用户角色：root  
			    // 这里还有几个角色间接或直接提供了系统超级用户的访问（dbOwner 、userAdmin、userAdminAnyDatabase）
			    7. 内部角色：__system		

		具体角色:

			Read：允许用户读取指定数据库
			readWrite：允许用户读写指定数据库
			dbAdmin：允许用户在指定数据库中执行管理函数，如索引创建、删除，查看统计或访问system.profile
			userAdmin：允许用户向system.users集合写入，可以找指定数据库里创建、删除和管理用户
			clusterAdmin：只在admin数据库中可用，赋予用户所有分片和复制集相关函数的管理权限。
			readAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的读权限
			readWriteAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的读写权限
			userAdminAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的userAdmin权限
			dbAdminAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的dbAdmin权限。
			root：只在admin数据库中可用。超级账号，超级权限

	5. 刚建立了 userAdminAnyDatabase 角色，用来管理用户，可以通过这个角色来创建、删除用户。验证：需要开启auth参数。
	6. 用户命令:

		用户名密码登录:

			mongo -uroot -p123456 127.0.0.1:27017/admin

		创建一个数据库拥有者:

			db.createUser({ user: "root", pwd: "123456", roles: [{ role: "dbOwner", db: "test" }] })

		查找所有用户:

			db.system.users.find().pretty()

		删除用户:

			use test#先进入数据库
			db.dropUser("root1")#成功返回true,否则返回false

	7. **重新启动服务，加上登录验证**

			mongod --auth

##数据库操作
1. 新建数据库

		use book
		#注意必须向数据库插入数据,数据库才会存在

2. 查看所有数据库

		show dbs

3. 删除数据库

		use book
		db.dropDatabase()

4. 删除集合(表)

		use book
		db.表名.drop()
5. 插入文档

		use blog
		    db.articles.insert(
		        {title: 'css3 教程',
		        description: 'css3 是一个 脚本 语言',
		        by: 'lzhan',
		        url: 'http://www.lzhan.com',
		        tags: ['mongodb', 'database', 'NoSQL'],
		        likes: 3400
		    })

5. 更新数据

		db.articles.update({'title':'MongoDB 教程’},{$set:{‘by’:'lzhan'}})

		#默认只修改找到的第一条数据

		格式: db.表名.update({'查询key':'查询value'},{$set:{'修改key':'修改value'}})

		query : update的查询条件，类似sql update查询内where后面的。
		
		update : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
		
		upsert : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
		
		multi : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
		
		writeConcern :可选，抛出异常的级别。

		b. save() 方法通过传入的文档来替换已有文档。语法格式如下：
	
	    ```
	    db.collection.save(
	       <document>,
	       {
	         writeConcern: <document>
	       }
	    )

		#例如:

		db.col.save({
		    "_id" : ObjectId("56064f89ade2f21f36b03136"),
		    "title" : "MongoDB",
		    "description" : "MongoDB 是一个 Nosql 数据库",
		    "by" : "Runoob",
		    "url" : "http://www.runoob.com",
		    "tags" : [
		            "mongodb",
		            "NoSQL"
		    ],
		    "likes" : 110
		})

		db.articles.update({“条件”:’值’},{$inc:{“自增字段":步长}，{multi:true})


8. 删除文档

		db.col.remove({'title':'MongoDB 教程'})
	
		db.col.remove({})#删除所有数据

	如果你只想删除第一条找到的记录可以设置 justOne 为 1，如下所示：


		db.COLLECTION_NAME.remove(DELETION_CRITERIA,1)

9. 查询文档

		#查询所有
		db.articles.find().pretty()
		db.comments.find({'like':{$gte:5,$lte:100}}).pretty()

	* 条件操作符


		![](https://i.imgur.com/RYuhTT8.jpg)

			db.col.find({likes : {$gt : 100}})
			db.col.find({likes : {$lt :200, $gt : 100}})

	and语句:
		
		用,隔开就表示and

	or语句:

	
		db.col.find(
		        {
		            $or: [
		                {key1: value1}, {key2:value2}
		                 ]
		        }
		        ).pretty()

		#例如
		db.col.find({$or:[{"by":"菜鸟教程"},{"title": "MongoDB 教程"}]}).pretty()
