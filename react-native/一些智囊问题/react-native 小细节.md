1: 
在写层级render的时候.如果说上一层级需要被下一层级隐藏. 但是他们同时属于一个render函数里的时候.那么就需要把 最后一层的组件放在上一层组件的后面进行render. 比如
A组件是一个按钮组件.点击一下需要弹出一个B组件. 但是这个B 组件刚好会挡住这个A组件. 刚好又同时处在同一个render函数里面,这个时候就需要这样操作

```js
render(){
	<View>
		<A />
		<B />
	</View>
}
```
顺序很重要.

---
2: 
TouchableOpacity，TouchableWithoutFeedback，TouchableHighlight
除了第一个不需要子组件以外。另外的两个都需要一个子组件放在里面

---
3: 
img.png   
img@2x.png
img@3x.png
如果图片的分辨率不符合倍数关系的话，react-native 会报错
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU4ODA1NTM4MF19
-->