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

```js
### `Map` 转化为 `Object`

通过 `Object.fromEntries`， 可以将 [`Map`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Map)  转换为 [`Object`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object):

```js
const map = new Map([ ['foo', 'bar'], ['baz', 42] ]);
const obj = Object.fromEntries(map);
console.log(obj); // { foo: "bar", baz: 42 }

```

### `Array` 转化为 `Object`

通过 `Object.fromEntries`， 可以将  [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array)  转换为 [`Object`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object):

```js
const arr = [ ['0', 'a'], ['1', 'b'], ['2', 'c'] ];
const obj = Object.fromEntries(arr);
console.log(obj); // { 0: "a", 1: "b", 2: "c" }

```

### 对象转换

`Object.fromEntries` 是与 [`Object.entries()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/entries)  相反的方法，用 [数组处理函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#Methods_2) 可以像下面这样转换对象：

```js
const object1 = { a: 1, b: 2, c: 3 };

const object2 = Object.fromEntries(
  Object.entries(object1)
  .map(([ key, val ]) => [ key, val * 2 ])
);

console.log(object2);
// { a: 2, b: 4, c: 6 }
```

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY4MjU2NjY0MSwtNDI4NzkzOTc3XX0=
-->