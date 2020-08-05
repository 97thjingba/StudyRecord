`findIndex()`方法返回数组中满足提供的测试函数的第一个元素的**索引**。否则返回-1


```js

const array1 = [5, 12, 8, 130, 44];

const isLargeNumber = (element) => element > 13;

console.log(array1.findIndex(isLargeNumber));
// expected output: 3
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU1ODI2NTY0Nl19
-->