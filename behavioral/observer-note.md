# 观察者模式 ObserverPattern

观察者模式(Observer Pattern)定义对象间的一对多依赖关系，使得当一个对象(观察目标)的状态发生改变时，其相关依赖对象(观察者)得到通知并自动更新。

## 代码与图示

``` java
abstract class Subject {
    private List<Observer> obs = new ArrayList<>();
    public void addObserver(Observer observer) {
        obs.add(observer);
    }
    public void rmObserver(int index) {
        obs.remove(index);
    }
    public void notify() {
        for (Observer ob : obs) {
            ob.update(this);
        }
    }
}
class ConSubject extends Subject {
    private int state;
    public int getState() {
        return state;
    }
    public void setState(int state) {
        this.state = state;
        notify();
    }
}
interface Observer {
    void update(Subject subject);
}
class ConObserver implements Observer { /*...*/ }
class Main {
    public static void main(String[] args) {
        ConSubject conSubject = new ConSubject();
        conSubject.addObserver(observer);
        conSubject.setState(1);
    }
}
```

* [观察者模式类图](./observer-class.puml)
* [观察者模式时序图](./observer-timing.puml)

### JDK自带的观察者模式

``` java
class ConSubject extends Observable {
    private int state;
    public int getState() {
        return state;
    }
    pubic void setState(int state) {
        this.state = state;
        setChanged();
        notifyObservers();
    }
}
class ConObserver implements Observer {
    public void update(Observable o, Object arg) { /*...*/ }
}
class Main {
    public static void main(String[] args) {
        ConSubject conSubject = new ConSubject();
        Observer observer = new ConObserver();
        conSubject.addObserver(observer);
        conSubject.setState(1);
    }
}
```

## 适用场景

* 一个对象的改变将导致其他一个或多个对象也发生改变，而不知道具体有多少对象将发生改变
* 一个抽象模型有两个方面，其中一个方面依赖于另一个方面。将这些方面封装在独立的对象中使它们可以各自独立地改变和复用
