1: 类 class .看class 本质 只是一个语法糖

2: 模块化. 导入导出import and export

3: 箭头函数. =>是function的简写.箭头函数与包围它的代码共享同一个this.

4: 函数参数默认值
ES6支持在定义函数的时候为其设置默认值：
```
function foo(height = 50, color = 'red')
{
    // ...
}

复制代码
```
不使用默认值
```
function foo(height, color)
{
    var height = height || 50;
    var color = color || 'red';
    //...
}
```

5: 模版字符串 ${} 

6: 解构赋值 const {ddd} = this.props   ==  this.props.ddd
可以一次性取出多个值出来

7: 延展操作符

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4Mjg5NDU0MzVdfQ==
-->