# 外观模式 FacadePattern

外观模式(Facade Parttern)定义了一个高层接口，为了系统中的一组接口提供了一致的界面，从而使得子系统更为易用。

## 代码与图示

``` java
class SystemA {
    public void oprationA() { /*...*/ }
}
class SystemB {
    public void oprationB() { /*...*/ }
}
class Facade {
    private SystemA systemA;
    private SystemB systemB;
    public void warpOpration() {
        systemA.oprationA();
        systemB.oprationB();
    }
}
class Main {
    public static void main(String[] args) {
        Facade facade; // init it
        facade.warpOpration();
    }
}
```

* [外观模式类图](./facade-class.puml)
* [外观模式时序图](./facade-timing.puml)

## 适用场景

* 当要为一个复杂子系统提供一个简单接口时
* 在层次化结构中，可以使用外观模式定义系统中每一层的入口，层与层之间不直接产生联系，而通过外观类建立联系，降低层之间的耦合度
