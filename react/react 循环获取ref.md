#### 今天遇到一个小坑.记录一下

```js
const E = [1,2,3]
E.map((item)=>{
	<XXX 
		ref={(ref)=> this.xxx = ref}	
   />
})
 ```
 
 开发的时候看了半个小时实在没有找到怎么回事
当我去调用this.xxx.update()方法的时候,他只会对循环列表里的最后一个ref进行函数调用

解决方式是
使用this.refs= [] 或者this.refs = {};

```js
E.map((item)=>{
		<XXX ref={refs=> this.ref[i]= refs} 
}
)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjM1OTM1NDQwXX0=
-->