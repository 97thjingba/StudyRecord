## 一、为什么需要 WebSocket？

初次接触 WebSocket 的人，都会问同样的问题：我们已经有了 HTTP 协议，为什么还需要另一个协议？它能带来什么好处？

答案很简单，因为 HTTP 协议有一个缺陷：通信只能由客户端发起。

举例来说，我们想了解今天的天气，只能是客户端向服务器发出请求，服务器返回查询结果。HTTP 协议做不到服务器主动向客户端推送信息。

![](http://www.ruanyifeng.com/blogimg/asset/2017/bg2017051507.jpg)

这种单向请求的特点，注定了如果服务器有连续的状态变化，客户端要获知就非常麻烦。我们只能使用["轮询"](https://www.pubnub.com/blog/2014-12-01-http-long-polling/)：每隔一段时候，就发出一个询问，了解服务器有没有新的信息。最典型的场景就是聊天室。

轮询的效率低，非常浪费资源（因为必须不停连接，或者 HTTP 连接始终打开）。因此，工程师们一直在思考，有没有更好的方法。WebSocket 就是这样发明的。

## 二、简介

WebSocket 协议在2008年诞生，2011年成为国际标准。所有浏览器都已经支持了。

它的最大特点就是，服务器可以主动向客户端推送信息，客户端也可以主动向服务器发送信息，是真正的双向平等对话，属于[服务器推送技术](https://en.wikipedia.org/wiki/Push_technology)的一种。

![](http://www.ruanyifeng.com/blogimg/asset/2017/bg2017051502.png)

其他特点包括：

（1）建立在 TCP 协议之上，服务器端的实现比较容易。

（2）与 HTTP 协议有着良好的兼容性。默认端口也是80和443，并且握手阶段采用 HTTP 协议，因此握手时不容易屏蔽，能通过各种 HTTP 代理服务器。

（3）数据格式比较轻量，性能开销小，通信高效。

（4）可以发送文本，也可以发送二进制数据。

（5）没有同源限制，客户端可以与任意服务器通信。

（6）协议标识符是`ws`（如果加密，则为`wss`），服务器网址就是 URL。

> ```markup
> 
> ws://example.com:80/some/path
> 
> ```

![](http://www.ruanyifeng.com/blogimg/asset/2017/bg2017051503.jpg)

## 三、客户端的简单示例

WebSocket 的用法相当简单。

下面是一个网页脚本的例子（点击[这里](http://jsbin.com/muqamiqimu/edit?js,console)看运行结果），基本上一眼就能明白。

> ```javascript
> 
> var ws = new WebSocket("wss://echo.websocket.org");
> 
> ws.onopen = function(evt) { 
>   console.log("Connection open ..."); 
>   ws.send("Hello WebSockets!");
> };
> 
> ws.onmessage = function(evt) {
>   console.log( "Received Message: " + evt.data);
>   ws.close();
> };
> 
> ws.onclose = function(evt) {
>   console.log("Connection closed.");
> };      
> 
> ```

## 四、客户端的 API

WebSocket 客户端的 API 如下。

### 4.1 WebSocket 构造函数

WebSocket 对象作为一个构造函数，用于新建 WebSocket 实例。

```javascript
 var ws = new WebSocket('ws://localhost:8080');
```

执行上面语句之后，客户端就会与服务器进行连接。

1:常用的实例对象
实例对象的`onopen`属性，用于指定连接成功后的回调函数。
 ```javascript
 ws.onopen = function () {
   ws.send('Hello Server!');
}
 ```

2:实例对象的`onclose`属性，用于指定连接关闭后的回调函数

3:实例对象的`onmessage`属性，用于指定收到服务器数据后的回调函数。

 ```javascript
 ws.onmessage = function(event) {
   var data = event.data;
   // 处理数据
 };
 ws.addEventListener("message", function(event) {
   var data = event.data;
   // 处理数据
 });
```

4:实例对象的`send()`方法用于向服务器发送数据。
发送文本的例子。
```javascript
ws.send('your message');
```

目前比较好用的是 封装好的centrifuge来进行通信
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU1NDAxMjAzNiwtMjA4ODc0NjYxMl19
-->