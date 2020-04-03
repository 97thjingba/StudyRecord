---


---

<h2 id="初始化项目"><strong>初始化项目</strong></h2>
<p>首先我们先给项目创建一个文件夹 webpack-react-tutorial：</p>
<pre class=" language-js"><code class="prism  language-js">mkdir webpack<span class="token operator">-</span>react<span class="token operator">-</span>tutorial <span class="token operator">&amp;&amp;</span> cd webpack<span class="token operator">-</span>react<span class="token operator">-</span>tutorial

</code></pre>
<p>接着在这个文件夹下创建一个src的子文件夹：</p>
<pre class=" language-text"><code class="prism  language-text">mkdir -p src
</code></pre>
<p>初始化项目：</p>
<pre class=" language-js"><code class="prism  language-js">npm init <span class="token operator">-</span>y 

</code></pre>
<h2 id="如何安装配置webpack"><strong>如何安装配置webpack</strong></h2>
<p><strong>webpack</strong></p>
<p>webpack是一款非常有用的前端打包工具，了解<a href="https://link.zhihu.com/?target=https%3A//www.valentinog.com/blog/from-gulp-to-webpack-quickstart/">如何使用它</a>是React开发者的基础，因为webpack可以将React组件转化成几乎所有浏览器都可以运行的JS code。</p>
<p>让我们先来安装它：</p>
<pre class=" language-text"><code class="prism  language-text">npm i webpack --save-dev
</code></pre>
<p>你可能会需要webpack-cli，所以也先装上</p>
<pre class=" language-text"><code class="prism  language-text">npm i webpack-cli --save-dev
</code></pre>
<p>接着在package.json里添加webpack的指令</p>
<pre class=" language-text"><code class="prism  language-text">"scripts": {
  "build": "webpack --mode production"
}
</code></pre>
<p>到目前为止还不需要写webpack的配置文件。</p>
<p>老版的webpack会自动去找配置文件，但是从webpack 4之后，你就需要自己去匹配需要的配置文件了。</p>
<p>下面我们来安装和配置Babel来编译我们的代码。</p>
<p><strong>初始化Babel</strong></p>
<p>为什么要使用Babel?</p>
<p>React Component大多是用JS ES6语法来写的，而浏览器没办法运行ES6的语法，所以就需要工具来将ES6的代码转化成浏览器可以运行的代码（通常是es5的语法）。</p>
<p>webpack本身是不会做这件事情的，需要靠转换器：loader。</p>
<p>一个webpack loader作用就是把输入进去的文件转化成指定的文件格式输出。其中<strong>babel-loader负责将传入的es6文件转化成浏览器可以运行的文件</strong>。</p>
<p>babel-loader需要利用Babel，所以需要预先将Babel配置好。</p>
<ol>
<li>**babel preset env：**将ES6的代码转成ES5(注意：babel-preset-es2015已经被废弃了)</li>
</ol>
<p>2**.babel preset react:** 将JSX语法编译成JS</p>
<p>接着安装这两个依赖：</p>
<pre class=" language-js"><code class="prism  language-js">npm i @babel<span class="token operator">/</span>core babel<span class="token operator">-</span>loader @babel<span class="token operator">/</span>preset<span class="token operator">-</span>env @babel<span class="token operator">/</span>preset<span class="token operator">-</span>react <span class="token operator">--</span>save<span class="token operator">-</span>dev

</code></pre>
<p>不要忘了配置Babel! 首先要在webpack-react-tutorial文件夹里新建一个文件.babelrc，内容为</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token punctuation">{</span>
  <span class="token string">"presets"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">"@babel/preset-env"</span><span class="token punctuation">,</span> <span class="token string">"@babel/preset-react"</span><span class="token punctuation">]</span>
<span class="token punctuation">}</span>

