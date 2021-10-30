参考 ：https://tech.tuya.com/setstate/

总结：

`setState`并不是单纯 同步／异步，它的表现会因调用场景不同而不同：

-   在 React 钩子函数及合成事件中，它表现为异步
-   而在  `setTimeout`  、`setInterval`  等函数中，包括在  `DOM`  原生事件中，它都表现为同步

造成这种差异的本质是：React 事务机制 和 批量更新机制 的 工作方式

--- 
react的事件执行机制

https://vue3js.cn/interview/React/SyntheticEvent.html#%E4%BA%8C%E3%80%81%E6%89%A7%E8%A1%8C%E9%A1%BA%E5%BA%8F

-   React 所有事件都挂载在 document 对象上
-   当真实 DOM 元素触发事件，会冒泡到 document 对象后，再处理 React 事件
-   所以会先执行原生事件，然后处理 React 事件
-   最后真正执行 document 上挂载的事件

## 三、总结

`React`事件机制总结如下：

-   React 上注册的事件最终会绑定在document这个 DOM 上，而不是 React 组件对应的 DOM(减少内存开销就是因为所有的事件都绑定在 document 上，其他节点没有绑定事件)
-   React 自身实现了一套事件冒泡机制，所以这也就是为什么我们 event.stopPropagation()无效的原因。
-   React 通过队列的形式，从触发的组件向父组件回溯，然后调用他们 JSX 中定义的 callback
-   React 有一套自己的合成事件 SyntheticEvent
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjExOTI4MDU2Nyw3NDcwMDA2MDhdfQ==
-->