# 创建型

## 单例模式
* 作用
    
    只允许对象实例化一次，节省内存，同时避免实例化太多相同作用的实例.
* 场景

    1. 全局弹窗，全局提示。
    2. 管控全局变量，例如，vue初始化实例，vuex实例。
* 实现
```
        class Single {
            constructor() { 
                if (!Single.instance) {
                    Single.instance = this
                } else {
                    return Single.instance
                }
            }
        }
        const a = new Single()
        const b = new Single()
        a === b // true
```