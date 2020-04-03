---


---

<p><strong>Script动态设置fontSize</strong></p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span>  oHtml <span class="token operator">=</span> document<span class="token punctuation">.</span><span class="token function">getElementsByTagName</span><span class="token punctuation">(</span><span class="token string">'html'</span><span class="token punctuation">)</span><span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span>
<span class="token keyword">const</span>  width <span class="token operator">=</span> oHtml<span class="token punctuation">.</span>clientWidth<span class="token punctuation">;</span>
oHtml<span class="token punctuation">.</span>style<span class="token punctuation">.</span>fontSize <span class="token operator">=</span> <span class="token number">12</span> <span class="token operator">*</span> <span class="token punctuation">(</span>width <span class="token operator">/</span> <span class="token number">320</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token string">"px"</span><span class="token punctuation">;</span>
</code></pre>
<p><strong>css初始化样式:</strong></p>
<pre class=" language-js"><code class="prism  language-js">body<span class="token punctuation">,</span>div<span class="token punctuation">,</span>dl<span class="token punctuation">,</span>dt<span class="token punctuation">,</span>dd<span class="token punctuation">,</span>ul<span class="token punctuation">,</span>ol<span class="token punctuation">,</span>li<span class="token punctuation">,</span>h1<span class="token punctuation">,</span>h2<span class="token punctuation">,</span>h3<span class="token punctuation">,</span>h4<span class="token punctuation">,</span>h5<span class="token punctuation">,</span>h6<span class="token punctuation">,</span>pre<span class="token punctuation">,</span>code<span class="token punctuation">,</span>form<span class="token punctuation">,</span>fieldset<span class="token punctuation">,</span>legend<span class="token punctuation">,</span>input<span class="token punctuation">,</span>button<span class="token punctuation">,</span>textarea<span class="token punctuation">,</span>p<span class="token punctuation">,</span>blockquote<span class="token punctuation">,</span>th<span class="token punctuation">,</span>td <span class="token punctuation">{</span> margin<span class="token punctuation">:</span><span class="token number">0</span><span class="token punctuation">;</span> padding<span class="token punctuation">:</span><span class="token number">0</span><span class="token punctuation">;</span> <span class="token punctuation">}</span>
</code></pre>

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjM4Njc5MzE1XX0=
-->