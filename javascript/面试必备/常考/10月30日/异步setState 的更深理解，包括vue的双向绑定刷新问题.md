参考 ：https://tech.tuya.com/setstate/

总结：

`setState`并不是单纯 同步／异步，它的表现会因调用场景不同而不同：

-   在 React 钩子函数及合成事件中，它表现为异步
-   而在  `setTimeout`  、`setInterval`  等函数中，包括在  `DOM`  原生事件中，它都表现为同步

造成这种差异的本质是：React 事务机制 和 批量更新机制 的 工作方式
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzQ3MDAwNjA4XX0=
-->