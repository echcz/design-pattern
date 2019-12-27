# 命令模式 CommandPattern

命令模式(Command Pattern)通过将接收者封装进一个命令对象中让调用者与接收者解耦，让调用者只需知道如何发送请求，而不必知道如何完成请求

## 代码与图示

``` java
class Receiver {
    public void action() { /*...*/ }
}
interface Command {
    void execute();
}
class ConComand implements Command {
    private Receiver receiver;
    public ConComand(Receiver receiver) {
        this.receiver = receiver;
    }
    public void execute() {
        receiver.action();
    }
}
class Invoker {
    private Command command;
    public setCommand(Command command) {
        this.command = command;
    }
    public void call() {
        command.execute();
    }
}
class Main {
    public static void main(String[] args) {
        Receiver receiver = new Receiver();
        Command command = new Command(receiver);
        Invoker invoker = new Invoker();
        invoker.setCommand(command);
        invoker.call();
    }
}
```

* [命令模式类图](./command-class.puml)
* [命令模式时序图](./command-timing.puml)

## 适用场景

* 系统需要将请求调用者和请求接收者解耦，使得调用者和接收者不直接交互
* 系统需要在不同的时间指定请求、将请求排队和执行请求
* 系统需要支持命令的撤销(Undo)操作和恢复(Redo)操作
* 系统需要将一组操作组合在一起，即支持宏命令
