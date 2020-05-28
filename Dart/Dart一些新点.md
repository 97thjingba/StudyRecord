```dart
var c = ’‘’ 
d
d
d
‘’‘
print( c )
result:
d
d
d
```

```dart
== 可直接判断数值和类型是否相等。
和js的 == 不一样
Dart的 == 相当于js 的 ===
```

```dart
final 和 const
final 相当于 js 里面的 const
```

```dart
 var c = {
	"E":2,
	"dd": "se"
}
 print(c["E"]);
 result:
 2
```

```dart
	使用is来判断数据的类型
 var str = '1111';
 if(str is String){
 print('is string');
 }
```


```dart
b??=23 表示如果b为空的话，把23赋值给b
```

```dart
list.forEach((value){
	print(value); // 表示对list进行循环打印
})
```

```dart
// 自执行方法
((int n){
	print(n)
	print('我是自执行方法')
})(12) <- 表示传入的参数
```

```dart
class Person{
	Person(){
		// 默认构造函数,相当于react 里的生命周期里的constructor.
		// 当被实例化以后就会触发这个函数
	}
}
```

类里面的静态属性和静态方法设置了以后.可以直接通过类来访问，而不用去进行实例化.如果没有设置static的话,就需要进行对类先进行实例话 再来进行访问类里面的方法和属性
---


```dart
// 联缀操作
Person p1 = Person('张三',20)
p1.printInfo()

p1..name="李四"
  ..age=22
  ..printInfo();
 // 表示修改p1对象里面的name和age然后执行printInfo函数

```





<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NTY4MjAyMjAsMTE3Nzk0Nzk1MywtNz
A2NTExOTAzLDk3OTM5OTIzOSwxOTU1NTE4NTg1LC01MTg1OTUw
ODMsLTE3MDE5Nzk2MDUsMzI4NTM3MDIyLDE2MjY0MzYzNjZdfQ
==
-->