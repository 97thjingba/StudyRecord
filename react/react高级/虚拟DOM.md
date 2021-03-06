## 什么是虚拟 dom

虚拟 dom 是相对于浏览器所渲染出来的真实 dom 的，在react，vue等技术出现之前，我们要改变页面展示的内容只能通过遍历查询 dom 树的方式找到需要修改的 dom 然后修改样式行为或者结构，来达到更新 ui 的目的。

这种方式相当消耗计算资源，因为每次查询 dom 几乎都需要遍历整颗 dom 树，如果建立一个与 dom 树对应的虚拟 dom 对象（ js 对象），以对象嵌套的方式来表示 dom 树，那么每次 dom 的更改就变成了 js 对象的属性的更改，这样一来就能查找 js 对象的属性变化要比查询 dom 树的性能开销小。
Dom 就是一个普通的JavaScript对象，包含了tag，props，children 三个属性
```html
<div id="app">  
	<p class="text">hello world!!!</p>  
</div>
```
上面的HTML转换为虚拟DOM：
```js
{
  tag: 'div',
  props: {
    id: 'app'
  },
  chidren: [
    {
      tag: 'p',
      props: {
        className: 'text'
      },
      chidren: [
        'hello world!!!'
      ]
    }
  ]
}
```

## 为什么操作 dom 性能开销大

其实并不是查询 dom 树性能开销大而是 dom 树的实现模块和 js 模块是分开的这些跨模块的通讯增加了成本，以及 dom 操作引起的浏览器的回流和重绘，使得性能开销巨大，原本在 pc 端是没有性能问题的，因为 pc 的计算能力强，但是随着移动端的发展，越来越多的网页在智能手机上运行，而手机的性能参差不齐，会有性能问题。虚拟 DOM 最大的优势在于抽象了原本的渲染过程，实现了跨平台的能力，而不仅仅局限于浏览器的 DOM，可以是Android和 IOS 的原生组件，可以是近期很火热的小程序，也可以是各种GUI。

##  diff 算法
diff 算法，顾名思义，就是比对新老 VDOM 的变化，然后将变化的部分更新到视图上。对应到代码上，就是一个 diff 函数，返回一个 patches（补丁)

```js
const before = h('div', {}, 'before text') 
const after = h('div', {}, 'after text') 
const patches = diff(before, after)
```

##  二叉树的深度优先遍历（DFS）和广度优先遍历（BFS）

深度优先遍历：从根节点出发，沿着左子树方向进行纵向遍历，直到找到叶子节点为止。然后回溯到前一个节点，进行右子树节点的遍历，直到遍历完所有可达节点为止。

广度优先遍历：从根节点出发，在横向遍历二叉树层段节点的基础上纵向遍历二叉树的层次。


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk0NTk0MjEyNCwtNDk2NTEwNDM3LC0yMD
g4NzQ2NjEyXX0=
-->