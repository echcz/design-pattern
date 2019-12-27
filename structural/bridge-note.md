# 桥接模式 Bridge Partten

桥接模式(Bridge Partten)用于将抽象部分与实现部分脱耦，使它们可以独立的变化

## 代码与图示

``` java
interface Implementor {
    void operationImpl()
}
class Implementor implements Implementor {
    public void operationImpl() { /*...*/ }
}
abstract class Abstraction {
    private Implementor implementor;
    public Abstraction(Implementor implementor) {
        this.implementor = implementor;
    }
    public void operation() {
        implementor.operationImpl();
    }
}
class RefinedAbstraction extends Abstraction {
    public RefinedAbstraction(Implementor implementor) {
        super(implementor);
    }
    public void otherOperation() { /*...*/ }
}
```

* [桥接模式类图](./bridge-class.puml)
* [桥接模式时序图](./bridge-timing.puml)


## 分析

* 抽象部分: 将对象的共同性质抽取出来的部分
* 实现部分: 根据抽象部分给出的具体实现
* 脱耦: 在一个系统的抽象部分和实现部分之间使用弱关联代替强关联，即使用关联关系(组合或者聚合关系)而不是继承关系，从而使两者可以相对独立地变化
