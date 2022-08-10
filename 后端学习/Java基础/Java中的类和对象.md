类是对象的抽象, 对象是类的实体

一个类中有成员变量和成员方法

类是Java程序的基本组成单位

**类的定义**
如下定义了一个phone类
```
package DEMO;

public class phone {
    int price;
    String brand;

    public void PrintPrice(){
        System.out.println("手机价格:" + price);
    }

    public void PrintBrand(){
        System.out.println("手机品牌:" + brand);
    }
}

```
在另一个类中去使用它
```
package DEMO;
import DEMO.phone;

public class TEST {
    public static void main(String[] args) {
        phone i = new phone();
        i.brand = "apple";
        i.price = 7000;

        i.PrintBrand();
        i.PrintPrice();
    }
}
/*
手机品牌:apple
手机价格:7000
*/
```

类中的成员变量具有默认值, 如int类型的为0, String类型的为null

每个类实例的成员变量的内存都是在堆中分配的, 当调用类方法时, 方法会入栈, 调用结束后出栈.

**类（对象）的使用**

要使用一个类， 就要先创建它的一个实例， 即对象。
创建对象的格式为
```
className objName = new className();
```
new语句返回的是内存空间的指针, 所以
```
class i = new class();
class j = i;
```
i 与 j指向的是同一块内存空间, 同一个对象

使用类的成员变量和成员方法
```
obj.val
obj.func(args);
```



