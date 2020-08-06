`toLocaleUpperCase()` 方法根据本地主机语言环境把字符串转换为大写格式，并返回转换后的字符串

```js
const city = 'istanbul';

console.log(city.toLocaleUpperCase('en-US'));
// expected output: "ISTANBUL"

console.log(city.toLocaleUpperCase('TR'));
// expected output: "İSTANBUL"
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc2NDY2MTU4MF19
-->