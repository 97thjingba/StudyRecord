useEffect 注意点：

 1.  传递给useEffect的函数会在浏览器完成布局与绘制之后，**在一个延迟事件中被调用**，
 2. 虽然useEffect绘制浏览器延迟后执行，但会保证在任何新的渲染前执行。在开始新的更新前，react总会先清除上一轮渲染的effect

| useEffect  | useLayoutEffect |
|--|--|
| 页面渲染后执行 |同步执行，会阻塞页面渲染  |
|不会阻塞渲染|会阻塞渲染，会影响到渲染的操作尽量使用，避免出现闪烁问题||


<!--stackedit_data:
eyJoaXN0b3J5IjpbOTkxMTgzNDM4LC03ODk4NzU4NDddfQ==
-->