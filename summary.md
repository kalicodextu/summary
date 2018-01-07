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

## 4。gevent.pywsgi

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


## pymongo
	