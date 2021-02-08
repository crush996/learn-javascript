# JSONP

**基本原理：** 利用`script`标签的`src`没有跨域限制来完成跨域目的
**执行过程：**

1. 前端定义一个解析函数：`jsonpCallBack = function (res) {}`
2. 通过`params`的形式包装`script`标签的请求参数，并且声明执行函数，如：`cb = jsonpCallBack`
3. 后端获取前端生命的执行函数（`jsonpCallBack`），并且带上参数且调用函数的方式传递给前端
4. 前端再`script`标签返回资源的时候就会执行`jsonpCallBack`并通过回调函数的方式拿到数据

**优缺点：**

1. 【缺点】只能进行`GET`请求
2. 【优点】兼容性好，在一些古老的浏览器中都可以运行

## 基本实现

-   1.前端部分：

```Html
<script type='text/javascript'>
  window.jsonpCallBack = function(res) {
    console.log(res);
  }
</script>
<script src='http://localhost:8080/api/jsonp?id=1&cb=jsonpCallBack' type='text/javascript'></script>
```

1. 创建一个`jsonpCallBack`函数，但是还没有调用
2. 加载`src`资源，调用 `localhost:8080` 端口的` API：api/jsonp`，传递的参数是 `id = 1` 以及 `cb = jsonpCallBack`

-   2.后端部分

```JavaScript
const Koa = require('koa');
const app = new Koa();
const items = [{ id: 1, title: 'title1' }, { id: 2, title: 'title2' }]

app.use(async (ctx, next) => {
  if (ctx.path === '/api/jsonp') {
    const { cb, id } = ctx.query;
    const title = items.find(item => item.id == id)['title']
    ctx.body = `${cb}(${JSON.stringify({title})})`;
    return;
  }
})
console.log('listen 8080...')
app.listen(8080);
```

1. 解析`ctx.query`，将`id`和`cd`获取到
2. 查找`title`
3. 返回一个字符串，该字符串调用`cb`方法，并将`title`转成字符串，返回到内容`ctx.body`中

-   3.前端部分

这时候前端接收到 `Node.js` 的返回，直接调用了 `cb(title)`，方法，最终执行了它的回调，从而执行：

```JavaScript
window.jsonpCallBack = function(res) {
  console.log(res);
}
```

## 封装 JSONP

```JavaScript
function jsonp({
    url,
    params={},
    callbackKey='cb',
    callback,
}) {
    // 定义本地的唯一 callBackId，防止多次调用的时候出问题
  JSONP.callBackId = JSONP.callBackId || 1; // 默认为 1

  // 拿到这个 id
  const callBackId = JSONP.callBackId;

  // 将要执行的回调假如到 JSONP 对象中，避免污染 window
  JSONP.callbacks = JSONP.callbacks || [];
  JSONP.callbacks[callBackId] = callback;

  // 把这个名称加入到参数中：`cb = JSONP.callbacks[1]`
  params[callbackKey] = `JSONP.callbacks[${callBackId}]`;

  // 组合 params：'id=1&cb=JSONP.callbacks[1]'
  const paramString = Object.keys(params).map((key) => `${key}=${params[key]}`);

  // 动态创建 script 标签
  const script = document.createElement("script");
  script.setAttribute("src", `${url}?${paramString}`);
  document.body.appendChild(script);

  // id 自增，保证唯一
  JSONP.callBackId++;
}
```
