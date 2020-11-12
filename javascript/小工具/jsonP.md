-   本质是利用了标签(link,img,script,这里使用script)具有可跨域的特性，由服务端返回预先定义好的javascript函数的调用，并且将服务端数据以该函数参数的形式传递过来

```js
<script>
    function fuc(data){
        console.log(data.name);
    }
</script>
<script src="http://www.baidu.com/api.php?callback=fuc"></script>
```

## jsonp优点

-   完美解决在测试或者开发中获取不同域下的数据,用户传递一个callback参数给服务端，然后服务端返回数据时会将这个callback参数作为函数名来包裹住JSON数据，这样客户端就可以随意定制自己的函数来自动处理返回数据了

## jsonp缺点

-   jsonp只支持get请求而不支持post请求
-   用session来判断当前用户的登录状态，跨域时会出现问题
-   jsonp存在安全性问题
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNjAxNDA1ODRdfQ==
-->