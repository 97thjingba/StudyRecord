### HTTP 协议主要特点

-   简单快速：当客户端向服务器端发送请求时，只是简单的填写请求路径和请求方法即可，然后就可以通过浏览器或其他方式将该请求发送就行了
-   灵活：HTTP 协议允许客户端和服务器端传输任意类型任意格式的数据对象
-   无连接：无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接，采用这种方式可以节省传输时间。(当今多数服务器支持Keep-Alive功能，使用服务器支持长连接，解决无连接的问题)
-   无状态：无状态是指协议对于事务处理没有记忆能力，服务器不知道客户端是什么状态。即客户端发送HTTP请求后，服务器根据请求，会给我们发送数据，发送完后，不会记录信息。(使用 cookie 机制可以保持 session，解决无状态的问题)

## HTTP 请求报文

HTTP 请求报文由**请求行**、**请求头**、**空行** 和 **请求体(请求数据)** 4 个部分组成，如下图所示：

![](https://lc-gold-cdn.xitu.io/871c141568586a6197ff.png?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

### 请求报文示例

```
GET / HTTP/1.1
Host: www.baidu.com
Connection: keep-alive
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/57.0.2987.110 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate, sdch, br
Accept-Language: zh-CN,zh;q=0.8,en;q=0.6,id;q=0.4
Cookie: PSTM=1490844191; BIDUPSID=2145FF54639208435F60E1E165379255; BAIDUID=CFA344942EE2E0EE081D8B13B5C847F9:FG=1;复制代码
```

### 请求行

请求行由请求方法、URL 和 HTTP 协议版本组成，它们之间用空格分开。

```
GET / HTTP/1.1复制代码
```

### 请求头

请求头由 `key-value` 对组成，每行一对，key (键) 和 value (值)用英文冒号 `:` 分隔。请求头通知服务器有关于客户端请求的信息，典型的请求头有：

-   User-Agent：用户代理信息 - Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/537.36 ...
-   Accept：客户端可识别的内容类型列表 - text/html,application/xhtml+xml,application/xml
-   Accept-Language：客户端可接受的自然语言 - zh-CN,zh;q=0.8,en;q=0.6,id;q=0.4
-   Accept-Encoding：客户端可接受的编码压缩格式 - gzip, deflate, sdch, br
-   Host：请求的主机名，允许多个域名同处一个IP地址，即虚拟主机 - `www.baidu.com`
-   connection：连接方式
    -   close：告诉WEB服务器或代理服务器，在完成本次请求的响应后，断开连接
    -   keep-alive：告诉WEB服务器或代理服务器。在完成本次请求的响应后，保持连接，以等待后续请求
-   Cookie：存储于客户端扩展字段，向同一域名的服务端发送属于该域的cookie - PSTM=1490844191; BIDUPSID=2145FF54639208435F60E1E165379255;

### 空行

最后一个请求头之后是一个空行，发送回车符和换行符，通知服务器以下不再有请求头。

### 请求体

请求数据不在 GET 方法中使用，而是在 POST 方法中使用。与请求数据相关的最常使用的请求头是 Content-Type和 Content-Length。

## HTTP 响应报文

HTTP响应报文由**状态行、响应头、空行和响应体**4 个部分组成，如下图所示：

![](https://lc-gold-cdn.xitu.io/8704822e2e641277efac.png?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

### 响应报文示例

```
HTTP/1.1 200 OK
Server: bfe/1.0.8.18
Date: Thu, 30 Mar 2017 12:28:00 GMT
Content-Type: text/html; charset=utf-8
Connection: keep-alive
Cache-Control: private
Expires: Thu, 30 Mar 2017 12:27:43 GMT
Set-Cookie: BDSVRTM=0; path=/复制代码
```

### 状态行

状态行格式： HTTP-Version Status-Code Reason-Phrase CRLF

-   HTTP-Version - HTTP 协议版本
-   Status-Code - 状态码
-   Reason-Phrase - 状态码描述
-   CRLF - 回车/换行符

### 响应头

响应头由 `key-value` 对组成，每行一对，key (键) 和 value (值)用英文冒号 `:` 分隔。响应头域允许服务器传递不能放在状态行的附加信息，这些域主要描述服务器的信息和Request-URI进一步的信息，典型的响应头有：

-   Server：包含处理请求的原始服务器的软件信息
-   Date：服务器日期
-   Content-Type：返回的资源类型 (MIME)
-   Connection：连接方式
    -   close：连接已经关闭
    -   keep-alive：连接已保持，在等待本次连接的后续请求
-   Cache-Control：缓存控制
-   Expires：设置过期时间
-   Set-Cookie：设置 Cookie 信息

### 空行

最后一个响应头之后是一个空行，发送回车符和换行符，通知浏览器以下不再有响应头。

### 响应体

服务器返回给浏览器的响应信息，下面是百度首页的响应体片段：

```
<!DOCTYPE html>
<!--STATUS OK-->
<html>
<head>
    <meta http-equiv="content-type" content="text/html;charset=utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=Edge">
    <link rel="icon" sizes="any" mask href="//www.baidu.com/img/baidu.svg">
    <title>百度一下，你就知道</title>
</head>
<body>
  ...
</body>
</html>复制代码
```

## HTTP Methods

HTTP 协议的请求方法有：GET、POST、HEAD、PUT、DELETE、OPTIONS、TRACE、CONNECT、PATCH、HEAD

HTTP 常用的请求方法：

-   GET - 获取资源，使用 URL 方式传递参数，大小为 2KB
    -   `http://www.example.com/users` - 获取所有用户
-   POST - 传输资源，HTTP Body, 大小默认8M
    -   `http://www.example.com/users/a-unique-id` - 新增用户
-   PUT - 资源更新
    -   `http://www.example.com/users/a-unique-id` - 更新用户
-   DELETE - 删除资源
    -   `http://www.example.com/users/a-unique-id` - 删除用户

## HTTP Status Code

状态代码由三位数字组成，第一个数字定义了响应的类别，且有五种可能取值：

-   1xx：指示信息 – 表示请求已接收，继续处理
-   2xx：成功 – 表示请求已被成功接收
-   3xx：重定向 – 要完成请求必须进行更进一步的操作
-   4xx：客户端错误 – 请求有语法错误或请求无法实现
-   5xx：服务器错误 – 服务器未能实现合法的请求

常见状态代码、状态描述的说明如下：

-   200 OK：客户端请求成功
-   204 No Content：没有新文档，浏览器应该继续显示原来的文档
-   206 Partial Content：客户发送了一个带有Range头的GET请求，服务器完成了它
-   301 Moved Permanently：所请求的页面已经转移至新的url
-   302 Found：所请求的页面已经临时转移至新的url
-   304 Not Modified：客户端有缓冲的文档并发出了一个条件性的请求，服务器告诉客户，原来缓冲的文档还可以继续使用。
-   400 Bad Request：客户端请求有语法错误，不能被服务器所理解
-   401 Unauthorized：请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用
-   403 Forbidden：对被请求页面的访问被禁止
-   404 Not Found：请求资源不存在
-   500 Internal Server Error：服务器发生不可预期的错误
-   503 Server Unavailable：请求未完成，服务器临时过载或当机，一段时间后可能恢复正常

## **HTTP cookeie 和 session**
-   [简书 - 全面解读 HTTP Cookie](http://www.jianshu.com/p/1e28fe8125dc)
-   [阮一峰 - JavaScript 标准参考教程 - Cookie](http://javascript.ruanyifeng.com/bom/cookie.html#toc1)
-   [segmentfault - 聊一聊 Cookie](https://segmentfault.com/a/1190000004556040)
-   [知乎 - COOKIE和SESSION有什么区别？](https://www.zhihu.com/question/19786827)

## **HTTP Cache(缓存)**
- [HTTP缓存看着一篇就可以了](https://github.com/ljianshu/Blog/issues/23)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MDIwMjk0NDYsMTE0ODU5MjA0Nl19
-->