
**Script动态设置fontSize**

```js
const  oHtml = document.getElementsByTagName('html')[0]
const  width = oHtml.clientWidth;
oHtml.style.fontSize = 12 * (width / 320) + "px";

```

**css初始化样式:**
```js
body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,pre,code,form,fieldset,legend,input,button,textarea,p,blockquote,th,td { margin:0; padding:0; }
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMDA3NTY1NzldfQ==
-->