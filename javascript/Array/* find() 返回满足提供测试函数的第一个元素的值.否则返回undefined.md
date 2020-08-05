`find()` 方法返回数组中满足提供的测试函数的**第一个元素**的值。否则返回 `undefined`

```js
const array1 = [5, 12, 8, 130, 44];

const found = array1.find(element => element > 10);

console.log(found);
// expected output: 12
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQxOTQ4MzY1M119
-->