</code></pre>
<p>到这个时候，就可以写一小部分webpack的配置文件了。</p>
<p>创建一个新的文件webpack.config.js，内容为</p>
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
<p>这个webpack的配置很简单。意思就是所有以.js结尾的文件都会用babel-loader把ES6编译转化成ES5的文件。</p>
<p>同时它定义了输入文件的路径为 src/index.js，输出为dist/bundle.js。webpack 4里这两行代码你不写也行，webpack会默认帮你加，但是为了代码可读性，我们还是把它加上。</p>
<p>配置完成之后，我们就可以开始写React 组件了。</p>
<h2 id="写react组件"><strong>写React组件</strong></h2>
<p>这里会写两种React组件：<a href="https://link.zhihu.com/?target=https%3A//medium.com/%40learnreact/container-components-c0e67432e005">容器</a>、<a href="https://link.zhihu.com/?target=https%3A//medium.com/%40dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0">展示</a>组件。如果不了解这两种组件概念的同学可以先了解一下。</p>
<p>简单来说: 容器跟展示组件是React组件的两种模式。</p>
<p>容器组件: 一般比较重数据处理的逻辑会写在这，比如监听外界传入（例如redux） state的变化，或者处理组件内部的state，等等。</p>
<p>展示组件：顾名思义，就是仅仅用来展示的。它一般都是一个纯箭头函数，接受容器组件通过props传来的数据，然后展示我们希望展示的html结构。</p>
<p>在下面的例子中，你会看到它们长啥样。</p>
<p>在本节中，我们来创建只有text input 的超级简单的React表单。</p>
<p>首先先把React库引进来：</p>
<pre class=" language-js"><code class="prism  language-js">npm i react react<span class="token operator">-</span>dom <span class="token operator">--</span>save

</code></pre>
<p>然后创建两个子文件夹来分别放React 容器/展示组件</p>
<pre class=" language-js"><code class="prism  language-js">mkdir <span class="token operator">-</span>p src<span class="token operator">/</span>js<span class="token operator">/</span>components<span class="token operator">/</span><span class="token punctuation">{</span>container<span class="token punctuation">,</span>presentational<span class="token punctuation">}</span>

</code></pre>
<p>接着我们来写一个容器组件，它有下面的特点</p>
<ol>
<li>
<p>有自己的state</p>
</li>
<li>
<p>渲染一个html表单</p>
</li>
</ol>
<p>将这个容器组件放在container里</p>
<pre class=" language-js"><code class="prism  language-js">touch src<span class="token operator">/</span>js<span class="token operator">/</span>components<span class="token operator">/</span>container<span class="token operator">/</span>FormContainer<span class="token punctuation">.</span>js

</code></pre>
<p>容器组件的代码如下：</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">import</span> React<span class="token punctuation">,</span> <span class="token punctuation">{</span> Component <span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">"react"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> ReactDOM <span class="token keyword">from</span> <span class="token string">"react-dom"</span><span class="token punctuation">;</span>

<span class="token keyword">class</span> <span class="token class-name">FormContainer</span> <span class="token keyword">extends</span> <span class="token class-name">Component</span> <span class="token punctuation">{</span>
  <span class="token function">constructor</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
 <span class="token keyword">super</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

 <span class="token keyword">this</span><span class="token punctuation">.</span>state <span class="token operator">=</span> <span class="token punctuation">{</span>
      title<span class="token punctuation">:</span> <span class="token string">""</span>
 <span class="token punctuation">}</span><span class="token punctuation">;</span>
 <span class="token punctuation">}</span>

  <span class="token function">render</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
 <span class="token keyword">return</span> <span class="token punctuation">(</span>
 <span class="token operator">&lt;</span>form id<span class="token operator">=</span><span class="token string">"article-form"</span><span class="token operator">&gt;</span>
 <span class="token operator">&lt;</span><span class="token operator">/</span>form<span class="token operator">&gt;</span>
 <span class="token punctuation">)</span><span class="token punctuation">;</span>
 <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<span class="token keyword">export</span> <span class="token keyword">default</span> FormContainer<span class="token punctuation">;</span>

</code></pre>
<p>到目前为止，这个组件还没啥用，它只是一个包裹着子展示组件的外壳。</p>
<p>所以我们来定义一下子组件Input吧。</p>
<p>我们知道<a href="https://link.zhihu.com/?target=https%3A//developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">html input</a>有下列的属性：</p>
<ul>
<li>type</li>
<li>class</li>
<li>id</li>
<li>value</li>
<li>required</li>
</ul>
<p>所有的这些属性都由容器组件通过props传给它，这种组件叫做<a href="https://link.zhihu.com/?target=https%3A//reactjs.org/docs/forms.html%23controlled-components">controlled component</a>。</p>
<p>写一个react组件，最好给它加上<a href="https://link.zhihu.com/?target=https%3A//reactjs.org/docs/typechecking-with-proptypes.html">Prop Types</a>，<strong>这样一来可以做输入的数据类型检测，二来别人用你的组件，可以很快知道这个组件需要什么input</strong>。</p>
<p>安装prop-types</p>
<pre class=" language-js"><code class="prism  language-js">npm i prop<span class="token operator">-</span>types <span class="token operator">--</span>save<span class="token operator">-</span>dev

