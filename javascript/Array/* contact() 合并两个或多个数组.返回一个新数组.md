### 参数

`value_N_`可选

数组和/或值，将被合并到一个新的数组中。如果省略了所有  `valueN`  参数，则  `concat`  会返回调用此方法的现存数组的一个浅拷贝。详情请参阅下文描述。

### 返回值

新的  `Array`实例

```js
var alpha = ['a', 'b', 'c'];
var numeric = [1, 2, 3];

alpha.concat(numeric);
// result in ['a', 'b', 'c', 1, 2, 3]
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM3NzA5NjgyOF19
-->