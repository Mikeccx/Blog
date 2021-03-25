# 如何模拟一个new操作符？
```
    function foo (name) {
        this.name = name
    }
    var a = new fo('Mike')
    function New(fn, args) {
        const newObj = {}
        newObj.__proto__ = fn.prototype
        for (const key in args) {
            newObj[key] = args[key]
        }
        return newObj
    }
    var b = New(fo, {name: 'Jack'})
```