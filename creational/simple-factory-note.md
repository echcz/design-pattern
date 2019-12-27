# 简单工厂模式 SimpleFactoryPattern

简单工厂又称静态工厂(Static Factory)，是一个专门用于负责创建其它的类的实例的对象，可以根据参数的不同返回不同实现类的实例。

## 代码与图示

``` java
interface Product { /*...*/ }
class AProduct implements Product { /*...*/ }
class BProduct implements Product { /*...*/ }
class Factory {
    public static Product createProduct(String type) {
        switch(type) {
            case "A":
                return new AProduct();
                break;
            case "B":
                return new BProduct();
                break;
            default:
                return null;
        }
    }
}
class Main {
    public static void main(String[] args) {
        Product product = Factory.createProduct("A")
        // use product for something
    }
}
```

* [简单工厂模式类图](./simple-factory-class.puml)
* [简单工厂模式时序图](./simple-factory-timing.puml)

## 优点

* 实现了对象的创建与使用的责任分离，降低了系统的耦合度
* 简单工厂使用简单方便

## 缺点

* 系统扩展困难，一旦添加新的产品类型，将不得不修改工厂逻辑，不符合开闭原则
* 产品类型较多时，易造成工厂方法逻辑过于复杂

## 适用场景

* 客户端不关于对象创建的细节
* 工厂负责创建的对象较少
