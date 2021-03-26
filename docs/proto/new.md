# 如何模拟一个new操作符？
```
    function foo (name) {
        this.name = name
    }
    var a = new fo('Mike')
    function _new(fn) {
        // 新建一个新对象
        const newObj = {}
        // 绑定原型
        newObj.__proto__ = fn.prototype
        fn.apply(newObj, [].slice.call(arguments, 1))
        return resObj
    }
    var b = New(fo, 'jack', 'rose')
```