`Object.assign()` 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

```js
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// expected output: Object { a: 1, b: 4, c: 5 }

console.log(returnedTarget);
// expected output: Object { a: 1, b: 4, c: 5 }

```

--- 
如果目标对象中的属性具有相同的键，**则属性将被源对象中的属性覆盖**。后面的源对象的属性将类似地覆盖前面的源对象的属性
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQxMzAwMzc3MV19
-->