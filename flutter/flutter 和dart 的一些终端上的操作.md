我觉得我以后肯定需要用的上：

这个是同时更新sdk包和依赖包的
```shell
flutter upgrade // 更新flutter 有时候出现了莫名其妙的错误然后更新一下就好了
```
--- 

如果您修改了`pubspec.yaml`文件，或者只想更新应用依赖的包(不包括Flutter SDK)，请使用以下命令：

-   `flutter packages get`获取`pubspec.yaml`文件中列出的所有依赖包
-   `flutter packages upgrade`  获取`pubspec.yaml`文件中列出的所有依赖包的最新版本


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MjMwNDgxODhdfQ==
-->