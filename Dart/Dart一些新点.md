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
就像 react的 b || 23
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

```dart
子类调用父类的方法的时候.使用super关键字调用
调用父类的属性的时候.直接使用this关键字来调用
```
```dart

```





<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMTM0MDQ5NjQsLTY4Njk0OTg5MiwxMT
E4MTI1NDM5LC0xMjc1NzYxNjE5LC0xODU2ODIwMjIwLDExNzc5
NDc5NTMsLTcwNjUxMTkwMyw5NzkzOTkyMzksMTk1NTUxODU4NS
wtNTE4NTk1MDgzLC0xNzAxOTc5NjA1LDMyODUzNzAyMiwxNjI2
NDM2MzY2XX0=
-->