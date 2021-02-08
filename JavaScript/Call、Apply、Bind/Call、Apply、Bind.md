# Call、Apply、Bind

-   `call`：可以改变函数指向，第一个参数是要改变指向的对象，之后的参数形式是：`arg1,arg2...`
-   `apply`：基本同`call`,不同点在于第二个参数是一个数组`[arg1,arg2...]`
-   `bind`：改变`this`作用域会返回一个新函数，这个函数不会马上执行

## Call

`call()`方法使用一个指定的`this`值和单独给出的一个或多个参数来调用一个函数。

> 注意：该方法的语法和作用与`apply()`方法类似，只有一个区别，就是`call()`方法接收的参数是一个参数列表，而`apply()`方法接收的是一个包含多个参数的数组。

-   语法：`function.call(thisArg,arg1,arg2,...)`
    -   `thisArg`：可选的。在`function`函数运行时使用的`this`值。
    -   `arg1,arg2,...`：指定的参数列表

`call`的特性：

1. `obj.call(null)`，那么`this`指向`window`
2. `obj1.call(onj2)`，谁调用它，`this`指向谁
3. `call`可以传入多个参数，可以利用`arguments`这个字段来获取所有的参数。将`arguments`转换数组后，获取排除第一个参数外的其他参数
4. 设置一个变量，用完可以删除它

```JavaScript
Function.prototype.mycall = function (contetx) {
        if (typeof this !== 'function') {
            throw new TypeError('not funciton')
        }
        context = context || window
        context.fn = this
        let arg = [...arguments].slice(1)
        let result = context.fn(...arg)
        delete context.fn
        return result
    }
```

## Apply

`apply()`方法调用一个具有给定`this`值的函数，以及以一个数组（或类数组对象）的形式提供的参数。

-   语法：`function.apply(thisArg,[argsArray])`
    -   `thisArg`：必选的。在`function`函数运行时使用的`this`值
    -   `[argsArray]`：可选的。一个数组或者类数组对象，其中数组元素将作为单独的参数传给`func`函数

```JavaScript
    Function.prototype.myapply = function (context) {
        if (typeof this !== 'function') {
            throw new TypeError('not funciton')
        }
        context = context || window
        context.fn = this
        let result
        if (arguments[1]) {
            result = context.fn(...arguments[1])
        } else {
            result = context.fn()
        }
        delete context.fn
        return result
    }
```

## Bind

`bind()`方法创建一个新的函数，在`bind()`被调用时，这个新函数的`this`被指定为`bind()`的第一个参数，而其余参数将作为新函数的参数，供调用时使用。

-   语法：`function.bind(thisArg,arg1,arg2,...)`
    -   `thisArg`：调用绑定函数时作为`this`参数传递给目标函数的值
    -   `arg1,arg2,...`：当目标函数被调用时，被预置入绑定函数的参数列表中的参数
    -   返回值：一个原函数的拷贝，并拥有指定的`this`值和初始参数

```JavaScript
    Function.prototype.mybind = function (context) {
        if (typeof this !== 'function') {
            throw new TypeError('Error')
        }
        let _this = this
        let arg = [...arguments].slice(1)
        return function F() {
            // 处理函数使用new的情况
            if (this instanceof F) {
                return new _this(...arg, ...arguments)
            } else {
                return _this.apply(context, arg.concat(...arguments))
            }
        }
    }
```
