---


---

<h3 id="panresponder">PanResponder</h3>
<p>PanResponder 是 React Native 实现的一套手势相应方法</p>
<h3 id="基本用法">基本用法</h3>
<p>这是官方给的例子.但是由于componentWillMount 将在以后被移除.所以把这个东西最好放到constructor里面</p>
<pre class=" language-jsx"><code class="prism  language-jsx">  componentWillMount<span class="token punctuation">:</span> <span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">this</span><span class="token punctuation">.</span>_panResponder <span class="token operator">=</span> PanResponder<span class="token punctuation">.</span><span class="token function">create</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
      <span class="token comment">// 要求成为响应者：</span>
      onStartShouldSetPanResponder<span class="token punctuation">:</span> <span class="token punctuation">(</span>evt<span class="token punctuation">,</span> gestureState<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token boolean">true</span><span class="token punctuation">,</span>
      onStartShouldSetPanResponderCapture<span class="token punctuation">:</span> <span class="token punctuation">(</span>evt<span class="token punctuation">,</span> gestureState<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token boolean">true</span><span class="token punctuation">,</span>
      onMoveShouldSetPanResponder<span class="token punctuation">:</span> <span class="token punctuation">(</span>evt<span class="token punctuation">,</span> gestureState<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token boolean">true</span><span class="token punctuation">,</span>
      onMoveShouldSetPanResponderCapture<span class="token punctuation">:</span> <span class="token punctuation">(</span>evt<span class="token punctuation">,</span> gestureState<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token boolean">true</span><span class="token punctuation">,</span>

      onPanResponderGrant<span class="token punctuation">:</span> <span class="token punctuation">(</span>evt<span class="token punctuation">,</span> gestureState<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
        <span class="token comment">// 开始手势操作。给用户一些视觉反馈，让他们知道发生了什么事情！</span>

        <span class="token comment">// gestureState.{x,y}0 现在会被设置为0</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      onPanResponderMove<span class="token punctuation">:</span> <span class="token punctuation">(</span>evt<span class="token punctuation">,</span> gestureState<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
        <span class="token comment">// 最近一次的移动距离为gestureState.move{X,Y}</span>

        <span class="token comment">// 从成为响应者开始时的累计手势移动距离为gestureState.d{x,y}</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      onPanResponderTerminationRequest<span class="token punctuation">:</span> <span class="token punctuation">(</span>evt<span class="token punctuation">,</span> gestureState<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token boolean">true</span><span class="token punctuation">,</span>
      onPanResponderRelease<span class="token punctuation">:</span> <span class="token punctuation">(</span>evt<span class="token punctuation">,</span> gestureState<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
        <span class="token comment">// 用户放开了所有的触摸点，且此时视图已经成为了响应者。</span>
        <span class="token comment">// 一般来说这意味着一个手势操作已经成功完成。</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      onPanResponderTerminate<span class="token punctuation">:</span> <span class="token punctuation">(</span>evt<span class="token punctuation">,</span> gestureState<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
        <span class="token comment">// 另一个组件已经成为了新的响应者，所以当前手势将被取消。</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      onShouldBlockNativeResponder<span class="token punctuation">:</span> <span class="token punctuation">(</span>evt<span class="token punctuation">,</span> gestureState<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
        <span class="token comment">// 返回一个布尔值，决定当前组件是否应该阻止原生组件成为JS响应者</span>
        <span class="token comment">// 默认返回true。目前暂时只支持android。</span>
        <span class="token keyword">return</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span><span class="token punctuation">,</span>

  render<span class="token punctuation">:</span> <span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token punctuation">(</span>
      <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>View</span> <span class="token spread"><span class="token punctuation">{</span><span class="token punctuation">...</span><span class="token attr-value">this</span><span class="token punctuation">.</span><span class="token attr-value">_panResponder</span><span class="token punctuation">.</span><span class="token attr-value">panHandlers</span><span class="token punctuation">}</span></span> <span class="token punctuation">/&gt;</span></span>
    <span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span><span class="token punctuation">,</span>
</code></pre>
<p>这个东西可以放在任何的一个view里.任何的一个view都可以作为一个手势系统.只不过我们使用的时候是没有被激活的。</p>
<p>有一些注意的点:在使用的时候我踩下的坑<br>
<strong>不要把这个和TouchOpacity 等一起使用.PanResponder事件会被这些组件给阻塞</strong></p>
<p>参考：<a href="https://reactnative.cn/docs/0.41/panresponder/">官方文档</a></p>

