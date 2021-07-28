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
## 代理模式