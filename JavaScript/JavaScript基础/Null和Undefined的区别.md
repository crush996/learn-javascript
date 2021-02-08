## Null 和 Undefined 的区别

根据使用场景细分如下：

-   `null:`

    1. `Number(null)`得到的为`0`。
    2. 作为函数的参数，表示该函数的参数不是对象。
    3. 作为对象原型链的终点。 `Object.propotype.__proto__===null`.

-   `undefined:`
    1. `Number(undefined)`得到的为`NAN`。
    2. 变量被声明，但未赋值，等于`undefined`。
    3. 调用函数时，传入的对象为空，也等于`undefined`。
    4. 对象没有赋值，这个属性的值为`undefined`。
    5. 函数没有返回值，默认返会`undefined`。
