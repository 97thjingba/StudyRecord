`some()` 方法测试数组中是不是至少有1个元素通过了被提供的函数测试。它返回的是一个**Boolean类型**的值


```js
const array = [1, 2, 3, 4, 5];

// checks whether an element is even
const even = (element) => element % 2 === 0;

console.log(array.some(even));
// expected output: true

```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM5NTYyNDg1Nl19
-->