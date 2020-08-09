`Object.fromEntries()` 方法把键值对列表转换为一个对象

```js
const entries = new Map([
  ['foo', 'bar'],
  ['baz', 42]
]);

const obj = Object.fromEntries(entries);

console.log(obj);
// expected output: Object { foo: "bar", baz: 42 }
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQyODc5Mzk3N119
-->