# 行为型

## 观察者模式/发布订阅模式
### 观察者模式
* 作用

    定义一种一对多的关系，解决多对象的依赖关系
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