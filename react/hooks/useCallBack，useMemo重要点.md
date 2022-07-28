
|  |  useCallback|useMemo  |
|--|--|--|
| 返回值|返回缓存的函数的引用  |返回缓存的变量 |
| 使用场景|一般用在父子组件传递props，优化子组件 |一般使用在子组件优化以及含有大量计算逻辑的函数体中|
|通俗来讲|第一个函数体内不含return|函数体内含return|
|空deps[]|意味着方法没有依赖值，将不会更新|没有依赖值，不会进行更新|
|注意点|1：useCallBack不要每个函数都包一下，否则就会变成反向优化，useCallBack本身就是需要一定性能2:useCallBack并不能阻止函数重新创建,它只能通过依赖决定返回新的函数还是旧的函数,从而在依赖不变的情况下保证函数地址不变3:**useCallBack需要配合React.memo使用**4:https://juejin.cn/post/7107943235099557896|memo用来优化**函数组件**的重复渲染行为，针对的是一个**组件**useMemo返回一个memoized的**值** |
 
---- 
|  | useCallBack |useMemoizedFn |
|--|--|--|
|区别|依赖变化会导致返回的函数的地址变化 | 可以省略第二个参数 deps，同时保证函数地址永远不会变化|

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMTc5MjkyNDQsLTE3NTEyNTM0NDIsLT
IyODUxMjQxMiwtNjg4NzcwMDAxLC01MTQ1Mjg0NzksMTE4Mzc5
MTQ4M119
-->