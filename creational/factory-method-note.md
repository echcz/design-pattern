# 工厂方法模式 FactoryMethodPattern

工厂方法模式是简单工厂模式的进一步抽象和改进。相比简单工厂模式，抽象工厂模式使用了多态的方式将创建过程延迟到子类中来创建不同子类产品，而不是在方法内使用逻辑分支。

## 代码与图示

``` java
interface Product { /*...*/ }
class AProduct implements Product { /*...*/ }
class BProduct implements Product { /*...*/ }
interface Factory {
    Product createInstace();
}
class AFactory implements Factory {
    Product createInstace() {
        return new AProduct();
    }
}
class BFactory implements Factory {
    Product createInstace() {
        return new BProduct();
    }
}
class Main {
    public static void main(String[] args) {
        Factory factory = new AFactory();
        Product product = factory.createInstance();
        // use product for something
    }
}
```

* [工厂方法模式类图](./factory-method-class.puml)
* [工厂方法模式时序图](./factory-method-timing.puml)

## 优点

* 参见简单工厂模式优点
* 除此之外，解决了简单工厂在新增产品类时只能修改工厂方法，不符合开闭原则的缺点。在新增产品类时只需要加一个对应的的工厂实现类。

## 缺点

* 一个产品子类会对应一个工厂实现类，这样会导致系统的类的个数加多，增加了系统的复杂度。

## 适用场景

* 参见简单工厂模式适用场景
