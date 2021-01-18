```js
typeof null // "object"
复制代码
```

`JavaScript` 中的值是由一个表示类型的标签和实际数据值表示的。第一版的 `JavaScript` 是用 32 位比特来存储值的，且是通过值的低 1 位或 3 位来识别类型的，对象的类型标签是 000。如下

-   1：整型（int）
-   000：引用类型（object）
-   010：双精度浮点型（double）
-   100：字符串（string）
-   110：布尔型（boolean）

但有两个特殊值：

-   undefined，用整数−2^30（负2的30次方，不在整型的范围内）
-   null，机器码空指针（C/C++ 宏定义），低三位也是000

由于 `null` 代表的是空指针（低三位也是 `000` `），因此，null` 的类型标签是 `000`，`typeof null` 也因此返回 "object"。

这个算是 `JavaScript` 设计的一个错误，但是也没法修改，毕竟修改的话，会影响目前现有的代码
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk4MTE3MDI3MF19
-->