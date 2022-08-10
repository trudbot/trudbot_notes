Object类是所有类直接或间接的父类,  当一个类没有明确继承某个类时, Object类就是它的直接父类

也就是说以下两种形式是完全相同的
```
class A{}

class A extends Object{}
```

#### 常用方法
**toString**
以字符串的形式返回对象的信息, 原型存在于Object类中, 子类一般需要对它进行重写
用java标准输出如println对对象进行输出时, 其实等价于println(object.toString())
```
class demo{
    int x = 100;
    String str = "hello";
}

public class TEST {

    public static void main(String[] args) {
        demo d = new demo();
        System.out.println(d.toString());//DEMO.demo@4eec7777
    }
}
```
重写toString
```
package DEMO;
import java.util.*;


class demo{
    int x = 100;
    String str = "hello";

    @Override
    public String toString() {
        return "demo{" +
                "x=" + x +
                ", str='" + str + '\'' +
                '}';
    }
}

public class TEST {

    public static void main(String[] args) {
        demo d = new demo();
        System.out.println(d.toString());
        //demo{x=100, str='hello'}
    }
}
```

**equals**

在Object类中的equals原型只能判断两个对象是否是同一个对象, 即地址是否相同, 所以一般也会重写equals方法
在idea中使用alt + insert也可以自动生成
如
```
class Student{
    String name;
    int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;

        Student student = (Student) o;

        if (age != student.age) return false;
        if (name != null ? !name.equals(student.name) : student.name != null) return false;

        return true;
    }

}

public class TEST {

    public static void main(String[] args) {
        Student stu1 = new Student("张三", 19);
        Student stu2 = new Student("张三", 19);
        System.out.println(stu1.equals(stu2));//true
    }
}
```


