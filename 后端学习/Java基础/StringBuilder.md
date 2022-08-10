StringBuilder是一个可变的字符串类.]
定义在java.lang中, 使用时无需导包

**常用的构造方法**
创建一个空串
```
StringBuilder str1 = new StringBuilder();
```
根据String对象创建StringBuilder
```
StringBuilder str2 = new StringBuilder("hello world");
```
完整代码
```
public class TEST {
    public static void main(String[] args) {
        StringBuilder str1 = new StringBuilder();
        StringBuilder str2 = new StringBuilder("hello world");
        System.out.println("str1:" + str1);
        System.out.println("str2:" + str2);

    }
}
/*
str1:
str2:hello world
*/

```

**常用的函数**

* strb.length();

* strb.append(str);
将str拼接到strb的末尾, 注意的是会直接改变strb.返回值是strb本身(地址)
同时, append函数有多种重载形式, 参数可以是多种类型的值或对象, 如字符数组, 整型等

* toString()
根据StringBuilder的内容返回一个String对象

```
public class TEST {
    public static void main(String[] args) {
        StringBuilder str = new StringBuilder();
        str.append("hello");
        str.append(" ").append("world");//append的返回值是源对象, 所以可以使用链式编程
        System.out.println(str);
        String str1 = str.toString();
        System.out.println(str1);
    }
}
/*
hello world
hello world
*/
```

