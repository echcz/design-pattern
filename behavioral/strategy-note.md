# 策略模式 StrategyPattern

策略模式(Strategy Pattern)定义一系列算法(策略)，并把它们一个个封装为对象，使它们可以互换，从厕使它们可以独立于使用它们的客户而变化

## 代码与图示

``` java
class Context {
    private Strategy strategy;
    public void setStrategy(Strategy strategy) {
        this.strategy = strategy;
    }
    public void execute() {
        strategy.execute();
    }
}
interface Strategy {
    void execute();
}
class ConStrategyA implements Strategy { /*...*/ }
class ConStrategyB implements Strategy { /*...*/ }
class Main {
    public static void main(String[] args) {
        Context context = new Context();
        context.setStrategy(new ConStrategyA());
        context.execute();
        context.setStrategy(new ConstrategyB());
        context.execute();
    }
}
```

* [策略模式类图](./strategy-class.puml)
* [策略模式时序图](./strategy-timing.puml)

## 适用场景

* 如果在一个系统里面有许多类，它们之间的区别仅在于它们的行为，那么使用策略模式可以动态地让一个对象在许多行为中选择一种行为
* 一个系统需要动态地在几种算法中选择一种
* 不希望客户端知道复杂的、与算法相关的数据结构，在具体策略类中封装算法和相关的数据结构，提高算法的保密性与安全性
