# 如何模拟一个new操作符？
```
    function foo (name) {
        this.name = name
    }
    var a = new fo('Mike')
    /**
    *   1.以 Object.prototype 为原型创建一个新对象；
    *   2.以新对象为 this，执行函数的[[call]]；
    *   3.如果[[call]]的返回值是对象，那么，返回这个对象，否则返回第一步创建的新对象。
    **/
    function _new(fn) {
        const newObj = Object.create(fn.prototype)
        newObj.__proto__ = fn.prototype
        var resObj = fn.apply(newObj, [].slice.call(arguments, 1))
        return typeof resObj === 'Object' ? resObj : newObj
    }
    var b = New(fo, 'jack', 'rose')
```