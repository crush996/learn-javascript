# New

-   `new()`
    -   首先创建一个空对象 `tempObj={}`
    -   接着调用`Foo.apply`方法，将`tempObj`作为`apply`方法的参数，这样当`Foo`的执行上下创建时，它的`this`就指向`tempObj`对象
    -   然后执行`Foo`函数，此时的`Foo`函数执行上下文中的`this`指向了`tempObj`对象
    -   最后返回`tempObj`对象
