# 创建型
## 工厂模式
* 作用
    通过工厂对象，创建某一类对象实例。封装某一大类，通过参数，实例化其子类。
* 场景
    1. 方法库等实例化。
* 实现
```
    // 足球类
    class soccerBall{
        constructor(name) {
            this.ballName = name
        }
        play() {
            console.log(`play ${this.ballName}`)
        }
    }
    // 蓝球类
    class basketBall{
        constructor(name) {
            this.ballName = name
        }
        play() {
            console.log(`play ${this.ballName}`)
        }
    }
    // 球类工厂
    class ballFactory{
        constructor(type) {
            switch(type) {
                case 'soccerBall' : return new soccerBall('足球');break;
                case 'basketBall' : return new basketBall('篮球');break;
                default: break;
            }
        }
    }

    var ball = new ballFactory('soccerBall')
```
## 建设者模式
* 作用
    
    构建一个复杂对象，通过多层级变现。
* 场景
    暂时没想到～
* 实现
```
    // 职业类
    class skill {
        constructor(skill) {
            this.skill = skill
        }
    }
    // 人类
    class Human {
        constructor(name) {
            this.name = name
            this.skill = new skill('font-developer)
        }
    }
    const MrC = new Human('cx')
```
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