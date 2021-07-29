# 结构型

## 装饰器模式
* 作用
    
    允许向现有的类添加功能，但不影响现有类的功能和结构，类似于俄罗斯套娃。
* 场景

    1. api函数防抖、节流、弹窗确认。
* 实现
```
        //es7 写法
        // 包装函数
        const withLoading = (option = {
            message: '加载中...',
            isTransparent: false
        }) => {
            return function (target, name, descriptor) {
                const originFunc = descriptor.value
                // 弹窗加载
                const Ins = new Loading(option.message, option.isTransparent)
                descriptor.value = async function (...args) {
                    Ins.open()
                let res
                try {
                    res = await originFunc.apply(this, args)
                } catch (e) {
                    res = Promise.reject(e)
                }
                Ins.close()
                return res
                }
            }
        }
        // 利用@使用
        @withLoading({ message: '', isTransparent: true })
        pushEvent(options) {
            return api.post(
                `/kapi/app/wy_emergency_report/CqEventFollowUp`,
                options
            )
        }
```
## 外观模式
* 作用
    
    为复杂的子系统提供提议的接口,子系统可能毫无联系。
* 场景

    1. 撰写浏览器兼容判断.
    2. 代码库接口.
* 实现
```
    const appearance = {
        getEle = (id) => {
            return document.getElementById(id)
        },
        setCss = (id, key, value) => {
            document.getElementById(id).style[key] = value
        }
    }
```
## 适配器模式
* 作用
    让相互不兼容的对象或者类能够共同协作
* 场景
    1. 数据格式的转换及映射。
    2. 引入第三方库。
* 实现
```
    // 数据映射
    function adapter(originData) {
        return {
            name: originData[0],
            age: originData[1],
            job: originData[2]
        }
    }
```
## 代理模式
* 作用
    对象间无法直接通信，通过代理对象通信
* 场景
    1. vue3响应式原理-proxy
    2. 浏览器跨域代理
* 实现
```
    var boy = {
        sendflower(gift) {
            console.log('男孩送出花')
            friend.receive(gift)
        }
    }
    var friend = {
        receive(gift) {
            console.log(`朋友收到${gift}`)
            girl.receive(gift)
        }
    }
    var girl = {
        receive(gift) {
            console.log(`女孩收到${gift}`)
        }
    }
```
