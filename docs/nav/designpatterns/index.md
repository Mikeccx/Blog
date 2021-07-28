# 设计模式
* 某类问题，成熟的解决方案，能够合理的降低类的耦合，从而实现高内聚，低耦合。
## 六大原则
* Single Responsibility Principle：单一职责原则
* Open Closed Principle：开闭原则
* Liskov Substitution Principle：里氏替换原则
* Law of Demeter：迪米特法则
* Interface Segregation Principle：接口隔离原则
* Dependence Inversion Principle：依赖倒置原则

### 单一职责原则
* 一个类或者方法或模块尽可能只负责一类事。
* 拆分复杂的模块，将复杂的模块拆分成多个职责单一的组合。
### 开闭原则
* 对外扩展开放，对内修改封闭
* 增加需求时，扩展新代码，而非修改已有代码
### 里氏替换原则
* 子类能覆盖父类
### 迪米特法则
* 每个类尽量减少对其他类的依赖
### 接口隔离原则
* 保持接口的单一独立
### 依赖倒置原则
* 使用方只关注接口而不关注具体类的实现

