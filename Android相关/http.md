### HTTP
---
### 1.HTTP
HTTP 全称是` HyperText Transfer Protocal `，即：超文本传输协议，HTTP 是应用层协议，当浏览网页的时候，浏览器和 web 服务器之间就会通过 HTTP 在 Internet 上进行数据的发送和接收。HTTP 是一个基于请求/响应模式的、无状态的协议。即我们通常所说的 Request/Response
+ 支持客户端/服务器模式
+ 简单快速：客户向服务器请求服务时，只需传送请求**方法和路径**。由于 HTTP 协议简单，使得 HTTP 服务器的程序规模小，因而通信速度很快
+ 灵活：HTTP 允许传输任意类型的数据对象。正在传输的类型由 `Content-Type`加以标记
+ 无连接：无连接的含义是限制每次链接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开链接，采用这种方式可以节省传输时间
+ 无状态：HTTP 协议是无状态协议。无状态是指协议对于事物处理没有记忆能力。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能会导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就比较快

### 2.URL
URL（Uniform Resource Locator）是统一资源定位符的简称
通用的格式：**scheme://host[:port#]/path/…/[?query-string][#anchor]**
| 名称	         |                           功能| 
| :--------------| :-----------------------------| 
| scheme         | 访问服务器以获取资源时要使用哪种协议，比如，http，https 和 FTP 等 |  
| host           | HTTP 服务器的 IP 地址或域名|  
| port#          | HTTP 服务器的默认端口是 80，这种情况下端口号可以省略，如果使用了别的端口，必须指明，例如www.cnblogs.com：8080|  
| path           |	访问资源的路径 |  
| query-string   | 发给 http 服务器的数据 |  
| anchor         | 锚 |  
>www.mywebsite.com/js/test/tes…
### 3. HTTP请求
#### 请求行
请求行（Request line）分为三个部分：**请求方法**、**请求地址**和**协议版本**
#### 请求方法
HTTP/1.1 协议中共定义了八种方法（也叫“动作”）来以不同的方式操作指定的资源
| 名称	         |                           功能| 
| :--------------| :-----------------------------| 
| GET            | 向指定的资源发出“显示”请求，使用 GET 方法应该只用在读取数据上，而不应该用于产生“副作用”的操作中 |  
| POST           | 指定资源提交数据，请求服务器进行处理（例如提交表单或者上传文件）。数据被包含在请求文本中。这个请求可能会创建新的资源或者修改现有资源，或两者皆有。|  
|HEAD          | 与 GET 方法一样，都是向服务器发出指定资源的请求，只不过服务器将不传回资源的本文部分，它的好处在于，使用这个方法可以在不必传输全部内容的情况下，就可以获取其中关于该资源的信息（原信息或称元数据）|  
| OPTIONS        |	使服务器传回该资源所支持的所有HTTP请求方法。用*来代替资源名称，向 Web 服务器发送 OPTIONS 请求，可以测试服务器功能是否正常运作 |  

#### 请求头
请求头可用于传递一些附加信息，格式为：键:  值
>注意冒号后面有一个空格

**Request Headers**
```java
Accept：*/*
Origin: http://www.test.com
User-Agent: Mozilla/5.0(Windows NT 10.0; WOW64) AppleWebkit/537.36(KHTML, likeGecko) Chrome/56.0.2924.87 Safari/537.36
x-writer-version: 25
Content-Type: multipart/form-data; boundary=----
SEKFOENJFNEIFHF
```
请求和响应常见通用的 Header

| 名称	            |作用| 
| :-----------------| :-----------------------------| 
| Content-Type	 | 请求体/响应体的类型，如：text/plain、application/json |  
| Accept         | 说明接收的类型，可以多值，用","(英文逗号)分开|  
| Content-length  | 请求体/响应体的长度，单位字节|  
| Content-Encoding|	请求体/响应体的编码格式，如 gzip、deflate |  
| Accept-Encoding | 告知对方我方接受的 Content-Encoding |  
|ETag	          |给当前资源的标识，和Last-Modified、If-None-Match、If-Modified-Since配合，用于缓存控制|
| Cache-Control	  | 取值一般为no-cache、max-age=xx，xx为整数，表示资源缓存有效期（秒）| 
| User-Agent	  | 用户标识，如：OS 和浏览器的类型和版本| 
| If-Modified-Since	| 值为上一次服务器返回的Last-Modified值，用于确定某个资源是否被更改过，没有更改过就从缓存中读取| 
| Cookie  | 已有的Cookie| 
| Host	  | 请求的主机和端口号| 
#### 请求体
请求体（又叫请求正文）是 post 请求方式中的请求参数，以 key = value 形式进行存储，多个请求参数之间用&连接，如果请求当中请求体，那么在请求头当中的 Content-Length 属性记录的就是该请求体的长度
HTTP 请求的请求体有三种
1. 移动开发者常见的，请求体是任意类型的，服务器不会解析请求体，请求体的处理需要自己解析，如 *POST JSON* 的时候就是这类。
2. 第二种和第三种都有固定的格式，是服务器端开发人员最先了解的两种。这里的格式要求就是 URL 中 `Query String` 的格式要求：多个键值对之间用`&`连接，键与值之间用`=`连接，且只能用 ASCII 字符，非 ASCII 字符需使用`UrlEncode`编码。
3. 第三种请求体被分成多个部分，文件上传 时会被使用，这种格式最先是被用于邮件传输中，每个字段/文件都被 boundary（Content-Type中指定的）分成单独的段，每段以`--`加 boundary 开头，然后是该段的描述头，描述头之后空一行接内容，请求结束的标识为 boundary 后面加`--`。
```java
// 2
 key1=value1&key2=value2
```
 >区分是否被当成文件的关键是` Content-Disposition `是否包含 `filename`，因为文件有不同的类型，所以还要使用` Content-Type `指示文件的类型，如果不知道是什么类型取值可以为 `application/octet-stream` 表示文件是一个二进制的文件，如果不是文件则 `Content-Type` 可以省略。
 
### 4. HTTP响应
 HTTP 响应的格式上除状态行与请求报文的请求行不一样之外，其他的就格式而言是一样的，但排除状态行和请求行的区别，从 Header 上还是可以区分出 HTTP 请求和 HTTP 响应的区别的，怎么区别就要看前面的 Header。
 
#### 响应状态行
 + 状态码
 + 响应头 响应头同样可用于传递一些附加信息
 +  响应体 响应体也就是网页的正文内容
 
 ** Response Headers**
  ```java
  status: 200
  
  ```