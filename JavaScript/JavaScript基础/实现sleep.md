# 实现 sleep

实现`1000`毫秒之后执行其他内容：

```JavaScript
const sleep= time=>{
    return new Promise((resolve,reject)=>{
        setTimeout(()=>{
            resolve(time)
        },time);
    });
};

sleep(1000).then((res)=>{
    console.log(res);
});
```
