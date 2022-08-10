> Lambda 表达式是一种匿名函数(对 Java 而言这并不完全正确，但现在姑且这么认为)，简单地说，它是没有声明的方法，也即没有访问修饰符、返回值声明和名字。

**语法格式**
```
(arg1, arg2...) -> { body }

(type1 arg1, type2 arg2...) -> { body }
```

**Lambda 表达式的结构**

- 一个 Lambda 表达式可以有零个或多个参数
- 参数的类型既可以明确声明，也可以根据上下文来推断。例如：(int a)与(a)效果相同
- 所有参数需包含在圆括号内，参数之间用逗号相隔。例如：(a, b) 或 (int a, int b) 或 (String a, int b, float c)
- 空圆括号代表参数集为空。例如：() -> 42
- 当只有一个参数，且其类型可推导时，圆括号（）可省略。例如：a -> return a*a
- Lambda 表达式的主体可包含零条或多条语句
- 如果 Lambda 表达式的主体只有一条语句，花括号{}可省略。匿名函数的返回类型与该主体表达式一致
- 如果 Lambda 表达式的主体包含一条以上语句，则表达式必须包含在花括号{}中（形成代码块）。匿名函数的返回类型与代码块的返回类型一致，若没有返回则为空
- 使用Lambda表达式必须有上下文环境, 才能推断接口

**函数式接口**
即只有一个抽象方法的接口.

在java中lambda表达式就与函数式接口配合使用, 能够简洁的实现接口, 每个Lambda表达式都能转化为一个接口的实现类.

如Runable
```java
Runnable runnable = () -> {
    System.out.println("hello world");
};
```

@FunctionalInterface常用于修饰函数式接口, 可以防止发生错误
```java
@FunctionalInterface
interface ADD {
    int add(int a, int b);
}

public class Main {
    static Scanner sc = new Scanner(System.in);

    public static void main(String[] args) {
        foo((a, b) -> {
            return a+b;
        });
    }
    
    public static void foo(ADD a) {
        System.out.println(a.add(10, 20));
    }
}
```

Lambda 表达式与匿名类的另一不同在于两者的编译方法。Java 编译器编译 Lambda 表达式并将他们转化为类里面的私有函数，它使用 Java 7 中新加的 invokedynamic 指令动态绑定该方法，关于 Java 如何将 Lambda 表达式编译为字节码，Tal Weiss 写了一篇[很好的文章](https://blog.overops.com/compiling-Lambda-expressions-scala-vs-java-8/)。