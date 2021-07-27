# 行为型

## 观察者模式/发布订阅模式
### 观察者模式
* 作用

    解决多模块或者对象间的耦合，互不影响～
* 写法
    ```
    // 被观察者
    class Subject {
        constructor(name) {
            this.name = name || '无情的被观察者'
            this.list = []
        }
        addObs(ob) {
            this.list.push(ob)
        }
        // 更新发布
        publish() {
            this.list.forEach( o => o.update(this))
        }
    }

    // 观察者
    class Observer {
        constructor(name) {
            // 观察者名字
            this.name = name || '冷漠的机器人'
            
        }
        update(subject) {
            console.error(`${subject.name}改变了被观察者${this.name}发现了`)
        }
    }

    // 实例化被观察者
    var ob1 = new Subject('机器人一号')
    var ob2 = new Subject('机器人二号')

    // 实例化观察者
    var god = new Observer('god')
    // 被观察
    ob1.addObs(god)
    // 发布
    ob1.publish() // console:机器人一号改变了被观察者god发现了
    ```
* 实用场景
    1. vue双向绑定，劫持对象，get时，被观察，set时，发布.
    2. 给对象或者类预留扩展口子，可以动态拓展.
### 发布订阅模式
* 作用
    通过事件调度中心，解耦对象于对象的依赖关系
* 用法
    ```
       // 事件调度中心
        class Event {
            constructor() {
                this.list = {}
            }
            // 监听
            on(type, fn) {
                if(!this?.list[type]?.length) {
                    this.list[type] = []
                }
                this.list[type].push(fn)
            }
            // 发布
            emit(type, args) {
                if (!this?.list[type]?.length) {
                    return
                }
                this.list[type].forEach((f) => {
                    f.apply(this, [args])
                })
            }
        }

        // 实例化事件中心
        var event = new Event()
        // 订阅test类型
        event.on('test', (text) => {
            console.log(text)
        })
        // 发布test类型
        event.emit('test', '发出参数')
    ```
## 策略模式
* 作用

    解决多重if-else嵌套耦合问题
* 写法
```
    // 表单数据
    const data = {
        info: ''
    }
    // 策略类
    const reportStrategy = {
        /**
        * 判断是否为空？
        * @param {any} val 值
        * @param {string} errorMsg 报错信息
        * @returns string | undeifined
        */
        empty(val, errorMsg) {
            if (Array.isArray(val)) {
                if (val.length === 0) {
                    return errorMsg
                }
            } else {
                if (val !== 0 && !val) {
                    return errorMsg
                }
            }
        },
        /**
        * 传入一个数组，判断至少一个值不能为空
        * @param {Array} val
        * @param {string} errorMsg
        */
        atLeastOne(val, errorMsg) {
            if (!val.some(v => v !== 0 && v)) {
                return errorMsg
            }
        }
    }

    // 验证类
    class Validator {
        constructor(strategys) {
            this.rules = []
            this.strategys = strategys
        }
        /**
        * 添加规则
        * @param {any} val 需要验证的值
        * @param {string} ruleName 规则名
        * @param {string} errMsg 验证提示
        */
        add(val, ruleName, errMsg) {
            this.rules.push({
                val: val,
                ruleName: ruleName,
                errMsg: errMsg
            })
        }
        /**
        * 验证规则
        */
        check() {
            for (const item of this.rules) {
                const { val, ruleName, errMsg } = item
                const res = this.strategys[ruleName](val, errMsg)
                if (res) {
                    Toast(res)
                    return false
                }
            }
            return true
        }
    }

    // 初始化实例
    const validator = new Validator(reportStrategy)
    validator.add(
        data.info,
        'empty',
        '信息不能为空'
    )
    validator.check() // false
```
* 实用场景

    1. 提交表单。
    2. 多重条件判断