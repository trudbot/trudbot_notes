**函数的定义格式**
```
public static ReturnType FuncName(args list){
    // func body
    return data;
}
```
如以下定义的两个函数
```
public class HelloWorld {
    public static void main(String[] args) {
        Print();
        int i = sum(100, 200);
        System.out.println(i);
    }

    public static void Print(){
        System.out.println("hello world");
    }

    public static int sum(int a, int b){
        return a+b;
    }
}

/*
hello world
300
*/
```
要注意的是
* Java中函数不能用void代表不接收参数
* 函数的作用域与定义位置无关
* 返回数组时, 返回类型为 type[]

**函数的重载**

函数的重载发生于一个类中存在多个同名但参数列表不同的函数时.

```
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println(sum(1, 2));
        System.out.println(sum(1.0, 2.0));
        System.out.println(sum(1, 2, 3));
    }

    public static int sum(int a, int b){
        return a+b;
    }

    public static double sum(double a, double b){
        return a+b;
    }

    public static int sum(int a, int b, int c){
        return a+b+c;
    }
}
```
* 函数参数表必须不同
* 程序运行时, java虚拟机会根据函数参数的不同定位到相应的函数.
* 

**函数的参数传递**
对于栈内存中的变量, 不同函数之间无法相互影响.
```
public class HelloWorld {
    public static void main(String[] args) {
        int i = 100;
        System.out.println(i);
        func(i);
        System.out.println(i);
    }

    public static void func(int x){
        x++;
    }
}
/*
100
100
*/
```
对于堆内存的对象, 就可以在不同函数中访问
```
public class HelloWorld {
    public static void main(String[] args) {
        int arr[] = {1};
        System.out.println(arr[0]);
        func(arr);
        System.out.println(arr[0]);
    }

    public static void func(int[] arr){
        arr[0] = 100;
    }
}
/*
1
100
*/
```

