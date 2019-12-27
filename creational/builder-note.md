# 建造者模式 BuilderPattern

建造者模式(Builder Pattern)是一步步地创建对象的模式，用于将对象创建的过程与对象的表示进行分离。

## 代码与图示

``` java
class Product { /*...*/ }
interface Builder {
    void buildPartA();
    void buildPartB();
    void buildPartC();
    Product getResult();
}
class ConBuilder implements Builer{ /*...*/ }
class Director {
    private Builder builder;
    public Product build() {
        builder.builderPartA();
        builder.builderPartB();
        builder.builderPartC();
        return builder.getResult();
    }
    public void setBuilder(Builder builder) {
        this.builder = builder;
    }
}
class Main {
    public static void main(String[] args) {
        Builder builder = new ConBuilder();
        Director director = new Director();
        director.setBuilder(builder);
        Product product = director.build();
        // use product for something
    }
}
```

* [建造者模式类图](./builder-class.puml)
* [建造者模式时序图](./builder-timing.puml)

## 优点

* 将产品本身与产品的创建过程解耦，使得相同的创建过程可以创建不同的产品对象
* 将复杂产品的创建步骤分解在不同的方法中，使得创建过程更加清晰，也更方便使用程序来控制创建过程
* 增加新的具体建造者无须修改原有类库的代码，指挥者类针对抽象建造者类编程，系统扩展方便，符合“开闭原则”

## 适用场景

* 需要生成的产品对象有复杂的内部结构，这些产品对象通常包含多个成员属性，且这些属性相互依赖，需要以一定的顺序进行构造
* 对象的创建过程独立于创建该对象的类。在建造者模式中引入了指挥者类，将创建过程封装在指挥者类中，而不在建造者类中
* 隔离复杂对象的创建和使用，并使得相同的创建过程可以创建不同的产品

## 模式扩展

* 如果系统中只需要一个具体建造者的话，可以省略掉抽象建造者
* 在具体建造者只有一个的情况下，如果抽象建造者角色已经被省略掉，那么还可以省略指挥者角色，让Builder角色扮演指挥者与建造者双重角色
