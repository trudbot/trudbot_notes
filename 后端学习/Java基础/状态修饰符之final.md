final, 最终的， 不可改变的

>final在Java中是一个保留的关键字，可以声明成员变量、方法、类以及本地变量。一旦你将引用声明作final，你将不能改变这个引用了，编译器会检查代码，如果你试图将变量再次初始化的话，编译器会报编译错误。

**final修饰类**
final加在权限修饰符的后面
```
public final class className{
    ***
}
```
被final修饰的类将不能被继承(太监类)

**final修饰方法**
如
```
public class demo{
    String s = "hello";
    
    public final String getS(){
        return this.s;
    }
}
```
被final修饰的方法不能在子类被重写， 同时final修饰后的方法会比原来更快(变成静态的了)。

**final修饰局部变量**
被final修饰的变量将不能再改变， 但未被赋值时可以被赋值一次。
即一次赋值， 终生不变

但要注意的是
对于基本类型变量来说， 不变的是数据值
对于引用类型变量(相当于指针变量)来说， 不变的是地址， 数据值可以改变。

**final修饰成员变量**
被final修饰的成员变量也具有和被修饰的局部变量相同的不可变的特点

除此之外， 在类被初始化时， final成员变量必须得到初值。
一种方法是手动赋予初值如
```
final String name = "jessie";
```
另一种方法是通过构造方法赋初值
```
public class demo{
    final String name;
    
    public demo(){
        this.name = "jessie";
    }
    
    public demo(String name){
        this.name = name;
    }
}
```
要注意的是， 每个构造方法都要有语句对final变量进行赋初值。

