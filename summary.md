# ==Summary==

## 总览
1. gvim 基本使用: https://coolshell.cn/articles/5426.html
2. Learning Python 5th Edition revise0818: （PARTI，PARTII）
3. python web service gateway interfacehttps: http//www.python.org/dev/peps/pep-0333/: (wsgi)
4. gevent.wsgi: http://www.gevent.org/gevent.pywsgi.html
5. gevent: http://sdiehl.github.io/gevent-tutorial/ (gevent)
6. Falcon: http://falcon.readthedocs.io/en/0.3.0.1/user/index.html (falcon)

  * 搭建小型服务

7. pip: https://pip.pypa.io/en/stable/ (pip)
8. virtualenv: https://virtualenv.pypa.io/en/stable/ (virtualenv)

  * 在虚里环境登录

9. json schema: https://spacetelescope.github.io/understanding-json-schema/ (json schema)

10. jwt https://jwt.io/introduction/ (jwt)
  
  * 加上schemajwt 登录

11. mongodb: https://docs.mongodb.com/getting-started/shell/introduction/ (mongodb)
12. pymongodb https://api.mongodb.com/python/current/index.html (pymongo)
 
  * 从mongo获取数据　登录注册

13. pep-8: https://www.python.org/dev/peps/pep-0008/ (StyleGuide for Python Code)
14. unittest: https://docs.python.org/2/library/unittest.html (unit test)
15. mock: https://docs.python.org/3/library/unittest.mock.html (mock)

## 1. vim 
### Build Development Environment
* theme
* font color, font size
* virtual venv

### Basic Content	
* __Two Basic Modes__
		
    * Normal mode

		*In Normal mode the charactors that you type are commands.*
		
    * Insert mode

		*In Insert mode the  charactors are inserted as text.*

* __Basic Operator__
	* Inserting Text
		
    * i

		*switch to Insert mode, befor the cursor.*
		
    * a

		*switch to Insert mode, after the cursor.*
		
    * <ESC\>

		*switch to Numal mode*
	
	* Basic Moving
		* h ←
		* j ↓
		* k ↑
		* l  →
		
	* Deleting Charactors
		* x

		*delete a charactor.*
		
    * dd

		*delete a whole line.*
		
	* Undo and Redo
		* u

		*undoes the last edit*
		
    * CTRL-R

		*to reverse the preceding command*
		
	* Other Editing Commamd
		* i

		*insert*
		
    * a

		*append*
		
    * o

		*create a new, empty line below the cursor and put vim in Insert mode.*
		
    * O

		*open a line above the cursor.*
	
	* Getting out
		* ZZ

		*write the files and exit.*
		
    * q!

		*quit-and-throw-things-away.*
		
    * e!

		*reload the original version of the file.* 
		
	
* __Moving Around__	
	* Word Movement
		* (N)w 

		  *move the cusor forward the start of N's word.*
		
    * (N)b

		  *move backword to the start of the previous Ｎ'S word.*
		
    * (N)e

		  *move to the next end of N's word*
		
    * (N)ge

		  *move to the previous end of N's word*
		
    **Note:**
		> A word ends at a non-word character, such as a ".", "_" or  ")", use:
		W, B, E, gE
		
	* Start or End of Line Movement
		* $

		*move the cursor to the end of line.*
		
    * g_

		*move the cursor to the last non-blank charactor of line.*
		
    * 0

		*move the cursor to the vey first charactor of the line.*
		
    * ^

		*move the cursor to the first non-blank charactor of the line.*
		
	* Charactor Movement
		* (N)f(charactor)

		*search forward  in the line for the N's single charactor, and the cursor move to the charactor.*
		
    * (N)F(charactor)

		*search to the left.*
		
    * (N)t(charactor)

		*search forward  in the line for the N's single charactor, and the cursor move to a charactor before the charactor.*
		
    * (N)T(charactor)

		*search to the left.*
		
	* Parenthesis Matching

	*% can work for (), [], {} pairs.*
	
	* Line Movement
		* :N or NG

		*move to the start of N's line.*
		
    * gg

		*move to the start of first line.*
		
    * G

		*move to the start of last line.*
		
    * N%

		*move  to the line N%. 
		eg: 50% move to halfway line of the file*
	
	* Telling Where You Are
		* CTRL-G
		* :set number (display the line numer)
		* :set ruler
	
	* Scrolling Around
		* CTRL-U

		*scroll down half a screen of text.*
		* CTRL-D

		*move the viewing window down half a screen in the file.*
		* CTRL-E

		*scroll up one line*
		* CTRL-Y

		*scroll down one line*
		* CTRL-F
		* scroll forward by a whole screen.*
		* CTRL-B

		*scroll backward by whole screen.*
		* zz

		*Move the file so that the cursor is in the middle of the screen.*
		* zt

		*put the cursor line at  the top.*
		* zb

		*put the cursor line at the bottom.*
	
	* Simple Searches
		* /string

		*find the first string after the cursor.*
		* ?srting

		*find the first string before the cursor.*
		
	* Using Marks
		* ``

		*jump back*

		
