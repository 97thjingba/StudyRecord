
### PanResponder

PanResponder 是 React Native 实现的一套手势相应方法

### 基本用法

这是官方给的例子.但是由于componentWillMount 将在以后被移除.所以把这个东西最好放到constructor里面,但是它并没有在constructor直接调用this.setState(),而是相当于提前挂载了一个这个东西.放在了view里面去调用的.

```jsx
  componentWillMount: function() {
    this._panResponder = PanResponder.create({
      // 要求成为响应者：
      onStartShouldSetPanResponder: (evt, gestureState) => true,
      onStartShouldSetPanResponderCapture: (evt, gestureState) => true,
      onMoveShouldSetPanResponder: (evt, gestureState) => true,
      onMoveShouldSetPanResponderCapture: (evt, gestureState) => true,

```

},

render:  function()  {  
return  (  
<View  {…this._panResponder.panHandlers}  />  
);  
},  

这个东西可以放在任何的一个view里.任何的一个view都可以作为一个手势系统.只不过我们使用的时候是没有被激活的。

有一些注意的点:在使用的时候我踩下的坑  
**不要把这个和TouchOpacity 等一起使用.PanResponder事件会被这些组件给阻塞**

参考：[官方文档](https://reactnative.cn/docs/0.41/panresponder/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwODY1MDEwNzFdfQ==
-->