```js
const usePrevProps = (value) => {
	// useRef会在组件整个生命周期只执行一次,并且返回一个可变的对象.{ current：‘’} 
	const ref = useRef()
	useEffect(()=>{
		ref.current = value
	},[value])
	// 
	return ref.current
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2OTEwNDQxMl19
-->