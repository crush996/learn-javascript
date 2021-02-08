# setTimeout 实现 setInterval

```JavaScript
const say=()=>{
    setTimeout(say, 200);
};
setTimeout(say, 200);
```

清除这个定时器

```JavaScript
let i=0;
const timelist=[];

const say=()=>{
    console.log(i++);
    timeList.push(setTimeout(say, 200));
}
setTimeout(say, 200);

setTimeout=(()=>{
    for(let i=0;i<timelist.length;i++){
        clearTimeout(timeList[i]);
    }
},1000);

```
