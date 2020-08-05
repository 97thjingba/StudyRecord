`Array.of()` 和 `Array` 构造函数之间的区别在于处理整数参数：`Array.of(7)`  创建一个具有单个元素 **7** 的数组，而 **`Array(7)`** 创建一个长度为7的空数组（注意：这是指一个有7个空位(empty)的数组，而不是由7个`undefined`组成的数组）


### 参数

element_N_

任意个参数，将按顺序成为返回数组中的元素。

### 返回值
新的  `Array` 实例


```js
Array.of(7);       // [7] 
Array.of(1, 2, 3); // [1, 2, 3]

Array(7);          // [ , , , , , , ]
Array(1, 2, 3);    // [1, 2, 3]
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY4OTA0MjAyMV19
-->