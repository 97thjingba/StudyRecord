`toLocaleLowerCase()`方法根据任何指定区域语言环境设置的大小写映射，返回调用字符串被转换为小写的格式

### 参数

`locale` 可选

参数 `locale` 指明要转换成小写格式的特定语言区域。 如果以一个数组 [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array "REDIRECT Array")形式给出多个locales, 最合适的地区将被选出来应用（参见[best available locale](https://tc39.github.io/ecma402/#sec-bestavailablelocale)）。默认的locale是主机环境的当前区域(locale)设置。

### 返回值

根据任何特定于语言环境的案例映射规则将被调用字串转换成小写格式的一个新字符串。
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkxODU1MTkyNl19
-->