</code></pre>
<p>接着写这个展示组件</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">import</span> React <span class="token keyword">from</span> <span class="token string">"react"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> PropTypes <span class="token keyword">from</span> <span class="token string">"prop-types"</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> <span class="token function-variable function">Input</span> <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token punctuation">{</span> label<span class="token punctuation">,</span> text<span class="token punctuation">,</span> type<span class="token punctuation">,</span> id<span class="token punctuation">,</span> value<span class="token punctuation">,</span> handleChange <span class="token punctuation">}</span><span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">(</span>
  <span class="token operator">&lt;</span>div className<span class="token operator">=</span><span class="token string">"form-group"</span><span class="token operator">&gt;</span>
    <span class="token operator">&lt;</span>label htmlFor<span class="token operator">=</span><span class="token punctuation">{</span>label<span class="token punctuation">}</span><span class="token operator">&gt;</span><span class="token punctuation">{</span>text<span class="token punctuation">}</span><span class="token operator">&lt;</span><span class="token operator">/</span>label<span class="token operator">&gt;</span>
    <span class="token operator">&lt;</span>input
      type<span class="token operator">=</span><span class="token punctuation">{</span>type<span class="token punctuation">}</span>
      className<span class="token operator">=</span><span class="token string">"form-control"</span>
      id<span class="token operator">=</span><span class="token punctuation">{</span>id<span class="token punctuation">}</span>
      value<span class="token operator">=</span><span class="token punctuation">{</span>value<span class="token punctuation">}</span>
      onChange<span class="token operator">=</span><span class="token punctuation">{</span>handleChange<span class="token punctuation">}</span>
      required
    <span class="token operator">/</span><span class="token operator">&gt;</span>
  <span class="token operator">&lt;</span><span class="token operator">/</span>div<span class="token operator">&gt;</span>
<span class="token punctuation">)</span><span class="token punctuation">;</span>
Input<span class="token punctuation">.</span>propTypes <span class="token operator">=</span> <span class="token punctuation">{</span>
  label<span class="token punctuation">:</span> PropTypes<span class="token punctuation">.</span>string<span class="token punctuation">.</span>isRequired<span class="token punctuation">,</span>
  text<span class="token punctuation">:</span> PropTypes<span class="token punctuation">.</span>string<span class="token punctuation">.</span>isRequired<span class="token punctuation">,</span>
  type<span class="token punctuation">:</span> PropTypes<span class="token punctuation">.</span>string<span class="token punctuation">.</span>isRequired<span class="token punctuation">,</span>
  id<span class="token punctuation">:</span> PropTypes<span class="token punctuation">.</span>string<span class="token punctuation">.</span>isRequired<span class="token punctuation">,</span>
  value<span class="token punctuation">:</span> PropTypes<span class="token punctuation">.</span>string<span class="token punctuation">.</span>isRequired<span class="token punctuation">,</span>
  handleChange<span class="token punctuation">:</span> PropTypes<span class="token punctuation">.</span>func<span class="token punctuation">.</span>isRequired
<span class="token punctuation">}</span><span class="token punctuation">;</span>
<span class="token keyword">export</span> <span class="token keyword">default</span> Input<span class="token punctuation">;</span>

