`reduce()` 方法对数组中的每个元素执行一个由您提供的**reducer**函数(升序执行)，将其结果汇总为单个返回值。

```js
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```

**1.  Accumulator (acc) (累计器)
2.  Current Value (cur) (当前值)
3.  Current Index (idx) (当前索引)
4.  Source Array (src) (源数组)**
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk4NzY4NDQ5NywtMTg4NzE2Mzg1NCwtMT
I5MzM4MjAyMl19
-->