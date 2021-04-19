beforeCreate：示例初始化后被调用 el data message 皆为undified
created: 数据观测, 数据进行双向绑定, 但是el 还没有此选项
beforeMount：挂载前阶段，el 已经有了选项.  message 还是以虚拟DOM形式存在的.并没有改变
mouted: 挂载结束状态. 一般可以在这里进行 异步请求之类的. message 变为了真实的值

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxOTgyMjk4OCw1MDEyMzQzMDgsLTU0NT
Q0MTIzOCwtMjA4ODc0NjYxMl19
-->