## 2. PEP 333 WSGI
* 总述
  
  *指定web服务器与web应用程序或框架之间的接口标准,使得web应用在不同的服务器有较好的移植性*

* 应用程序或框架

  *`Application`对象是一个接受两个参数的可调用对象,这个对象可以是任何包含`__call__`方法的方法,函数,类或者类的实例*

  * environ
    
    *这个参数必须是字典对象,它必须是python内置的字典对象,app可以任意的修改这个字典对象,这个字典包含CGI风格的环境变量和WSGI请求变量,有时也要包含服务器的扩展变量*
  
    * CGI-style

      * REQUEST_METHOD

        *请求的方法,`GET, POST`*

      * SCRIPT_NAME

        *URL路径的起始部分*

      * PATH_INFO

        *URL路径除了起始部分后的剩余部分*

      * QUERY_STRING

        *查询字符串,在`?`之后*

      * CONTENT_TYPE

        *HTTP 请求`Content-Type`字段内容*

      * CONTENT_LENGHT

        *HTTP 请求`Content-Length`字段内容*

      * SERVER_NAME, SERVER_PORT

        *与上面的`SCRIPT_NAME`,`PATH_INFO`组成Url.如果`HTTP_HOST`存在,有限考虑`HTTP_HOST`*

      * SERVER_PROTOCOL

        *HTTP/1.1 或HTTP/1.0* 

      * HTTP_Variables
  
        *以HTTP_开头的变量,这些变量与HTTP请求头相对应*

    * WSGI请求变量
  
      * wsgi.version

        *(1, 0)代表WSGI version 1.0.*

      * wsgi.url_schema
    
        *http, https*

      * wsgi.input

        *一个从HTTP请求体中读取的类似文件类型的输入流*

      * wsgi.error

        *一个可以写入类似文件对象的输出流,用来记录程序或其它错误,可以是服务器的主错误日志,或者是sys.stderr*

      * wsgi.multithread

        *如果应用程序对象被统一进程的其它线程调用,设为true,否则设为false*

      * wsgi.multiprocess

        * 如果程序对象被另外的进程调用,值设为true,否则为false.*

      * wsgi.run_once

        *如果服务器或网关希望在包含应用程序进程的生命周期内只被调用一次,值设为true,否则设为false*

    * environ 还可能包含服务器定义变量,并且命名需要以服务器或网关唯一名称作为前缀*

  * start_response

    ``` python
      start_response(status, response_headers, exc_info=None)
    ```

    * status
    
      *HTTP string, '200 OK'*

    * response_headers
    
      * 它的参数是`header_name`,`header_value`元组的列表
      * `header_value`不能包含任何控制字符,例如回车与换行符
      * 服务器或网关负责确保正确的头部发送给客户端,如果应用程序没有设置,服务器或网关需要添加.
      * `Application`与`middleware`禁止使用`HTTP 1.1`中的`hop-by-hop`功能或首部,或者`http 1.0`中有等价的功能或首部. 
      
      *start_reponse 可调用对象不能直接发送相应首部,它们被存在服务器或网关,直到有实体body,或者迭代完成才被发送.这种延迟传送是为了确保缓存或者异步程序可以用错误信息替换掉原本输出.*

    * exc_info

      *如果提供次参数,必须是`sys.exc_info()元组`,当`response_headers`被一个错误的`handler`调用的时候,如果没有HTTP headers输出,则用exc_info替换掉储存的HTTP response headers,当错误产生允许应用程序做些调整.*

      *如果,`HTTP headers`已经被发送了,此时提供exc_info,就会抛出错误:*

      ``` python
        raise exc_info[0], exc_info[1], exc_info[2]
      ```
      *如果, `exc_info` 被提供了,而不带`exc_info`去调用`start_response`是一个致命错误.*

* 服务器或网关

  * 每当有来自HTTP客户端的请求的时候,服务器或网关就会调用应用程序
  * 服务器必须将可迭代对象内容传递给客户端
  * 服务端/网关 部分处理没有被添加的`environ`,或者做相关的替换
  * 异常处理,服务器日志记录

* 中间件

  * 功能
    * 通过重写`environ`,可根据请求的 url 传递到不同的应用程序
    * 允许多个应用程序在同一进程中运行
    * 通过网络传递请求和响应,实现负载均衡和远程处理
    * 对内容进行加工,比如附加 xsl 样式表



## 3. Gevent

