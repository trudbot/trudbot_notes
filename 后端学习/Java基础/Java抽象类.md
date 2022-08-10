在多态举的person、student的类中， person只是形如student这样的类的模板， person可能不会被单独的实例化， 更多的是作为其它类的父类。

> 在面向对象的概念中，所有的对象都是通过类来描绘的，但是反过来，并不是所有的类都是用来描绘对象的，如果一个类中没有包含足够的信息来描绘一个具体的对象，那么这样的类称为抽象类。

抽象类是从多个类中抽象出来的模板
**抽象类**
* 抽象类不能实例化， 但其它功能都还具备， 比如成员变量、成员方法、构造方法
* 抽象类只有被继承才能被使用
定义抽象类时在类名前加修饰符abstract

**抽象方法**
* 抽象方法没有方法体
* 只有抽象类中才能有抽象方法
* 子类继承了抽象类后，除非子类是抽象类， 否则必须重写其中的抽象方法(所以抽象方法不能用private修饰)
* 构造方法、静态方法不能声明为抽象方法

抽象方法的特点很好的体现了抽象类的模板作用。
定义抽象方法时在方法前加修饰符abstract
**例子**
一个抽象类figure， 它限定了它的子类必须有计算面积和计算周长的两个函数
```
public abstract class figure {

    public abstract double getArea();

    public abstract double getPerimeter();
}
```
以下是两个子类
```
public class rectangle extends figure{
    private double length;
    private double width;

    public rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }

    public double getArea(){
        return length*width;
    }

    public double getPerimeter(){
        return 2*(length+width);
    }
}
```
```
public class circle extends figure {
    private double radius;
    private static final double pi = 3.14159;

    public circle(double radius) {
        this.radius = radius;
    }

    public double getArea(){
        return pi*radius*radius;
    }

    public double getPerimeter(){
        return 2*pi*radius;
    }
}
```
