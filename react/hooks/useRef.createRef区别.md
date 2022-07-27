
|  | useRef |createRef |
|--|--|--|
| 相同点 | 当作dom句柄控制dom事件 |当作dom句柄控制dom事件|
|返回值|返回相同的引用|返回不同的引用|


useRef 注意点：
1： useRef创建的是{current : ... }对象.在每次渲染的时候返回同一个ref对象
2： ref对象发生更改的时候，useRef不会通知，变成.current属性bu

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg1MjU3MTQ2OF19
-->