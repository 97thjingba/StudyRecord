`keys()` 方法返回一个包含数组中每个索引键的`**Array Iterator**`对象。


```js
const array1 = ['a', 'b', 'c'];
const iterator = array1.entries();

for (const item of iterator) {
  console.log(item);
  console.log(item[0])
}

// expected output: 0
// expected output: 1
// expected output: 2
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NzUzNjU5NDldfQ==
-->