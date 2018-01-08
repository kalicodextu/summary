# ==Summary==

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
* 

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
		  
      *exception, uncaught exception instance thrown inside the greenlet
	
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



