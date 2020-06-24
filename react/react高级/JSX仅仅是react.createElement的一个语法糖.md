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

#### 3.1 代码逐行解读：

**第1行：** `import React from 'react';`

有 JSX 的地方，在文件开头就需要引入 React，因为实际上 JSX 是使用了 `React.createElement`，JSX 只是一个JS 的语法糖，所以需要引入 React 包，否则会报错。

**第2行：** `import ReactDOM from 'react-dom';`  
react-dom 是一个把React 代码渲染到网页端的包。如果在移动端渲染，就需要使用 React Native 的相关包。  
目前（截至2017年12月3日），React 与 ReactDOM 都更新到了 16.0.0，所以在 package.json 中可以看到这两个版本都是最新的版本。

**第4-6行：**

```jsx
const title = (
  <h1>Hello React (method 3)</h1>
);

```

这就是一段 jsx 代码，实际是 `React.createElement` 创建一个 React DOM 对象，完全等同于下面这行代码。

```javascript
const title = React.createElement("h1", {className: "main"}, "Hello React (method 3)");

```

JSX 更加直观，符合我们对 html 结构的认知，如果都用 React.createElement 去创建 React DOM，会非常的繁琐，且容易出错。

**第8行：**

```jsx
ReactDOM.render(title, document.getElementById('root'));

```
把上面创造出来的 React DOM 对象，渲染到网页 id 为 root 的元素中。

<!--stackedit_data:
eyJoaXN0b3J5IjpbNjI0NTA1MzksMTAxMTA4MDk3N119
-->