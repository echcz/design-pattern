# 代理模式 ProxyPattern

代理模式(Proxy Pattern)用于在客户与目标对象插入中介对象以保护目标对象或改变客户得到的服务。

## 代码与图示

``` java
interface Subject {
    void request();
}
class RealSubject implements Subject { /*...*/ }
class Proxy implements Subject {
    private Subject subject;
    public Proxy(Subject subject) {
        this.subject = subject;
    }
    public void request() {
        preRequest();
        subject.request();
        afterRequest();
    }
    private preRequest() { /*...*/ }
    private afterRequest() { /*...*/ }
}
class Main {
    public static void main(String[] args) {
        Subject subject = new RealSubject();
        Subject proxy = new Proxy(subject);
        proxy.request();
    }
}
```

* [代理模式类图](./proxy-class.puml)
* [代理模式时序图](./proxy-timing.puml)

### JDK动态代理

``` java
public class ProxyHandler implements InvocationHandler {
    private Subject subject;
    public ProxyHandler(Subject subject) {
        this.subject = subject
    }
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        preRequest();
        Object result = method.invoke(subject, args)
        afterRequest();
        return result;
    }
    private void preRequest() { /*...*/ }
    private void afterRequest() { /*...*/ }
    public Subject getProxy() {
        return (Subject) Proxy.newProxyInstance(this.getClass().getClassLoader(),
                subject.getClass().getInterfaces(), this);
    }
}
class Main {
    public static void main(String[] args) {
        Subject subject = new RealSubject();
        Subject proxy = new ProxyHandler(subject).getProxy();
        proxy.request();
    }
}
```

## 应用场景

* 远程(Remote)代理：为一个位于不同的地址空间的对象提供一个本地的代理对象，远程代理又叫做大使(Ambassador)
* 虚拟(Virtual)代理：如果需要创建一个资源消耗较大的对象，先创建一个消耗相对较小的对象来表示，真实对象只在需要时才会被真正创建
* Copy-on-Write代理：它是虚拟代理的一种，把复制（克隆）操作延迟到只有在客户端真正需要时才执行。一般来说，对象的深克隆是一个开销较大的操作，Copy-on-Write代理可以让这个操作延迟，只有对象被用到的时候才被克隆
* 保护(Protect or Access)代理：控制对一个对象的访问，可以给不同的用户提供不同级别的使用权限
* 缓冲(Cache)代理：为某一个目标操作的结果提供临时的存储空间，以便多个客户端可以共享这些结果
* 防火墙(Firewall)代理：保护目标不让恶意用户接近
* 同步化(Synchronization)代理：使几个用户能够同时使用一个对象而没有冲突
* 智能引用(Smart Reference)代理：当一个对象被引用时，提供一些额外的操作，如将此对象被调用的次数记录下来等
