
|  |  useCallback|useMemo  |
|--|--|--|
| 返回值|返回缓存的函数的引用  |返回缓存的变量 |
| 使用场景|一般用在父子组件传递props，优化子组件 |一般使用在子组件优化以及含有大量计算逻辑的函数体中|
|通俗来讲|第一个函数体内不含return|函数体内含return|
|空deps[]|意味着方法没有依赖值，将不会更新|没有依赖值，不会进行更新|
|注意点|1：useCallBack不要每个函数都包一下，否则就会变成反向优化，useCallBack本身就是需要一定性能2:useCallBack并不能阻止函数重新创建,它只能通过依赖决定返回新的函数还是旧的函数,从而在依赖不变的情况下保证函数地址不变3:**useCallBack需要配合React.memo使用**

 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI5NjI2MzM0LC02ODg3NzAwMDEsLTUxND
UyODQ3OSwxMTgzNzkxNDgzXX0=
-->