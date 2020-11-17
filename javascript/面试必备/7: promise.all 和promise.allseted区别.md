### Promise.all 缺陷

都知道 `Promise.all` 具有并发执行异步任务的能力。但它的最大问题就是如果其中某个任务出现异常(`reject`)，所有任务都会挂掉，`Promise` 直接进入 `reject` 状态。

想象这个场景：你的页面有三个区域，分别对应三个独立的接口数据，使用 `Promise.all` 来并发三个接口，如果其中任意一个接口服务异常，状态是 reject,这会导致页面中该三个区域数据全都无法渲染出来

### Promise.allSettled

当我们处理多个`promise`时，尤其是当它们相互依赖时，记录每个事件在调试中发生的错误可能很有用。使用`Promise.allSettled`，它会创建一个新的`promise`，在所有`promise`完成后返回一个包含每个`promise`结果的数组

 
 ### Promise.allSettled 的优势

`Promise.allSettled` 跟 `Promise.all` 类似 都是进行并发请求，但是，我们在上面的两个例子中，显然是已经看到了他们的一些区别，在使用 `Promise.all`进行并发请求的时候，只要有一个请求出现问题（异常），所有的请求正常的也都不能拿到数据，但是在我们的业务的开发中，我们需要保障我们业务的最大的可访问性，就是在我们执行并发任务中，不管我这个并发任务中的一任何个任务是正常还是异常，我们都需要拿到返回的对应的状态，在ES11中 `Promise.allSettled` 就为我们解决了这个问题，它和 `Promise.all` 类似,参数接受一个Promise的数组,返回一个新的Promise,也就是说当Promise全部处理完成后,我们可以拿到每个Promise的状态, 而不管是否处理成功。我们可以在 `then`里面通过 `filter`来过滤出想要的业务逻辑结果，这样就解决了`Promise.all` 的缺陷。

 ```

``
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzY4MzI2NjRdfQ==
-->