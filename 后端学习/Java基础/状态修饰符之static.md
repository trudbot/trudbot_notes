static叫静态修饰符

正如其名， 静态就是在一次分配内存后， 这块内存会一直存在， 直到程序结束。

> 被static修饰的成员变量和成员方法独立于该类的任何对象。也就是说，它不依赖类特定的实例，被类的所有实例共享。只要这个类被加载，Java虚拟机就能根据类名在运行时数据区的方法区内定找到他们。因此，static对象可以在它的任何对象创建之前访问，无需引用任何对象。

static是状态修饰符， 不会改变变量或方法的作用域。
static不允许用来修饰局部变量。

**静态成员变量**
静态成员变量相较于普通成员变量， 最大的特点是静态只跟类有关， 而跟类的实例无关， 且在内存中只有一块拷贝；即静态成员变量是所有类实例所共享的。

静态成员变量由于是类的所有实例所共享的， 所以并不建议通过某个实例去访问它， 而是直接用类名去访问它。

如一个学生类有相同的大学
```
public class Student {
    private String name;
    private int age;
    public static String university;

    public Student(String name, int age){
        this.name = name;
        this.age = age;
    }

    public void display(){
        System.out.println(this.name + ", " + this.age + ", " + Student.university);//使用类名获取静态变量的值
    }
}
```
```
public class Test {
    public static void main(String[] args) {
        Student.university = "SWPU";//使用类名去修改静态变量的值
        
        Student stu1 = new Student("jessie", 19);
        stu1.display();
        
        Student stu2 = new Student("mortis", 99);
        stu2.display();
    }
}
/*运行结果
jessie, 19, SWPU
mortis, 99, SWPU
*/

```
**静态成员方法**
静态方法类似的， 同样不依附于任何类实例。

由此特性， 静态方法中不能访问非静态成员变量或非静态成员方法， 因为非静态变量或方法是与具体的类实例相关联的。

![image.png](https://note.youdao.com/yws/res/6555/WEBRESOURCEdf30df63400f2bb320c087218efe97dd)

可以看到， 静态方法中可以使用静态变量或方法， 而使用非静态成员时编译器报错。

**static代码块**
static代码块用于对类的初始化， 在加载类时自动被执行。

将只需要执行一次的代码放到static块中， 能提高程序性能。

类中可以有多个static代码块， 加载类时会按顺序被执行。

static块中同样不能访问非静态成员。

```
public class Student {
    private String name;
    private int age;
    public static String university;

    static {
        System.out.println("Student类被成功加载了！");
    }

    public Student(String name, int age){
        this.name = name;
        this.age = age;
    }

}
```
```
public class Test {

    public static void main(String[] args){
        Student stu = new Student("jessie", 20);
    }

}
//Student类被成功加载了！
```

**

