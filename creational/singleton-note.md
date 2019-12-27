# 单例模式 SingletonPattern

单例模式(Singleton Pattern)用于确保某类在全局只有一个实例。

## 代码

``` java
class Singleton {
    private static Singleton instance = new Singleton();
    public static Singleton getInstance() {
        return instance;
    }
    private Singleton() { /*私有化构造器以限制实例化*/}
}

// 使用枚举(推荐)
enum Singleton {
    INSTANCE;
}

// 懒加载
class Singleton {
    private static Singleton instance = null;
    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

// 懒加载-双重检查
class Singleton {
    private volatile static Singleton instance = null;
    public static Singleton getInstance() {
        if (instance == null) {
            synchronized(Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```
