# JavaScript 变量

## var/let/const

-   `var:`

1. `var`可以重复声明
2. 作用域：全局作用域和函数作用域
3. 会进行预解析

-   `let`

1. 统一作用域下不能重复声明
2. 作用域：全局作用域和块级作用域`{}`
3. 不进行预解析

-   `let`和`var`比较

1. `var`声明的变量只能是全局的或整个函数块
2. `let`允许声明一个在作用域限制在块级的变量、语句或者表达式（块级作用域）
3. `let`不会被预解析
4. `let`存在暂时性死区
5. `let`不能重复声明

-   `const:`

1. `let`有的它都有
2. 初始化必须赋值
3. 赋值后不允许改动

## 暂时性死区

只要块级作用域内存在`let/const`命令，它所声明的变量就绑定这个区域，不再受外部的影响。  
在代码块内，使用`let/const`声明变量之前，该变量都是不可用的，所以叫 “暂时性死区”。

## 函数作用域和块级作用域

**·函数作用域：** 在 JavaScript 中定义一个函数，函数内部的变量只能通过函数内部访问，同时可以修改和影响外部变量。  
**·块级作用域：** 变量在离开定义的块级代码后立即被回收，存在暂时性死区的特性。

## 判断变量

JavaScript 判断变量的方式有：

1. `typeof(variable)`
2. `variable instanceof Array`
3. `variable.constructor = Array`
4. `Object.prototype.toString.call(variable)`

### typeof

`typeof`能区分的有：

-   `number`
-   `string`
-   `boolean`
-   `undefined`
-   `function`
-   `symbol`

检测其他类型的时候，都返回 object，不太稳定。

### instanceof

`instanceof`判断原型链指向。

```JavaScript
function getType(obj){
  let type  = typeof obj;
  if (type !== "object") {    // 先进行typeof判断，如果是基础数据类型，直接返回
    return type;
  }
  // 对于typeof返回结果是object的，再进行如下的判断，正则返回结果
  return Object.prototype.toString.call(obj).replace(/^\[object (\S+)\]$/, '$1');  // 注意正则中间有个空格
}
```
