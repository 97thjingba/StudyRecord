
### 1. px（绝对单位）

像素，计算机屏幕上的一个点。页面按照精确的像素进行样式展示。

### 2. em（相对单位）

指字体高度。基准点为父节点字体的大小，浏览器默认字体为 16px（1em=16px），如果元素自身定义了 font-size，则按照自身的值进行计算。因此，整个页面内的1em可以是不同的值。

【e.g.】根元素样式 font-size:62.5%; 意思为 16px*62.5%=10px，即显示在页面的字体大小是 10px（1em=10px）。

em 的特点是 em 是个相对值，它会根据父级元素的大小而变化，但是如果嵌套了多个元素，要计算它的大小，就要使用 rem。

### 3. rem（相对单位）

可理解为“root em”, 相对根节点的字体大小来计算，是截止目前用的最多的单位。

### 4. vh（视窗高度）

viewpoint height，视窗高度，1vh 等于视窗高度的 1%。

【e.g.】元素 height: 10vh; 视窗高度为 100px，则元素高度为 height = 100px * 10% = 10px

### 5. vw（视窗宽度）

viewpoint width，视窗宽度，1vw 等于视窗宽度的 1%。

【e.g.】元素 width: 5vh; 视窗宽度为 200px，则元素宽度为 width = 200px * 5% = 10px

### 6. vmin

vw 和 vh 中较小的那个。

### 7. vmax

vw 和vh 中较大的那个。

参考：[https://juejin.im/post/5b63c3f2518825210576000e](https://juejin.im/post/5b63c3f2518825210576000e)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjE2OTIyMDg3LC0xNDM4Mjk2MTE2XX0=
-->