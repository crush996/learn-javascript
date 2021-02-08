# This

-   `this`永远指向最后调用它的那个对象。
-   普通函数中`this`的指向，是`this`的执行时的上下文。
-   箭头函数中`this`的指向，是`this`的定义时的上下文。
-   `this`是和执行上下文绑定的，也就是说每个执行上下文中都有一个`this`。

执行上下文分为：

-   全局执行上下文
-   函数执行上下文
-   eval 执行上下文

## 全局执行上下文中的 this

全局执行上下文中的`this`是指向 Window 的。

## 函数执行上下文中的 this

### 通过 call/apply/bind 来改变 this

```JavaScript
this.myName = '张三';
let foo = function() {
  this.myName = '李四';
}
foo();
console.log(window.myName); // 李四
console.log(foo.myName); // undefined
```

通过`call`绑定：

```JavaScript
this.myName = '张三';
let foo = function() {
  this.myName = '李四';
}
foo.call(foo);
console.log(window.myName); // 张三
console.log(foo.myName); // 李四
```

通过`bind`绑定：

```JavaScript
this.myName = '张三';
let foo = function() {
  this.myName = '李四';
}
foo.bind(foo);
console.log(window.myName); // 张三
console.log(foo.myName); // undefined
```

通过`apply`绑定：

```JavaScript
this.myName = '张三';
let foo = function() {
  this.myName = '李四';
}
foo.apply(foo);
console.log(window.myName); // 张三
console.log(foo.myName); // 李四
```

### 通过对象调用方法设置

使用对象来调用其内部的一个方法，该方法的`this`是指向对象本身的。

### 通过构造函数中设置

## this 设计缺陷和应对方案

### 嵌套函数中的 this 不会从外层函数中继承

```JavaScript
var myObj = {
  myName: "张三",
  showThis: function(){
    console.log(this.myName); // 张三
// 解决办法一
    let that = this;
    function bar(){
      console.log(this.myName); // undefined
      console.log(that.myName); // 张三
    }
    bar();
  },
};
myObj.showThis();

//解决方法二  es6箭头函数
var myObj = {
  myName: "张三",
  showThis: function(){
    console.log(this.myName); // 张三
    const bar = () => {
      console.log(this.myName); // 张三
    }
    bar();
  },
};
myObj.showThis();
```

这是因为 ES6 中的箭头函数并不会创建其自身的执行上下文，所以箭头函数中的 `this` 取决于它的外部函数，即谁调用它 `this` 就继承自谁。

### 普通函数中 this 指向全局对象 window

在实际工作中，我们并不希望函数执行上下文中的`this`默认指向全局对象，因为这样会打破数据的边界，造成一些误操作。  
如果要让函数执行上下文中的`this`指向某个对象，最好使用`call`方法来显示调用。  
这个问题可以通过设置 JavaScript 的 **严格模式** 来解决。在严格模式下，默认执行一个函数，函数执行上下文中的`this`值是`undefined`，就可以解决上面的问题。
