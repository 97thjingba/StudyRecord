关于navigation里面传递回调函数
例子：
```js
_onPressDropDown = () => {
const { navigation } = this.props;
	navigation.navigate('ChooseCountryCode', {
	onPressCountryCodeItem: (value) => {
	this.setState({ countryCode:  value });},
});
}
```
这里就是第一个页面给第二个页面传递一个onPressCountryCodeItem 的回调函数.当第二个页面这个函数被触发的时候,会把所传递过来的value传递到第一个页面拿来使用

```js
_onPress = (code) => {
	const { navigation: { goBack, state } } = this.props;
	state.params.onPressCountryCodeItem(code);
	goBack();
}
```
这是第二个页面触发的函数,首先需要获取到goback,以及state.
goBack是直接返回上一页.state.params里就有我们之前从第一个页面传递过来的回调函数.当被触发时,把code的值传递回第一个页面然后在第一个页面进行相关操作.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNzc4OTExNThdfQ==
-->