* 总述

	*gevent 是一个基于[libev](http://software.schmorp.de/pkg/libev.html)的并发库*

* 核心概念

	* Greenlets

  	*作为C扩展包为python提供协程支持.*
	
	* Syschronous& Asyschronous
	
  	*并发的核心思想是将一个更大的任务分成一组子任务后被调度同时或者异步执行，而不是一次或者同步执行。*
	
  * 确定性
	
    *gevent是确定性的，给定greenlet和相同的一组输入相同的配置，他们总是产生相同的输出。*
	
  * Spawning Greenlets
	    
      *Gevent 提供了greenlet初始化的一些封装*
	
  * gevent.spawn()
	
  * 继承 gevent.Greenlet 类，重载`_run`方法，创建自定义Greenlet类，
	
  * Greenlet State
	  
 	  *Greenlet也会产生各种各样的错误，抛出异常时有可能会失败。Greenlet内部状态通常是与时间相关的参数。	Greenlet提供了一些标志，可以通过这些标志来监控线程的状态.*
    	
		* started() 
    	
      *whether the greenlet has been started.*
		
		* ready()
		  
      *whether the greenlet has been halted.*
		
		* successful()
    	
      *whether the Greenlet has halted and not thrown an exception.*
		
		* value
		  
      *arbitrary, the value returned by the Greenlet*

		* exception
		  
      *exception, uncaught exception instance thrown inside the greenlet*
	
  * Program Shutdown
    
    *当主程序接收到`SIGQUIT`信号时,Greenlets可能会超出预料时间hold程序执行,这就导致了僵尸进程。我们可以在主程序监听SIGQUIT事件，并在退出前调用gevent.shutdown.*
	
  * Timeouts
    
    *Timeouts是对代码块或Greenlet运行时的约束。*
    * 使用Timeout对象的实例设定timeout，用start()方法设定Timeout
    * 直接使用Timeout，接受timeout时间和timeout异常处理函数。

  * Monkeypatching
    * 'patch_all'
      * 'patch_socket'
      * 'patch_ssl'
      * 'patch_os'
      * 'patch_time'
      * 'patch_select'
      * 'patch_thread'
      * 'patch_subprocess'
      * 'patch_sys'

* 数据结构
  * Event
    * Event是Greenlet之间异步通信的一种形式。
      * 可以使用gevent.event.Event的wait()和set(),进行block通信 
      * AsyncResult是Gevent的扩展，可以允许随着唤醒呼叫发送一个值，也可以叫预设或延迟。
        * set()
        * get()
  * Queues
    * Queues是一个有序数据集，可以执行`put`和`get`操作，以便在Greenlet中安全的被操作。
      
      *如果一个Greenlet从一个Queue中抓取一个item，则这个item不会同时被另一个greenlet抓取执行。*
    * Queues也可以在put或get加block
    * 可以在Queue传入maxsize参数，设置queue的zise。

  * Group and Pools
    * Group
      
      *Group是一个被group管理和调度的运行时greenlets的集合，它也可以作为并行处理程序来镜像python的multiprocessing库*

      * Group提供了API去分配到分组的greenlet并且可以收集它们的结果。
        * getcurrent()
        * imap()
        * imap_unordered()
  
    * Pool
      
      *Pool是一个可以限制greenlet动态数量的结构，经常在网络和I/O绑定任务的时候使用。* 

  * Locks and Semaphores
    
    *信号量是一个低级同步原语，它允许greenlet协调和限制并发访问或执行。*
      
      * acquire()
      * release()
      * 可以在BoundSemaphore中传入信号量的size。
  
  * Thread Locals
    
    *Gevent还允许您指定greenlet上下文的本地数据。在内部，这是作为一个全局查找来实现的，该全局查找解决了由greenlet的getcurrent（）值键入的私有名称空间。*
    
    * gevent.local.local()
      
      *许多web框架使用gevent在gevent存储HTTP会话对象到gevent线程local。* 

  * Subprocess
    * 提供了子进程合适的等待 

## 4. gevent.pywsgi

* A pure python, gevent-friendly WSGI sever*
	* class WSGISever

	*大多数实际WSGI工作是由WSGIHandler处理的，可以使用WSGIHandler的子类来自定义服务器*

	* class WSGIHandler

	*处理来自套接字的HTTP请求, 创建WSGI环境, 并与WSGI应用程序进行交互，它是WSGIServer的默认值.*

	* class LoggingLogAdapter

	*用于记录日志，需要patch*

	* class Environ -- base dict

	*用于 WSGI 环境变量*

	* class SecureEnviron

	*默认不打印 Environ 的键和值*

	* class WSGISecureEnviron

	*为指定的WSGI变量设置一些默认的白名单*

## 5. Falcon
*Falcon是一个适合构建基于RESTful服务和应用程序的简、高新能的web框架。*
* 特点
	* 速度快
	* 专注于单一用例：HTTP api，不包括模块引擎，ORM等，可以自定义选择
	* Falcon避开使用magic，使得诊错时，可以掌握自主权

* Classes and Functions
	* API Class

		*Falcon的API是WSGI的app，他可以在任何符合WSGI标准的服务器来托管。*

		* class falcon.API

			*这个类是falcon应用程序的主要入口点*
			
			* parameters
				* media_type

					*默认是application/json*
				
				* middleware

				* request_type

				* response_type

				* router

			* method
				* req_options

					*一组与传入请求相关的行为选项*

				* \__call__(env, start_response) 

					*使得API的实例可以从WSGI服务器中可以调用*

				* add_error_handler(exception, handler=None)

					*为给定的异常错误类型注册handler*

				* add_route(uri_template, resource)

					*将URI路径与资源相关联*

				* add_sink(sink, prefix='/')

					*为API注册一个接收器方法，当没有与请求匹配的路由时，但请求的URI中的路径与接收器前缀匹配，则不管请求的HTTP方法如何，Falcon都会将控制权传递给关联的接收器*

				* set_error_serializer(serializer)

					*重写 HTTPError 实例的默认序列化程序。*

	* class falcon.RequestOptions

		*此类是请求选项的容器。*

* Req/Resp

	*请求和响应类的实例分别作为第二和第三个参数传递给响应方。*

	* Request

		*表示客户端的HTTP请求。*
	
	* Response

		*表示对HTTP请求的响应。*

* Cookie
	* Getting Cookies

		*cookie可以从HTTP请求的属性中得到。*

	* Setting Cookies

		*在响应中设置Cookie是通过set_cookie()完成的*

* Status Codes
	* 1xx Informational
		* HTTP_100 = '100 Continue'
		* HTTP_101 = '101 Switching Protocols'

	* 2xx Success
		* HTTP_200 = '200 OK'
		* HTTP_201 = '201 Created'
		* HTTP_202 = '202 Accepted'
		* HTTP_203 = '203 Non-Authoritative Information'
		* HTTP_204 = '204 No Content'
		* HTTP_205 = '205 Reset Content'
		* HTTP_206 = '206 Partial Content'
		* HTTP_226 = '226 IM Used'

	* 3xx Redirection
		* HTTP_300 = '300 Multiple Choices'
		* HTTP_301 = '301 Moved Permanently'
		* HTTP_302 = '302 Found'
		* HTTP_303 = '303 See Other'
		* HTTP_304 = '304 Not Modified'
		* HTTP_305 = '305 Use Proxy'
		* HTTP_307 = '307 Temporary Redirect'

	* 4xx Client Error
		* HTTP_400 = '400 Bad Request'
		* HTTP_401 = '401 Unauthorized'  # <-- Really means "unauthenticated"
		* HTTP_402 = '402 Payment Required'
		* HTTP_403 = '403 Forbidden'  # <-- Really means "unauthorized"
		* HTTP_404 = '404 Not Found'
		* HTTP_405 = '405 Method Not Allowed'
		* HTTP_406 = '406 Not Acceptable'
		* HTTP_407 = '407 Proxy Authentication Required'
		* HTTP_408 = '408 Request Time-out'
		* HTTP_409 = '409 Conflict'
		* HTTP_410 = '410 Gone'
		* HTTP_411 = '411 Length Required'
		* HTTP_412 = '412 Precondition Failed'
		* HTTP_413 = '413 Payload Too Large'
		* HTTP_414 = '414 URI Too Long'
		* HTTP_415 = '415 Unsupported Media Type'
		* HTTP_416 = '416 Range Not Satisfiable'
		* HTTP_417 = '417 Expectation Failed'
		* HTTP_418 = "418 I'm a teapot"
		* HTTP_426 = '426 Upgrade Required'

	* 5xx Server Error
		* HTTP_500 = '500 Internal Server Error'
		* HTTP_501 = '501 Not Implemented'
		* HTTP_502 = '502 Bad Gateway'
		* HTTP_503 = '503 Service Unavailable'
		* HTTP_504 = '504 Gateway Time-out'
		* HTTP_505 = '505 HTTP Version not supported'

* Error Handling

	*Falcon可以捕获Falcon的HTTPError，并自动转化为适当的HTTP响应*
	
	* Base Class

		*表示通常的HTTPerror*

	* Mixin 

		*表示没有回应表现的子类，从HTTPError继承时，结合Mixin，可以重写has_representation属性，使其返回False，它将不会有错误的body。*

* Hooks
	* falcon.before(action)

	* falcon.after(action)	

## JSON Schema

*JSON Schema是一个验证json数据解构的工具*
* Type-specific keywords
	* string
	* Numeric types
	* object
	* array
	* boolean
	* null

* Generic keywords
	* Metadata

		*SON 架构包括一些keywords, title, description和default, 它们不是严格用于验证, 而是用于描述架构的各个部分。*
	
	* Enumerated values

		*enum 关键字用于将值限制列出一组固定的值。它必须是一个至少有一个元素的数组, 其中每个元素都是唯一的。*
		``` json
		{
  			"type": "string",
 			 "enum": ["red", "amber", "green"]
		}
	  ```

* Combining schemas

*JSON Schema包括几个将架构组合在一起的关键字。*

	* allOf

		*必须对所有的 subschemas 有效.*
	* anyOf

		*必须对任何 subschemas 有效*
	* oneOf

		*必须是有效的反对恰恰是 subschemas*

*  $schema 关键字
	* http://json-schema.org/schema #

		*针对规范的当前版本编写的 JSON 架构。*

	* http://json-schema.org/hyper-schema #

		*针对规范的当前版本编写的 JSON 架构 hyperschema。*

	* http://json-schema.org/draft-04/schema #

		*针对此版本编写的 JSON 架构。*

	* http://json-schema.org/draft-04/hyper-schema #

		*针对此版本编写的 JSON 架构 hyperschema。*

	* http://json-schema.org/draft-03/schema #

		*针对 json 架构编写的 json 架构, 草稿 v3*

	* http://json-schema.org/draft-03/hyper-schema #

		*针对 json 架构编写的 json 架构 hyperschema, 草稿 v3*

* 正则表达式

	*正则表达式语法来自JavaScript（ECMA 262）*

* 重用

	*可以使用`ref`来指定，`#`表示当前文件*

* id 属性

	*id 属性有两个目的:*
	* 它声明了架构的唯一标识符。
	* 它声明一个供$ref url 的解析的base url。

## JWT
*Json web token (JWT), 是为了在网络应用环境间传递声明而执行的一种基于JSON的开放标准（(RFC 7519).该token被设计为紧凑且安全的，特别适用于分布式站点的单点登录（SSO）场景。JWT的声明一般被用来在身份提供者和服务提供者间传递被认证的用户身份信息，以便于从资源服务器获取资源，也可以增加一些额外的其它业务逻辑所必须的声明信息*

* 结构
	* Header
		* alg
		* typ
	``` json
	{
		"alg": "HS256",
		"typ": "JWT"
	}
	```
	
	* Payload
		* Registered claims
			* iss: jwt签发者
			* sub: jwt所面向的用户
			* aud: 接收jwt的一方
			* exp: jwt的过期时间，这个过期时间必须要大于签发时间
			* nbf: 定义在什么时间之前，该jwt都是不可用的.
			* iat: jwt的签发时间
			* jti: jwt的唯一身份标识，主要用来作为一次性token,从而回避重放攻击。

			*重放攻击(Replay Attacks)又称重播攻击、回放攻击，是指攻击者发送一个目的主机已接收过的包，来达到欺骗系统的目的，主要用于身份认证过程，破坏认证的正确性。*

		* Public claims

			*公共的声明可以添加任何的信息，一般添加用户的相关信息或其他业务需要的必要信息.但不建议添加敏感信息，因为该部分在客户端可解密.*

		* Private claims

			*私有声明是提供者和消费者所共同定义的声明，一般不建议存放敏感信息，因为base64是对称解密的，意味着该部分信息可以归类为明文信息。*

	* Signature
		* jwt的第三部分是一个签证信息，这个签证信息由三部分组成：
			* header (base64后的)
			* payload (base64后的)
			* secret
		
		*这个部分需要base64加密后的header和base64加密后的payload使用.连接组成的字符串，然后通过header中声明的加密方式进行加盐secret组合加密，然后就构成了jwt的第三部分。*


## mongoDB
* Introduction

  *MongoDB 是一个开源的高性能,高可用性,可扩展的 `document`文档库.*

  * Documents
    
    *MongoDB 的一条记录,它是由字段和值组成的数据结构,它和JSON对象很类似,字段的值可以包含其它的 `document`, `arrays`, `document`数组* 

  * Collections

    *MongoDB将`Documents`储存在`Collections`中,必须有一个唯一的`_id`字段作为主键.*

* Import data

  * mongoimport
    * --db

      *指定要导入到的数据库名称*

    * --collection

      *指定要导入的collection名称*

    * --drop  

      *如果数据库中的`collection`已经存在,则删掉.*

    * --file

      *后接要导入的文件的路径*

* Insert

  * db.collection.insert()

    *插入一个或多个`document`, 插入一个时返回`WriteResult`对象,插入多个时返回`BulkWriteResult`,最好使用下面两种方法.*

  * db.collection.insertOne()
    
    *插入一个`document`,返回一个`document`,包含`acknowledged`和`insertedId`.*

  * db.collection.insertMany()

    *插入多个`document`,返回一个`document`,包含`acknowledged`和`insertedIds`,`insertedIds`是insertedId的数组*


* Find and Query

  * switch database

    ``` shell
       use {db_name}
    ```

  * 查询所有的`document`
    
   
   ``` shell
        db.collection.find()
    ```

  * 指定查询条件
    
    ``` shell
      { <field1>: <value1>, <field2>: <value2>, ... }
    ```

  * 嵌入型,数组和顶级`document`的查询

    * 顶级查询可以直接使用字段和值
  
    * 嵌入型和数组可以使用`.`符号表示查询的字段

  * 指定条件下操作
  
    ``` shell
        { <field1>: { <operator1>: <value1> } }
    ```
    * comparison
      * `$eq`  =
      * `$gt`  >
      * `$gte` >=
      * `$lt`  <
      * `$lte` <=
      * `$ne`  ≠
      * `$in   
      * `$nin` 

   * Logical
     * `$and`
     * `$not`
     * `nor`
     * `or`

   * Element
     * `$exits`
     * `type`

  * 查询结果排序
  
    * db.collection.find(...).sort({field1:1(-1), ...})
      
      *当值为1时升序排列,当值为-1时降序排列*

      
* Update
  
  * update

    *使用更新相关的操作更新指定的Document内容,默认更新一个匹配的`document`,如果想更新多个匹配的内容,可以使用`multi`选项设置*

    ``` shell
      db.restaurants.update(
      { "address.zipcode": "10016", cuisine: "Other" },
      {
        $set: { cuisine: "Category To Be Determined" },
        $currentDate: { "lastModified": true }
      },
      { multi: true}
    )
    ```
      
  * replace
    
    * 如果update参数中没有更新相关的操作符号,就默认为替换操作,只有`_id`不变

    *最好使用`updateOne`,`updateMany`和`replaceOne`等代替,避免歧义或误用

  
* Remove
  
  ``` shell
      db.collection.remove({field1:value1,...})
  ```


  * remove操作会删除掉所有匹配到的`document`

  * justOne

    *使用此选项设置只删掉一个匹配的`document`*
  
  * 如果remove的参数为一个空的`document`,则会匹配collection中所有的`document`,这会删掉collection中所有的`document`

  * Drop collection
    ``` shell
        db.collection.drop()
    ```

* 数据聚合
  
  * 使用collection方法: aggregate()
  
  ``` shell
      db.collection.aggregate({<stage1>,<stage2>,...})
  ```
  
  * $group
    
    *`$group`需要指定一个字段作为`_id`,后面的`stage`可以使用`accumulators`,或其他`stage`*
  
  * Filter
  
    *在使用`$group`时可以使用`$match`来对匹配的指定查询进行聚合*

  
* 索引
  * 创建 Single-Field 索引

    ``` shell
      db.collection.createIndex({field:1})
    ```

    *Field的值为1时升序,为-1降序*

  * 创建 compound 索引

    ``` shell
      db.collection.createIndex({ <field1>: <type1>, <field2>:<type2>, ...})
    ```

    *可以对不同字段创建不同的顺序,主要是根据业务需求,另外字段如果是嵌入型的可以使用`.`符号*


## pymongo -- mongodb diver for python

* 使用之前需要开启`mongod`的服务

* MongoClient

  *使用`MongoClient`去运行一个`mongod`的一个实例,下面三种默认主机和端口下是等效的,但是后面两种方法可以自定义主机和端口*

  * client = MongoClient()

  * client = MongoClient('localhost', 27017)

  * client = MongoClient('mongodb://localhost:27017/')

* 链接数据库

  *可以使用下面两种风格, 第一种支持默认`word`格式,第二种弱`word`格式*

  * collection = db.test_collection

  * collection = db['test-collection']

* Document

  *在`mongodb`中使用了`JSON-style`的`documents`,在`pymongo`中,使用字典类型表示`document`*

* 插入一个Document

  * 使用 `insert_one()` 方法

    *返回变亮有一个`inserted_id`属性代表插入的`document`的`ObjectId`.*

* 查询一个Document

  * 使用 `find_one()` 方法
  
* 通过`ObjectId`查询 

  *不能直接使用ObjectId的字符串进行查询,需要借用`bson`库提供的`ObjectId`进行转换*

* 批量插入(Bulk Inserts)
  
  *使用 `insert_many()` 方法

    *返回一个插入documents的`ObjectId`的数组*

* 查询多个Document

  * 使用 `find({filed1:value1,...})` 方法可以返回一个游标的实例,通过这个实例可以迭代出所有匹配的`document`
  
  * find()的参数为空时,将匹配`collection`中所有的`document`.
  
* 计数

  *`collection`或一个查询,都包含一个`count()`方法,可以去查询`document`的数量.*

* 查询结果排序

  * `query` 包含一个 `sort()` 方法
    * 通过一个字段排序
    
    ``` python
        sort('field', pymongo.ASCENDING)
    ```

    * 通过多个字段排序
    
    ``` python
      sort([
          ('field1', pymongo.ASCENDING),
          ('field2', pymongo.DESCENDING)
          ])
    ```

* 索引

  * 使用 `create_index()`方法

    ``` python
      db.collectioncreate_index([('user_id', pymongo.ASCENDING)],unique=True)
    ```

    *unique设置唯一索引,当新插入document包含已经存在的索引时,会报出`DuplicateKeyError`*

## unittest

* 概要
  
  * test fixture
  
    *代表在测试之前的准备工作,包括所有关联的清理工作,比如创建临时或代理数据库,目录或开始一个服务器的进程.*
  
  * test case
  
    *测试用例最小的测试的单位,它对特定输入集合的特定相应进行检查* 
  
  * test suit
  
    *一组测试用例或测试suit的集合,用来聚合测试,然后一起进行测试.*
  
  * test runner
  
    *它是一个协调测试的执行,并把结果提供给user的组件.*
  
* Command-line
  
  *当脚本中,没有定义 `test runner` 时,可以使用 `Command-line`来运行测试用例*
  
  ``` shell
    python -m unittest test_basic
  ```

* Test Discovery
  
  * 在`unittest`后面加上`discover`可以实现简单的test的搜索.
    * -v

      *详细信息*

    * -s

      *搜索开始的目录* 

    * -p

      *设置要匹配的测试*

    * -t
    
      *项目的顶层目录*

    
* 测试程序结构

  * 可以使用重写 `setUp` 方法,用于测试用例执行前的初始化工作

  * 重写 `tearDown` 方法,用于测试用例执行完的善后工作,即使测试过程中抛出了异常,它仍然会执行.

  * unittest.TestCase : 所有测试用例继承的基本类

  * unittest.main() 
    
    *使用`Testloader`类搜索所有包含在该模块中的一`test`开头的测试,并执行*

  * unittest.TestSuite
    
    *用来创建测试套件*

  * unittest.TextTestRunner()

    *`unittest` 框架的 `TextTestRunner` 类的run方法运行suite组装的测试用例*

  * unittest.defaultTestLoader()

    *通过该类下面的 `discover` 方法可以根据测试目录匹配查找测试文件*


* 装饰器

  * @unittest.skip(reason) 无条件跳过
  * @unittest.skipIf(reason) 条件真跳过
  * @unittest.skipUnless(reason) 条件假跳过
  * @unittest.exceptedFailure 将一个测试标记为`fail`, 如果`fail`,则不会`failure`

* 断言

  * assertEqual(a, b, [msg])
    
    *a == b*

  * assertNotEqual(a, b, [msg])
  
    *a != b*	 
  
  * assertTrue(x, [msg])	
  
    *bool(x) is True*
  
  * assertFalse(x, [msg])
  
    *bool(x) is False*	
  
  * assertIs(a, b, [msg])
  
    *a is b*
  
  * assertIsNot(a, b, [msg])
  
    *a is not b*
  
  * assertIsNone(x, [msg])
  
    *x is None*
  
  * assertIsNotNone(x, [msg])
  
    *x is not None*
  
  * assertIn(a, b, [msg])
  
    *a in b*
  
  * assertNotIn(a, b, [msg])
  
    *a not in b*
  
  * assertIsInstance(a, b, [msg])
  
    *isinstance(a, b), a is the instance of b*
  
  * assertNotIsInstance(a, b, [msg])
  
    *not isinstance(a, b)*


## unittest.mock mock object library

在测试过程中可以使用`mock`库来用模拟的对象替换掉被测试的部分,这些部分可能很难获取或者很难被构造出来.

- Mock Class

  ``` python
    class unittest.mock.Mock(spec=None, side_effect=None, return_value=DEFAULT, wraps=None, name=None, spec_set=None, unsafe=False, **kwargs) 
  ```

  * parameter 
    * spec 
      
      *mock对象的规范,它可以是一组字符串列表或者是一个已经存在的对象,如果传入一个对象,则通过调用`dir`来形成字符串列表,当访问不在列表中的属性时,就会抛出`AttributeError.`*

    * spec_set

      *作为spec参数的严格变体,如果设置或者获取的mock属性,不在传入的对象属性中,则抛出`AttributeError`*

    * side_effect

      * 当Mock被调用时,这个参数指定的函数也会被调用,被用来抛出异常或动态修改返回值.
      * 它的参数与mock参数相同,并且除非它的返回值是`default`,否则使用这个函数的返回值作为返回值.
        * 或者说`side_effect`可以是`exception`类或实例,这种情况下,调用mock将会抛出这个异常.
      * 如果`side_effect`是一个可迭代的,每次调用都会返回这个可迭代对象的下一个值.
      * 设置为`None`,可以清除`side_effect`

    * return_value

      *当调用mock时,这个值会被返回.一般情况下,这是一个新的Mock,即被创建或第一次被访问* 

    * unsafe
    
      *默认情况下,任何以`assert`或`assret`开头的属性,都会抛出`AttributeError`异常* 

    * wraps

      * 用于mock对象的封装
      * 如果`wraps`不是`None`,调用Mock会将这个调用传递向封装mock对象wraps对象.
      * mock上的属性访问会返回一个包含`wraps`对象属性的Mock对象

    * name

      * 在mock一些准备工作中被使用
      * 可以用于调试
      * 这个名字可以传递给子mock

    
  * method

    * assert_called(*args, **kwargs)
    
      *断言这个mock至少被调用了一次*

    * assert_called_once(*arg, **kwargs) 

      *断言这个mock被只调用了一次*

    * assert_called_with(*args, **kwargs)

      *这是一个方便的方法去断言mock是被一种指定的方式调用*

    * assert_called_once_with(*args, **kwargs)

      *断言这个mock被指定的方法调用了一次*

    * assert_any_call(*args, **kwargs)  

      *断言这个mock曾经被用指定方式调用过,与`assert_called_with`和`assert_called_once_with`不同的是只要mock只要曾经被调用过,它就pass,而后两个则需要最近一次被调用*

    * assert_has_calls(calls, any_order=False)
    
      *断言这个mock被指定的呼叫调用,calls是一个 `mock_calls`列表*
      
      * any_order 默认为false
        
        *这个calls必须是有序的,可以在指定的calls之前或之后加额外的calls*

      * any_order 为 true

        *这个可以是无序的,但是必须使用`mock_calls`中的呼叫*

    * assert_not_called()

      *断言这个mock从来没有被调用过*

    * reset_mock(*, return_value=False, side_effect=False)

      *这个方法会重置这个mock的所有调用属性*

    * mock_add_spec(spec, spec_set=False)

      *向mock增加规范列表或对象,如果`spec_set`为True,只有spec的属性可以设置*

    * configure_mock(**kwargs)
  
      *通过关键字参数,设置mock属性*

    * called

      *判断mock是否被调用过,返回布尔值*

    * call_count

      *mock 被调用的此时*

    * return_value

      *设置这个mock返回值*

    * side_effect
      
      * 配置 `side_effect`*

    * call_args

      * 如果没有被调用过,值为 None
      * 否则值为最后一次被调用的参数

    * call_args_list

      *被调用参数列表*

    * method_calls
    
      *调用的方法列表*

    * mock_calls
  
      *记录调用的mock对象,方法, magic方法, return_value mocks*

    * __class__

      *对象的属性*


- patcher

  *`patch`用来对修饰范围之内的对象进行修补*

   
  * patch

     *`patch`可以作为函数装饰器,类装饰器和一个上下文管理器*

    ``` python
      unittest.mock.patch(target, new=DEFAULT, spec=None, create=False, spec_set=None, autospec=None, new_callable=None, **kwargs)
    ```

    * target 
      * `target`必须是`package.module.ClassName`形式的字符串
      * 导入对象,并且被新的对象替换
      * 这个对象在装饰器执行的时候会被导入,而不是在装饰的时候
    
    * spec spec_set
  
      * spec = True spec_set=True
  
        *`patch`会被作为`spec/spec_set`对象,传递给mock对象*
  
    * new_callable
  
      *指定新的不同的类或可调用对象*
  
    * autospec
    
      *autospec是一个更强大的规范形式。如果你设置autospec = True，那么mock将被替换的对象的规范创建。mock的所有属性也将具有被替换的对象的相应属性的规格。被模拟的方法和函数将检查它们的参数，如果调用了错误的签名，将引发TypeError。*
  

  * patch.dict
  
    *修补一个字典或者像对象的字典,并且在测试完之后恢复它.*

    ``` python
      patch.dict(in_dict, values=(), clear=False, **kwargs)
    ```

    * in_dict
      * in_dict 可以是字典或者像容器一样的映射,如果是映射它至少要支持获取,设置,删除以及迭代键
      * in_dict 也可以是字典的名称,可以通过导入来获取

    * values
      * 字典的值
      * 键与值的迭代

    * clear

      *如果设为`true`,那么在在设置新的值之前,字典会被清除*

  * patch.multiple

    *执行多个修补程序*
    
    ``` python
      patch.multiple(target, spec=None, create=False, spec_set=None, autospec=None, new_callable=None, **kwargs)
    ```
    
  * patch methods: start and stop
    
    *所有的patcher都有start和stop方法*

    * 使用patcher的start方法会返回创建的mock
    * 经常在unittest的 `setUp` 中使用
    * stopall 方法会停止所有使用start的patcher

  * patch builtins
    
    *可以对内置模块进行补丁*

  * TEST_PREFIX

    * patch 匹配的字首

  * Nesting Patch Decorators

    *可以使用多个堆叠的修补修饰器,进行多次修补,注意参数顺序是由里向外*

  * Where to patch
  
    *主要是从所需的地方引入*

- MagicMock and magic method support

  * Mocking Magic Methods
  
    *mock支持模拟python协议方法,称为`MagicMock`*

  * Magic Mock

    *可以无需自定义,使用MagicMock*

    ``` python
      class unittest.mock.MagicMock(*args, **kw)
    ```

    * python protocol 默认值

      * __lt__: NotImplemented
      * __gt__: NotImplemented
      * __le__: NotImplemented
      * __ge__: NotImplemented
      * __int__: 1
      * __contains__: False
      * __len__: 0
      * __iter__: iter([])
      * __exit__: False
      * __complex__: 1j
      * __float__: 1.0
      * __bool__: True
      * __index__: 1
      * __hash__: default hash for the mock
      * __str__: default str for the mock
      * __sizeof__: default sizeof for the mock
      

    
