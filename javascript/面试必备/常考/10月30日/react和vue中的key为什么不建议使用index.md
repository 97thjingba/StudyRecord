https://juejin.cn/post/6844904133430870024

总结：
1：当以数组的下标index作为key值时，其中一个元素发生了变化 就有可能导致所有元素的key值发生改变 。diff算法是比较同级之间的不同并以key值来进行关联。当对数组进行下标的变换时，比如删除第一条数据，那么以后所有的Index都会发生改变，那么key值自然也跟着全部发生改变，所以，index作为key值和没加index是一样的，并不能提升性能

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkwNzczMTQzNF19
-->