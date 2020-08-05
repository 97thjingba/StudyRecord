`map()`  方法创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。


```js
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]

```

### 参数

`callback`

生成新数组元素的函数，使用三个参数：

`currentValue`

`callback`  数组中正在处理的当前元素。

`index`可选

`callback`  数组中正在处理的当前元素的索引。

`array`可选

`map` 方法调用的数组。

`thisArg`可选

执行 `callback` 函数时值被用作`this`。

### 返回值

一个由原数组每个元素执行回调函数的结果组成的新数组。
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ2NTkzMTk1Ml19
-->