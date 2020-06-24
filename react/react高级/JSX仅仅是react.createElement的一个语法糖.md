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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk3Mzc3NzE4Nl19
-->