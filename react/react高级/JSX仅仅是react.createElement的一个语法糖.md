实际上，JSX 仅仅只是  `React.createElement(component, props, ...children)`  函数的语法糖。如下 JSX 代码：

```js
<MyButton color="blue" shadowSize={2}>
  Click Me
</MyButton>
```
会编译为：
```js
React.createElement(
  MyButton,
  {color: 'blue', shadowSize: 2},
  'Click Me'
)
```

如果没有子节点，你还可以使用自闭合的标签形式，如：

```js
<div className="sidebar" />
```

会编译为:

```js
React.createElement(
  'div',
  {className: 'sidebar'}
)
```


##  document.createElement, React.createElement 与 JSX 三种方法创建 DOM 的比较

React DOM 并不是浏览器的 DOM，而是 React DOM 只是用来告诉浏览器如何创建 DOM 的方法

html结构应该如下：

```html
<div id="root">
  <h1 id="main">Hello React</h1>
</div>

```

### 1 document.createElement

JavaScript原生方法，没有过多需要解释的部分。

```javascript
// 方法1：document.createElement
const title = document.createElement('h1');
title.innerText='Hello React (method 1)';
title.className='main';
document.getElementById('root').appendChild(title);

```

### 2 React.creaetElement

第二种方法是用 React 的 createElement 来创建 React DOM。

```javascript
// 方法2：React.createElement
import React from 'react';
import ReactDOM from 'react-dom';

const title = React.createElement("h1", {className: "main"}, "Hello React (method 2)");
ReactDOM.render(title, document.getElementById('root'));
```

  
 ### 3 JSX

JSX 是一种 JavaScript 的语法糖。Facebook 开发JSX出来，主要用于 React 中。虽然 JSX 的内容会长得像 html，但还是 JavaScript。

用 JSX 方法来创建 React DOM 的代码如下：

```javascript
// 方法3：JSX
import React from 'react';
import ReactDOM from 'react-dom';

const title = (
  <h1>Hello React (method 3)</h1>
);

ReactDOM.render(title, document.getElementById('root'));
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAxMTA4MDk3N119
-->