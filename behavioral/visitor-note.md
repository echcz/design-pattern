# 访问者模式 VisitorPattern

访问者模式(Visitor Pattern)使得用户可以在不改变各元素类的情况下添加作用于这个元素的操作，是一种将数据操作和数据结构分离的设计模式，符合开闭原则

## 代码与图示

``` java
interface Element {
    void accept(Visitor visitor)
}
class AElement implements Element {
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}
class BElement implements Element {
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}
interface Visitor {
    void visit(AElement element);
    void visit(BElement element);
}
class XVisitor implements Visitor {
    public void visit(AElement element) { /*...*/ }
    public void visit(BElement element) { /*...*/ }
}
class YVisitor implements Visitor {
    public void visit(AElement element) { /*...*/ }
    public void visit(BElement element) { /*...*/ }
}
class Main {
    public static void main(String[] args) {
        List<Element> elements = new ArrayLIst<>();
        Element a = new AElement();
        Element b = new BElement();
        elements.add(a);
        elements.add(b);
        Visitor x = new XVisitor();
        Visitor y = new YVisitor();
        for(Element element : elements) {
            element.accept(x);
            element.accept(y);
        }
    }
}
```

* [访客模式类图](./visitor-class.puml)
* [访客模式时序图](./visitor-timing.puml)

## 适用场景

* 对象结构比较稳定，但经常需要在此对象上定义新的操作
* 需要对一个对象进行很多不同的操作，但要避免这些操作污染此对象，也不希望在新增操作时修改此对象的类
