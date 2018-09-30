##Python项目-Day49-Django
1. 安装Django

		pip install django

2. 创建项目

		django-admin startproject testdj

	启动项目:

		# python manage.py runserver 0.0.0.0:8000
	    # python manage.py runserver 8080
	    $ python manage.py runserver

	>启动django后，不能访问，报400错误。
	    原因：没有开启允许访问
	    处理：编辑HelloWorld目录下setting.py ，把其中的
	    ALLOWED_HOSTS=[]改成ALLOWED_HOSTS=['*'] ##* 表示任意地址。

3. 项目目录分析

	* 树结构


	![](https://i.imgur.com/pm1PKwv.jpg)

	* python_django_jobapp:项目的容器
	* manage.py: 一个实用的命令行工具，可让你以各种方式与该 Django 项目进行交互。
	*python_django_jobapp/__init__.py: 一个空文件，告诉 Python 该目录是一个 Python 包。
	*python_django_jobapp/settings.py: **该 Django 项目的设置/配置。
	* python_django_jobapp/urls.py: 该 Django 项目的 URL 声明; 一份由 Django 驱动的网站"目录"。

	* python_django_jobapp/wsgi.py: 一个 WSGI 兼容的 Web 服务器的入口，以便运行你的项目。
	* static:项目的css和js文件
		>注意:要使客户端能访问到static,需要公开static,在settings.py进行设置
			
			STATIC_URL = '/static/'
			STATICFILES_DIRS = [
			    os.path.join(BASE_DIR, "static"),
			]
	* templates:项目的html文件,需要在settings.py里面设置


			TEMPLATES = [
			    {
			        'BACKEND': 'django.template.backends.django.DjangoTemplates',
			        'DIRS': ['./templates'],
			        'APP_DIRS': True,
			        'OPTIONS': {
			            'context_processors': [
			                'django.template.context_processors.debug',
			                'django.template.context_processors.request',
			                'django.contrib.auth.context_processors.auth',
			                'django.contrib.messages.context_processors.messages',
			            ],
			        },
			    },
			]

	* python_django_jobapp/wsgi.py: 一个 WSGI 兼容的 Web 服务器的入口，以便运行你的项目。

4. 在项目中创建应用

		python manage.py startapp polls

	>项目和应用程序有什么区别？
	
	应用程序是一种Web应用程序，它可以执行某些操作，例如Weblog系统，公共记录数据库或简单的轮询应用程序。项目是特定网站的配置和应用程序的集合。项目可以包含多个应用程序。一个应用程序可以在多个项目中。

5. 创建路由

	在urls.py中:

		from django.urls import path
		
		        from . import views
		        
		        urlpatterns = [
		            path('', views.index, name='index'),
		        ]