1: 使用useRef 来进行判断
```js
const usePrevProps = (value) => {
	// useRef会在组件整个生命周期只执行一次,并且返回一个可变的对象.{ current：‘’} 
	const ref = useRef()
	useEffect(()=>{
		ref.current = value
	},[value])
	// 会一直记录这个值
	return ref.current
}
```

2. 使用Es6的set 对象来进行判断
```js
const setObject = new Set()
const callBack = useCallBack(()=>{
	console.log('a')
},[]) 
setObject.add(callBack)
// 判断setObject的sizesh
return <div> {setObject.size}</div>
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNTM2MTA3NTZdfQ==
-->