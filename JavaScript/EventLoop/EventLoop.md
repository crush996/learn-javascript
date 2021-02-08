# Event Loop

## 单线程和多线程

JavaScript 是一个单线程的语言。  
单线程在程序执行的时候，所走的程序路径按照连续顺序排下来，前面的必须处理好，后面的才会执行。  
以 Chrome 浏览器为例，打开一个 tab 时，就是创建一个进程。  
一个进程中可以有多个线程，比如渲染线程、JS 引擎线程、HTTP 请求线程等等。  
当你发起一个请求时，其实就是创建了一个线程，当请求结束后，该线程可能就会被销毁。  
**·浏览器内核是怎样的**  
浏览器内核是多线程的，在内核控制下个线程相互配合以保持同步，一个浏览器通常由一下常驻线程组成：

1. GUI 渲染线程：解析 HTML、CSS 等。在 JavaScript 引擎线程运行脚步期间，GUI 渲染线程处于挂起状态，也就是被“冻结”了。
2. JavaScript 引擎线程：负责处理 JavaScript 脚本。
3. 定时触发线程：`setTimeout`、`setInterval`等。事件触发线程会将计数完毕后的事件加入到任务队列的尾部，等待 JS 引擎线程执行。
4. 事件触发线程：负责将准备好的事件交给 JS 引擎执行。
5. 异步`http`请求线程：负责执行异步请求之类函数的线程，例如：`Promise.then()`、ajax 等。

# Event Loop

-   为什么会有 Event Loop  
    JavaScript 线程一次只能做一件事。如果碰到需要等待的程序，如何？  
    所以，JavaScript 为了协调事件、用户交互、脚本、渲染、网洛等，就搞出来一个 **事件循环(Event Loop)**。
-   什么是 Event Loop?
    JavaScript 从`script`开始读取，然后不断循环，从”任务队列”中读取执行事件的过程，就是 \_\_事件循环(Event Loop)。

## Event Loop 执行过程

**Event Loop** 执行过程如下：

1. 一开始整个脚本`script`作为一个宏任务执行
2. 执行过程中，**同步代码** 直接执行，**宏任务** 进入宏任务队列，**微任务** 进入微任务队列。
3. 当前宏任务执行完出队，检查微任务队列，有则依次执行，直到全部执行完毕。
4. 执行浏览器`UI`线程的渲染工作。
5. 检查是否有`Web Worker`任务，有则执行。
6. 执行完本轮的宏任务，回到步骤 2，依次循环，知道宏任务和微任务队列为空。

事件循环中的异步队列有两种：宏任务队列（MacroTask）和微任务队列（MicrTask）。

> Web Worker 是运行在后台的 JS,独立于其他脚本，不会影响页面的性能。

**宏任务队列可以有多个，微任务队列只有一个。**  
**宏任务** 包括：

-   `script`
-   `setTimeout`
-   `setInterval`
-   `setImmediate`
-   `I/O`
-   `UI rendering`

**微任务** 包括：

-   `MutationObserver`
-   `Promise.then()/catch()`
-   以`Promise`为基础开发的其他技术，例如：`fetch API`
-   V8 的垃圾回收过程
-   Node 独有的 `process.nextTick`