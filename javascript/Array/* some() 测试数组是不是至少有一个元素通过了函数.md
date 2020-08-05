`some()` 方法测试数组中是不是至少有1个元素通过了被提供的函数测试。它返回的是一个**Boolean类型**的值


```js
const array = [1, 2, 3, 4, 5];

// checks whether an element is even
const even = (element) => element % 2 === 0;

console.log(array.some(even));
// expected output: true

```

### 参数

`callback`

用来测试每个元素的函数，接受三个参数：

	`element`

	数组中正在处理的元素。

	`index` 可选

	数组中正在处理的元素的索引值。

	`array`可选

	`some()`被调用的数组。

`thisArg`可选

执行  `callback`  时使用的 `this` 值。

### 返回值

数组中有至少一个元素通过回调函数的测试就会返回**`true`**；所有元素都没有通过回调函数的测试返回值才会为false。

<!--stackedit_data:
eyJoaXN0b3J5IjpbNzI2Njc5OTcwLC0zOTU2MjQ4NTZdfQ==
-->