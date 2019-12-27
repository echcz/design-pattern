# 状态模式 StatePattern

状态模式(State Pattern)允许一个对象在其内部状态改变时改变其行为(参考状态机)。

## 代码与图示

``` java
class Context {
    private State state;
    public Context() {
        setState(new ConStateA());
    }
    public void setState(State state) {
        this.state = state;
    }
    public request() {
        state.handle(this);
    }
}
interface State {
    void handle(Context context);
}
class ConStateA implements State {
    public void handle(Context context) {
        // ...
        context.setState(new ConStateB());
    }
}
class ConStateB implements State { /*...*/ }
class Main {
    public static void main(String[] args) {
        Context context = new Context();
        context.request();
        context.request();
    }
}
```

* [状态模式类图](./state-class.puml)
* [状态模式时序图](./state-timing.puml)

## 适用场景

* 对象的行为依赖于它的状态并且可以根据它的状态改变而改变它的相关行为
* 代码中包含大量与对象状态有关的条件语句
