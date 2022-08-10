**声明数组的两种形式**
```
type name[];
type[] name; //推荐
```
Java中type[] 即表示数组的类型, 为了方便C/Cpp程序员快速了解Java, 所以仍保留了type name[]格式的使用.
**数组的动态初始化**

```
//1
type[] name;
name = new type[size];
//2
type[] name = new type[size];
```
Java中数组在初始化时, 会自动为空间赋初始值, 
整数:0
浮点数:0.0
布尔值:false
字符:空字符

new是内存分配符, 用于为创建对象在堆上申请一块新的空间, 返回地址
type[] name 就是创建C语言中一个指针变量, 而new type[size]就是C语言中的动态分配, 返回指针.

**数组的静态初始化**
两种形式
```
type[] name = new type[]{value1, value2...};

type[] name = {value1, value2...};

```
数组的长度不指定, 为花括号中元素个数
内存依然在堆中分配

**数组的长度**
Java中数组对象有一个length方法, 可以用于获取数组长度.

**遍历数组的方式**
* 下标遍历
```
public class HelloWorld {
    public static void main(String[] args) {
        int arr[] = new int[]{1, 2, 4};
        for(int i=0; i<arr.length; i++)
            System.out.println(arr[i]);
    }
}
```
* foreach循环
```
public class HelloWorld {
    public static void main(String[] args) {
        int arr[] = new int[]{1, 2, 4};
        for(int i : arr)
            System.out.println(i);
}
```
类似于python, 依次取出数组的每一个元素

