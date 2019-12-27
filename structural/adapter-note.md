# 适配器模式 Adapter Partten

适配器模式(Adapter Partten)用于转化已有接口为客户期望的接口，以保持对现有类的复用

## 代码与图示

``` java
interface Target {
    void targetMethod()
}
class Adaptee {
    public void srcMethod() { /*...*/ }
}
class Adapter implements Target {
    private Adaptee adaptee;
    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }
    public void targetMethod() {
        adaptee.srcMethod();
    }
}
class Main {
    public static void main(String[] args) {
        Adaptee adaptee; // TODO init it
        Target target = new Adapter(adaptee);
        target.targetMethod();
    }
}
```

* [适配器模式类图](./adapter-class.puml)
* [适配器模式时序图](./adapter-timing.puml)

## 适用场景

* 系统需要使用现有的类，而这些类的接口不符合系统的需要
* 想要建立一个可以重复使用的类，用于与一些彼此之间没有太大关联的一些类，包括一些可能在将来引进的类一起工作
