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
import React, { useState, useCallback } from 'react';
 
const set = new Set();
 
export default function Callback() {
    const [count, setCount] = useState(1);
    const [val, setVal] = useState('');
 
    const callback = useCallback(() => {
        console.log(count);
    }, [count]);
    set.add(callback);
 
 
    return <div>
        <h4>{count}</h4>
        <h4>{set.size}</h4>
        <div>
            <button onClick={() => setCount(count + 1)}>+</button>
            <input value={val} onChange={event => setVal(event.target.value)}/>
        </div>
    </div>;
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNTIxMzc2MjFdfQ==
-->