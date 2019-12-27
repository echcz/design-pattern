# 中介者模式 MediatorPattern

中介者模式(Mediator Pattern)用一个中介对象封装一系列对象的交互，使各对象之间不需要显示的关联，从而使它们之间解耦并且可以独立地改变它们之间的交互。

## 代码与图示

``` java
interface Mediator {
    void registe(Integer id, Colleague colleague);
    void operation(Integer id, String msg);
}
class ConMediator implements Mediator {
    private Map<Integer, Colleague> register = new HashMap<>();
    public void registe(Integer id, Colleague colleague) {
        register.put(id, colleague);
        colleague.setMediator(this);
    }
    public void operation(Integer id, String msg) {
        Colleague colleague = register.get(id)
        if (colleague != null) {
            colleague.receiveMsg(msg);
        }
    }
}
interface Colleague {
    void setMediator(Mediator mediator);
    void sendMsg(Integer id, String msg);
    void receiveMsg(String msg);
}
class ConColleagueA implements Colleague {
    private Mediator mediator;
    public void setMediator(Mediator mediator) {
        this.mediator = mediator;
    }
    public sendMsg(Integer id, String msg) {
        mediator.operation(id, msg);
    }
    public receiveMsg(String msg) { /*...*/ }
}
class ConColleagueB implements Colleague { /*...*/ }
class Main {
    public static void main(String[] args) {
        Colleague colleagueA = new ConColleagueA();
        Colleague colleagueB = new ConColleagueB();
        Mediator mediator = new ConMediator();
        mediator.registe(1, colleagueA);
        mediator.registe(2, colleagueB);
        colleagueA.sendMsg(2, "hello world");
    }
}
```

* [中介者模式类图](./mediator-class.puml)
* [中介者模式时序图](./mediator-timing.puml)

## 适用场景

* 系统中对象之间存在复杂的引用关系，产生的相互依赖关系结构混乱且难以理解
* 一个对象由于引用了其他很多对象并且直接和这些对象通信，导致难以复用该对象
* 交互的公共行为，如果需要改变行为则可以增加新的中介者类
