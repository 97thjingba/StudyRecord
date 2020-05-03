首先需要的三个基本库
react-navigation
react-navigation-stack
react-navigation-tabs

快速建成一个项目一般需要这些：
```js
createSwitchNavigator  from react-navigation
createStackNavigator  from  react-navigation-stack
createBottomTabNavigator  from react-navigation-tabs
createAppContainer from react-navigation
```

Switch 一次只渲染一个页面.如其名
stackNavigator是最重要的一个创建路由的一个东西
BottomTabNavigator一般是底部的tab导航栏需要的东西


这里需要注意一点的是.需要把写好的路由给注册成一个组件.这样才能在
render里面进行渲染
```js
const RootNavigation = createAppContainer(typeOfNavigator)
```

```js
render() {
return (
<View  style={{ width:  '100%', height:  '100%' }}>
	<RootNavigation/>
</View>
);
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTMzMjYxNzYsLTEzOTk0MzA0NzVdfQ==
-->