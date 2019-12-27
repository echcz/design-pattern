# 装饰器模式 DecoratorPattren

装饰器模式(Decorator Pattren)用于动态地给现有的对象添加新的职责，其比生成子类的方式更为灵活。

## 代码与图示

``` java
interface Component {
    void operation();
}
class ConComponent implements Component { /*...*/ }
interface Decorator extends Component {
    void addedOperation();
}
class ConDecorator implements Decorator {
    private Component component;
    public ConDecorator(Component component) {
        this.component = component;
    }
    public operation() {
        component.operation();
    }
    public addedOperation() { /*...*/ }
}
class Main {
    public static void main(String[] args) {
        Component component = new ConComponent;
        Decorator decorator = new ConDecorator(component);
        decorator.operation();
        decorator.addedOperation();
    }
}
```

* [装饰器模式类图](./decorator-class.puml)
* [装饰器模式时序图](./decorator-timing.puml)

## 适用场景

* 在不影响其他对象的情况下，以动态、透明的方式给单个对象添加职责
* 当不能采用继承的方式对系统进行扩充或者采用继承不利于系统扩展和维护时
