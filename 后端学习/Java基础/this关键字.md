this关键字指向的是当前实例（对象）的引用

使用this.memval的格式调用类的成员变量， 可以解决成员变量与局部变量重名的的问题
如
```
package DEMO;

public class Student {
    private String name;
    private int age;

    public void setName(String name){
        this.name = name;
    }

    public void setAge(int age){
        this.age = age;
    }

    public void show(){
        System.out.println(name + ", " + age);
    }
}
```


this也可以调用方法
