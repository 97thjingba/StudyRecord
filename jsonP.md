---


---

<ul>
<li>本质是利用了标签(link,img,script,这里使用script)具有可跨域的特性，由服务端返回预先定义好的javascript函数的调用，并且将服务端数据以该函数参数的形式传递过来</li>
</ul>
<pre><code>&lt;script&gt;
    function fuc(data){
        console.log(data.name);
    }
&lt;/script&gt;
&lt;script src="http://www.baidu.com/api.php?callback=fuc"&gt;&lt;/script&gt;
</code></pre>
<h2 id="jsonp优点">jsonp优点</h2>
<ul>
<li>完美解决在测试或者开发中获取不同域下的数据,用户传递一个callback参数给服务端，然后服务端返回数据时会将这个callback参数作为函数名来包裹住JSON数据，这样客户端就可以随意定制自己的函数来自动处理返回数据了</li>
</ul>
<h2 id="jsonp缺点">jsonp缺点</h2>
<ul>
<li>jsonp只支持get请求而不支持post请求</li>
<li>用session来判断当前用户的登录状态，跨域时会出现问题</li>
<li>jsonp存在安全性问题</li>
</ul>

