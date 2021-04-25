钩子函数

 	created	activated
触发顺序	组件创建最初始	created  =>  mounted =>activated
触发次数	只在组件刚创建时创建	在使用keep-alive标签中有效，每次进入都会执行钩子中的函数
 

created()：在创建vue对象时，当html渲染之前就触发；但是注意，全局vue.js不强制刷新或者重启时只创建一次，也就是说，created()只会触发一次；

activated()：在vue对象存活的情况下，进入当前存在activated()函数的页面时，一进入页面就触发；可用于初始化页面数据等，

可以解决router跳转后不刷新页面数据问题


参考：https://blog.csdn.net/qq_41071477/article/details/102452051

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQxNDY4Mjc5N119
-->