# Promise

## 浅思

JavaScript 里的异步方案的演进时，是用下面这种顺序：  
`callback -> promise -> generator -> async/await`

## Promise 初探

`Promise`是一个构造函数。  
回调地狱带来的负面作用：

-   代码臃肿
-   可读性差
-   耦合度过高，可维护性差
-   代码复用性差
-   容易滋生 bug
-   只能在回调里处理异常

## Promise 基础

### new Promise()

1. `Promise`对象是一个构造函数，用来生成`Promise`实例，`new Promise()`.
2. `new Promise()` 传入一个函数，这个函数可以带 2 个参数：`resolve`和`reject`.
3. `resolve`的作用是将`Promise`对象的状态从“未完成”变为“成功”(`pending -> resolved`)
4. `reject`的作用是将`Promise`对象的状态从“未完成”变为“失败”(`pending -> rejected`)
5. 在没有执行`resolve`和`reject`之前，它们还是`pending`的。

### Promise 状态

`Promise`有 3 种状态：`pending`、`resolve`、`reject`。

1. 初始状态：`pending`
2. 成功状态：`resolve`
3. 失败状态：`reject`

如果你在 `new Promise` 中用了` resolve()`，那么它就会走 `.then()`；
如果你用的是 `reject()`，那么它就走`.catch()`。
