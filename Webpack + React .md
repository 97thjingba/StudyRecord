---


---

<p>webpack + react 的新手教程</p>
<p>安装:</p>
<pre class=" language-text"><code class="prism  language-text">npm i webpack --save-dev
</code></pre>
<pre class=" language-text"><code class="prism  language-text">npm i webpack-cli --save-dev
</code></pre>
<p>运行webpack</p>
<pre><code>node_modules/.bin/webpack
</code></pre>
<p>安装babel</p>
<pre class=" language-js"><code class="prism  language-js">npm i @babel<span class="token operator">/</span>core babel<span class="token operator">-</span>loader @babel<span class="token operator">/</span>preset<span class="token operator">-</span>env @babel<span class="token operator">/</span>preset<span class="token operator">-</span>react <span class="token operator">--</span>save<span class="token operator">-</span>dev
</code></pre>
<p>新建.babelrc</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token punctuation">{</span>
  <span class="token string">"presets"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">"@babel/preset-env"</span><span class="token punctuation">,</span> <span class="token string">"@babel/preset-react"</span><span class="token punctuation">]</span>
<span class="token punctuation">}</span>
</code></pre>
<p>新建webpack.config.js</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span> path <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'path'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
module<span class="token punctuation">.</span>exports <span class="token operator">=</span> <span class="token punctuation">{</span>
  entry<span class="token punctuation">:</span> <span class="token string">'./src/index.js'</span><span class="token punctuation">,</span>
  output<span class="token punctuation">:</span> <span class="token punctuation">{</span>
    filename<span class="token punctuation">:</span> <span class="token string">'bundle.js'</span><span class="token punctuation">,</span>
    path<span class="token punctuation">:</span> path<span class="token punctuation">.</span><span class="token function">resolve</span><span class="token punctuation">(</span>__dirname<span class="token punctuation">,</span> <span class="token string">'dist'</span><span class="token punctuation">)</span>
  <span class="token punctuation">}</span>
 
  module<span class="token punctuation">:</span> <span class="token punctuation">{</span>
    rules<span class="token punctuation">:</span> <span class="token punctuation">[</span>
      <span class="token punctuation">{</span>
        test<span class="token punctuation">:</span> <span class="token regex">/\.js$/</span><span class="token punctuation">,</span>
        exclude<span class="token punctuation">:</span> <span class="token regex">/node_modules/</span><span class="token punctuation">,</span>
        use<span class="token punctuation">:</span> <span class="token punctuation">{</span>
          loader<span class="token punctuation">:</span> <span class="token string">"babel-loader"</span>
        <span class="token punctuation">}</span>
      <span class="token punctuation">}</span>
    <span class="token punctuation">]</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>
</code></pre>
<p>查看默认定义文件</p>
<p>安装react 和react-dom</p>
<pre class=" language-js"><code class="prism  language-js">npm i react react<span class="token operator">-</span>dom <span class="token operator">--</span>save
</code></pre>
<p>在Html文件引入Bundle</p>
<pre class=" language-text"><code class="prism  language-text">npm i html-webpack-plugin html-loader --save-dev
</code></pre>
<p>更新webpack配置文件</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span> HtmlWebPackPlugin <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"html-webpack-plugin"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
module<span class="token punctuation">.</span>exports <span class="token operator">=</span> <span class="token punctuation">{</span>
  module<span class="token punctuation">:</span> <span class="token punctuation">{</span>
    rules<span class="token punctuation">:</span> <span class="token punctuation">[</span>
      <span class="token punctuation">{</span>
        test<span class="token punctuation">:</span> <span class="token regex">/\.js$/</span><span class="token punctuation">,</span>
        exclude<span class="token punctuation">:</span> <span class="token regex">/node_modules/</span><span class="token punctuation">,</span>
        use<span class="token punctuation">:</span> <span class="token punctuation">{</span>
          loader<span class="token punctuation">:</span> <span class="token string">"babel-loader"</span>
        <span class="token punctuation">}</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      <span class="token punctuation">{</span>
        test<span class="token punctuation">:</span> <span class="token regex">/\.html$/</span><span class="token punctuation">,</span>
        use<span class="token punctuation">:</span> <span class="token punctuation">[</span>
          <span class="token punctuation">{</span>
            loader<span class="token punctuation">:</span> <span class="token string">"html-loader"</span>
          <span class="token punctuation">}</span>
        <span class="token punctuation">]</span>
      <span class="token punctuation">}</span>
    <span class="token punctuation">]</span>
  <span class="token punctuation">}</span><span class="token punctuation">,</span>
  plugins<span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token keyword">new</span> <span class="token class-name">HtmlWebPackPlugin</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
      title<span class="token punctuation">:</span> <span class="token string">'Set Up Project'</span><span class="token punctuation">,</span> <span class="token comment">// title</span>
      template<span class="token punctuation">:</span> <span class="token string">"./index.html"</span> <span class="token comment">// 模版文件</span>
    <span class="token punctuation">}</span><span class="token punctuation">)</span>
  <span class="token punctuation">]</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>
</code></pre>
<p>构建</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span> wrapper <span class="token operator">=</span> document<span class="token punctuation">.</span><span class="token function">getElementById</span><span class="token punctuation">(</span><span class="token string">"create-article-form"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
wrapper <span class="token operator">?</span> ReactDOM<span class="token punctuation">.</span><span class="token function">render</span><span class="token punctuation">(</span><span class="token operator">&lt;</span>FormContainer <span class="token operator">/</span><span class="token operator">&gt;</span><span class="token punctuation">,</span> wrapper<span class="token punctuation">)</span> <span class="token punctuation">:</span> <span class="token boolean">false</span><span class="token punctuation">;</span>
</code></pre>
<p>安装一个webpack的开发服务器</p>
<pre class=" language-js"><code class="prism  language-js">npm i webpack<span class="token operator">-</span>dev<span class="token operator">-</span>server <span class="token operator">--</span>save<span class="token operator">-</span>dev
</code></pre>
<p>打开package.json 加入start script</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token string">"scripts"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
  <span class="token string">"start"</span><span class="token punctuation">:</span> <span class="token string">"webpack-dev-server --open --mode development"</span><span class="token punctuation">,</span>
  <span class="token string">"build"</span><span class="token punctuation">:</span> <span class="token string">"webpack"</span>
<span class="token punctuation">}</span>
</code></pre>
<pre class=" language-js"><code class="prism  language-js">npm start
</code></pre>
<p>加入css-loader 和style-loader</p>
<pre class=" language-js"><code class="prism  language-js">yarn add css<span class="token operator">-</span>loader style<span class="token operator">-</span>loader <span class="token operator">--</span>save<span class="token operator">-</span>dev
</code></pre>
<pre class=" language-js"><code class="prism  language-js"><span class="token punctuation">{</span>

	test<span class="token punctuation">:</span> <span class="token regex">/\.css$/</span><span class="token punctuation">,</span>

	loader<span class="token punctuation">:</span>  <span class="token string">'style-loader'</span><span class="token punctuation">,</span>

	<span class="token punctuation">}</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>

	test<span class="token punctuation">:</span> <span class="token regex">/\.css$/</span><span class="token punctuation">,</span>

	loader<span class="token punctuation">:</span>  <span class="token string">'css-loader'</span><span class="token punctuation">,</span>

<span class="token punctuation">}</span><span class="token punctuation">,</span>
</code></pre>
<p>参考：<a href="https://zhuanlan.zhihu.com/p/47704649">webpack+react新手教程</a></p>