</code></pre>
<p>到这一步我们就可以在容器组件里渲染Input这个子组件了</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">import</span> React<span class="token punctuation">,</span> <span class="token punctuation">{</span> Component <span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">"react"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> ReactDOM <span class="token keyword">from</span> <span class="token string">"react-dom"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> Input <span class="token keyword">from</span> <span class="token string">"../presentational/Input"</span><span class="token punctuation">;</span>
<span class="token keyword">class</span> <span class="token class-name">FormContainer</span> <span class="token keyword">extends</span> <span class="token class-name">Component</span> <span class="token punctuation">{</span>
  <span class="token function">constructor</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">super</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">this</span><span class="token punctuation">.</span>state <span class="token operator">=</span> <span class="token punctuation">{</span>
      seo_title<span class="token punctuation">:</span> <span class="token string">""</span>
    <span class="token punctuation">}</span><span class="token punctuation">;</span>
    <span class="token keyword">this</span><span class="token punctuation">.</span>handleChange <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>handleChange<span class="token punctuation">.</span><span class="token function">bind</span><span class="token punctuation">(</span><span class="token keyword">this</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
  <span class="token function">handleChange</span><span class="token punctuation">(</span>event<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">this</span><span class="token punctuation">.</span><span class="token function">setState</span><span class="token punctuation">(</span><span class="token punctuation">{</span> <span class="token punctuation">[</span>event<span class="token punctuation">.</span>target<span class="token punctuation">.</span>id<span class="token punctuation">]</span><span class="token punctuation">:</span> event<span class="token punctuation">.</span>target<span class="token punctuation">.</span>value <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
  <span class="token function">render</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">const</span> <span class="token punctuation">{</span> seo_title <span class="token punctuation">}</span> <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>state<span class="token punctuation">;</span>
    <span class="token keyword">return</span> <span class="token punctuation">(</span>
      <span class="token operator">&lt;</span>form id<span class="token operator">=</span><span class="token string">"article-form"</span><span class="token operator">&gt;</span>
        <span class="token operator">&lt;</span>Input
          text<span class="token operator">=</span><span class="token string">"SEO title"</span>
          label<span class="token operator">=</span><span class="token string">"seo_title"</span>
          type<span class="token operator">=</span><span class="token string">"text"</span>
          id<span class="token operator">=</span><span class="token string">"seo_title"</span>
          value<span class="token operator">=</span><span class="token punctuation">{</span>seo_title<span class="token punctuation">}</span>
          handleChange<span class="token operator">=</span><span class="token punctuation">{</span><span class="token keyword">this</span><span class="token punctuation">.</span>handleChange<span class="token punctuation">}</span>
        <span class="token operator">/</span><span class="token operator">&gt;</span>
      <span class="token operator">&lt;</span><span class="token operator">/</span>form<span class="token operator">&gt;</span>
    <span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token keyword">export</span> <span class="token keyword">default</span> FormContainer<span class="token punctuation">;</span>

</code></pre>
<p>写好组件之后，就可以用webpack来打包这些代码啦。</p>
<p>由于前面我们已经定义了webpack入口文件是 ./src/index.js</p>
<p>所以我们先创建一个index.js文件，在里面引入React组件</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">import</span> FormContainer <span class="token keyword">from</span> <span class="token string">"./js/components/container/FormContainer"</span><span class="token punctuation">;</span>

</code></pre>
<p>写好之后，激动人心的时刻到了!</p>
<p>我们终于可以通过运行</p>
<pre class=" language-js"><code class="prism  language-js">npm run build

</code></pre>
<p>来生成打包文件，由于我们在配置里定义了输出文件为：dist/bundle.js，所以一切顺利的话， 你现在应该可以看到一个新生成的dist文件，里面有一个bundle.js文件。</p>
<h2 id="在html文件引入bundle"><strong>在HTML文件引入bundle</strong></h2>
<p>为了展示我们的React组件，我们需要让webpack生成一个html文件。上面我们生成的bundle.js就会放在这个html文件的</p><p>webpack需要两个工具来生成这个html文件：<a href="https://link.zhihu.com/?target=https%3A//webpack.js.org/plugins/html-webpack-plugin/">html-webpack-plugin</a>跟<a href="https://link.zhihu.com/?target=https%3A//webpack.js.org/loaders/html-loader/">html-loader</a></p>
<p>首先添加这两个依赖：</p>
<pre class=" language-text"><code class="prism  language-text">npm i html-webpack-plugin html-loader --save-dev
</code></pre>
<p>然后更新webpack的配置文件</p>
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
      title<span class="token punctuation">:</span> <span class="token string">'Set Up Project'</span><span class="token punctuation">,</span>
      filename<span class="token punctuation">:</span> <span class="token string">"./index.html"</span>
    <span class="token punctuation">}</span><span class="token punctuation">)</span>
  <span class="token punctuation">]</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>

</code></pre>
<p>index.html是我们的模板文件，里面定义了React Component需要插入进入的容器</p><div>create-article-form</div>，不要忘了在FormContainer里用React.render绑定这个。<p></p>
<pre class=" language-js"><code class="prism  language-js"><span class="token operator">&lt;</span><span class="token operator">!</span>doctype html<span class="token operator">&gt;</span>
<span class="token operator">&lt;</span>html<span class="token operator">&gt;</span>
  <span class="token operator">&lt;</span>head<span class="token operator">&gt;</span>
    <span class="token operator">&lt;</span>title<span class="token operator">&gt;</span>Getting Started<span class="token operator">&lt;</span><span class="token operator">/</span>title<span class="token operator">&gt;</span>
  <span class="token operator">&lt;</span><span class="token operator">/</span>head<span class="token operator">&gt;</span>
  <span class="token operator">&lt;</span>body<span class="token operator">&gt;</span>
    <span class="token operator">&lt;</span>div id<span class="token operator">=</span><span class="token string">'create-article-form'</span><span class="token operator">&gt;</span>

    <span class="token operator">&lt;</span><span class="token operator">/</span>div<span class="token operator">&gt;</span>
  <span class="token operator">&lt;</span><span class="token operator">/</span>body<span class="token operator">&gt;</span>
<span class="token operator">&lt;</span><span class="token operator">/</span>html<span class="token operator">&gt;</span>

</code></pre>
<p>在./src/js/components/container/FormContainer.js 加上下面的代码：</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span> wrapper <span class="token operator">=</span> document<span class="token punctuation">.</span><span class="token function">getElementById</span><span class="token punctuation">(</span><span class="token string">"create-article-form"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
wrapper <span class="token operator">?</span> ReactDOM<span class="token punctuation">.</span><span class="token function">render</span><span class="token punctuation">(</span><span class="token operator">&lt;</span>FormContainer <span class="token operator">/</span><span class="token operator">&gt;</span><span class="token punctuation">,</span> wrapper<span class="token punctuation">)</span> <span class="token punctuation">:</span> <span class="token boolean">false</span><span class="token punctuation">;</span>

</code></pre>
<p>最后，在跑一次构建：</p>
<pre class=" language-js"><code class="prism  language-js">npm run build

</code></pre>
<p>这时候在dist文件夹里就会看到生成的html文件，由于html-webpack-plugin，bundle文件会被自动注入html里。</p>
<p>在浏览器里打开./dist/index.html，你会看到这个React表单。</p>
<h2 id="webpack-dev-server">webpack dev Server</h2>
<p>目前为止，我们来遗留一个问题：每次修改文件的时候，都需要重新跑一次编译</p>
<pre class=" language-js"><code class="prism  language-js">npm run build

</code></pre>
<p>这样是很麻烦的，我们想达到的效果是<strong>自动重新编译</strong>。</p>
<p>达到这个目标很简单，只需要3行配置就可以启动运行一个开发服务器。</p>
<p>启动服务器之后webpack就会在浏览器里启动你的应用，而且当你修改保存代码之后，webpack dev server还会<strong>自动刷新浏览器的窗口</strong>。</p>
<p>在启动webpack dev server前，需要先安装</p>
<pre class=" language-js"><code class="prism  language-js">npm i webpack<span class="token operator">-</span>dev<span class="token operator">-</span>server <span class="token operator">--</span>save<span class="token operator">-</span>dev

</code></pre>
<p>打开package.json 加入start script</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token string">"scripts"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
  <span class="token string">"start"</span><span class="token punctuation">:</span> <span class="token string">"webpack-dev-server --open --mode development"</span><span class="token punctuation">,</span>
  <span class="token string">"build"</span><span class="token punctuation">:</span> <span class="token string">"webpack"</span>
<span class="token punctuation">}</span>

</code></pre>
<p>保存这个文件，最后在跑这个命令</p>
<pre class=" language-js"><code class="prism  language-js">npm start
</code></pre>
<p>参考：<a href="https://zhuanlan.zhihu.com/p/47704649">https://zhuanlan.zhihu.com/p/47704649</a></p>

