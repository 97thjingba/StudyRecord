beforeCreate：示例初始化后被调用 el data message 皆为undified
created: 数据观测, 数据进行双向绑定, 但是el 还没有此选项
beforeMount：挂载前阶段，el 已经有了选项.  message 还是以虚拟DOM形式存在的.并没有改变
mouted: 挂载结束状态. 一般可以在这里进行 异步请求之类的. message 变为了真实的值
beforeUpdate： 数据更新时调用.发生在虚拟DOM打补丁之前
UPDATE: 数据更改导致的虚拟DOM重新渲染和打补丁. 在这以后会调用该钩子
beforeDestory：实例销毁之前调用. 此时实例还能可用
destroyed：Vue 实例销毁后调用
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MDA0MjgwMzMsNTAxMjM0MzA4LC01ND
U0NDEyMzgsLTIwODg3NDY2MTJdfQ==
-->