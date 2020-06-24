## 1：浅比较
> 浅比较就是只比较第一级，对于基本数据类型，只比较值；对于引用数据类型值，直接比较地址是否相同，不管里面内容变不变，只要地址一样，我们就认为没变。所以在这种情况下，我们以后用的时候，对于引用类型值修改状态或修改属性时候，对于它赋值的时候，我们尽可能把之前值拿过来克隆一份，赋给它新的地址就好~这是我们的注意点！我们想做性能优化的时候就可以在Component里做一个浅比较。

> =>React.PureComponent是基于浅比较，所以只要属性值是引用类型，但是修改后的值变了，但是地址不变，也不会重新渲染

引用类型：数组，对象，函数
基本类型： 布尔，null，undefined，symbol，bigInt，string，number

## 2: PureComponent 和Component

- 它们几乎完全相同，但是PureComponent通过prop和state的浅比较来实现shouldComponentUpdate，某些情况下可以用PureComponent提升性能

- PureComponent不仅会影响本身，而且会影响子组件，所以PureComponent最佳情况是展示组件

- 若是数组和对象等引用类型，则要引用不同，才会渲染

- 如果prop和state每次都会变，那么PureComponent的效率还不如Component，因为你知道的，进行浅比较也是需要时间

- 若有shouldComponentUpdate，则执行它，若没有这个方法会判断是不是PureComponent，若是，进行浅比较
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NjAxOTU4OTBdfQ==
-->