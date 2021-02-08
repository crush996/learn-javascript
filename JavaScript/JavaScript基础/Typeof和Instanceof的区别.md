# typeof 和 instanceof 的区别

-   `typeof：`对某一个变量类型的检测，基本除了`null`之外，都能正常的显示为对应的类型，引用类型除了函数会显示为`function`,其他都显示为`object`。
-   `instanceof：`主要用于检测某个构造函数的原型对象在不在某个对象的原型链上。

`typeof`会对`null`显示错误，`typeof null`输出的为`object`,因为 JavaScript 早起版本是 32 位系统，为了性能考虑使用低位存储变量的类型信息，`000` 开头代表是对象然而`null`表示为全零，所以它错误判断为`object。`

另外还有`Object.prototype.toString.call()`进行
