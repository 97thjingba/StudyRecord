###  参数

`arrayLike`

想要转换成数组的**伪数组**对象或可**迭代对象**。

`mapFn`  可选

如果指定了该参数，新数组中的每个元素会执行该回调函数。

`thisArg`  可选

可选参数，执行回调函数  `mapFn`  时  `this`  对象。

### 返回值

一个新的[`数组`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array)实例。

## 描述

### 从  `String`  生成数组

```js
Array.from('foo'); 
// [ "f", "o", "o" ]
```

### 从  `Set`  生成数组

```js
const set = new Set(['foo', 'bar', 'baz', 'foo']);
Array.from(set);
// [ "foo", "bar", "baz" ]
```

### 从  `Map`  生成数组

```js
const map = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(map);
// [[1, 2], [2, 4], [4, 8]]
const mapper = new Map([['1', 'a'], ['2', 'b']]);
Array.from(mapper.values());
// ['a', 'b'];
Array.from(mapper.keys());
// ['1', '2'];
```

### 从类数组对象（arguments）生成数组

```js
function f() {
  return Array.from(arguments);
}
f(1, 2, 3);
// [ 1, 2, 3 ]
```

### 在  `Array.from`  中使用箭头函数

```js
Array.from([1, 2, 3], x => x + x);
// [2, 4, 6]
Array.from({length: 5}, (v, i) => i);
// [0, 1, 2, 3, 4]
```

###  数组去重合并

```js
function combine(m,n){ 
    let arr = m.concat(n);  //没有去重复的新数组 
    return Array.from(new Set(arr));
} 

var m = [1, 2, 2], n = [2,3,3]; 
console.log(combine(m,n)); 
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkwMTEyNDk3XX0=
-->