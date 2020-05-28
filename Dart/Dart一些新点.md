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

`



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY1NjA0OTk3LDk3OTM5OTIzOSwxOTU1NT
E4NTg1LC01MTg1OTUwODMsLTE3MDE5Nzk2MDUsMzI4NTM3MDIy
LDE2MjY0MzYzNjZdfQ==
-->