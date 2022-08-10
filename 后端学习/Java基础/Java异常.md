java中每个报错其实都是一个类。

**throwable**
即"可抛出"，
它是java中error和Exception的直接父类， Java中可抛出类分为Error和Exception。

error : Error是的Throwable子类 表示严重的问题，合理的应用程序不应该试图捕获。 大多数此类错误都是异常情况。 
exception: 类异常及其子类是Throwable一种形式，它指示合理的应用程序可能想要捕获的条件。

**JVM对异常的处理方案**
* 输出异常的名称、异常原因以及异常出现位置
* 停止运行

**异常处理**
try--catch--finally
```java
try {
    // 可能会发生异常的语句
} catch(ExceptionType e) {
    // 处理异常语句
} catch(ExceptionType e) {
    // 处理异常语句
} catch(ExceptionType e) {
    // 处理异常语句
...
}finally{
    // 清理代码块
}
```
对于以上格式，无论是否发生异常（除特殊情况外），finally 语句块中的代码都会被执行。

如程序出现异常, 会在异常出new一个对应异常的对象, catch中对异常对象进行捕捉和匹配, 若匹配成功则执行代码块
```
int[] arr = {0, 1, 2};
System.out.println("开始");
try{
    System.out.println(arr[3]);
}catch (ArrayIndexOutOfBoundsException e){
    System.out.println("索引越界！");
}
System.out.println("结束");
/*
开始
索引越界！
结束

*/
```

**throwable的成员方法**
所有异常类都可以使用throwable的成员方法

getMessage, 返回可抛出类的详细信息
toString, 返回可抛出类的简短描述
printStackTrace, 打印异常信息(最完整)
```
int[] arr = {0, 1, 2};
System.out.println("开始");
try{
    System.out.println(arr[3]);
}catch (ArrayIndexOutOfBoundsException e){
    System.out.println(e.getMessage());
    System.out.println();

    System.out.println(e.toString());
    System.out.println();

    e.printStackTrace();
}
/*
开始
Index 3 out of bounds for length 3

java.lang.ArrayIndexOutOfBoundsException: Index 3 out of bounds for length 3

java.lang.ArrayIndexOutOfBoundsException: Index 3 out of bounds for length 3
	at DEMO.TEST.main(TEST.java:14)
*/
```

**异常的种类**
异常可以分为编译时异常和运行时异常

* 运行时异常：都是RuntimeException类及其子类异常，如NullPointerException(空指针异常)、IndexOutOfBoundsException(下标越界异常)等，这些异常是不检查异常，程序中可以选择捕获处理，也可以不处理。这些异常一般是由程序逻辑错误引起的，程序应该从逻辑角度尽可能避免这类异常的发生。
运行时异常的特点是Java编译器不会检查它，也就是说，当程序中可能出现这类异常，即使没有用try-catch语句捕获它，也没有用throws子句声明抛出它，也会编译通过。
* 非运行时异常 （编译异常）：是RuntimeException以外的异常，类型上都属于Exception类及其子类。从程序语法角度讲是必须进行处理的异常，如果不处理，程序就不能编译通过。如IOException、SQLException等以及用户自定义的Exception异常，一般情况下不自定义检查异常。

**throws**
当一个方法产生一个它不处理的异常时，那么就需要在该方法的头部声明这个异常，以便将该异常传递到方法的外部进行处理。
```
public static void main(String[] args) {
    try{
        foo();
    } catch (ArrayIndexOutOfBoundsException e){
        System.out.println(e.getMessage());
    }
}

public static void foo() throws ArrayIndexOutOfBoundsException{
    int[] arr = {1, 2, 3};
    System.out.println(arr[3]);
}
```
如在foo函数中, 如果发生了ArrayIndexOutOfBoundsException, 就会将异常抛给调用层, 由调用层来处理异常.

如果有多个异常类，它们之间用逗号分隔
```
returnType method_name(paramList) throws Exception 1,Exception2,…{…}
```

> 使用 throws 声明抛出异常的思路是，当前方法不知道如何处理这种类型的异常，该异常应该由向上一级的调用者处理；如果 main 方法也不知道如何处理这种类型的异常，也可以使用 throws 声明抛出异常，该异常将交给 JVM 处理。JVM 对异常的处理方法是，打印异常的跟踪栈信息，并中止程序运行，这就是前面程序在遇到异常后自动结束的原因。

**多异常捕获**
当存在对于多个不同种类的异常而处理方式相同时, 可以用多异常捕获来精炼代码
如
```
try{
    // 可能会发生异常的语句
} catch (IOException | ParseException e) {
    // 调用方法methodA处理
}
```

**自定义异常**
有时Java内置的异常不能满足我们使用的需求, 这时我们可以自己设计异常.

自定义异常类需要继承RunTimeException或Exception
>自定义异常类一般包含两个构造方法：一个是无参的默认构造方法，另一个构造方法以字符串的形式接收一个定制的异常消息，并将该消息传递给超类的构造方法。

如下定义了一个分数范围的异常类
```
public class ScoreRangeException extends Exception{
    public ScoreRangeException() {
    }

    public ScoreRangeException(String message) {
        super(message);
    }
}
```
在一个学生类型中使用了ScoreRangeException, CheckScore方法检查分数是否正确否则向调用层抛出异常

在方法中声明异常使用throw关键字, 后接一个异常类的对象, 代表此处发生了某类异常, 而使用throws能在方法发生某类异常时, 向调用层抛出异常
```
public class Student {
    private int score;

    public int getScore() {
        return score;
    }

    public void setScore(int score) {
        this.score = score;
        try {
            CheckScore();
        } catch (ScoreRangeException e) {
            e.printStackTrace();
        }
    }

    public void CheckScore() throws ScoreRangeException{
        if(score < 0 || score > 100){
            throw new ScoreRangeException("分数不正确: "+ score);
        }
    }
}
```
在测试类中
```
public static void main(String[] args) {
    MyUtil util = new MyUtil();
    int score = util.InputInt();

    Student stu = new Student();
    stu.setScore(score);
}
/*
1000
DEMO.Exception.ScoreRangeException: 分数不正确: 1000
	at DEMO.Exception.Student.CheckScore(Student.java:23)
	at DEMO.Exception.Student.setScore(Student.java:15)
	at DEMO.TEST.main(TEST.java:16)

*/
```