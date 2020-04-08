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
这里就是第一个页面给第二个页面传递一个onPressCountryCodeItem 的回调函数.当第二个页面这个函数被触发的时候,会把所传递过来的value传递dao
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMjg4MjA3NTBdfQ==
-->