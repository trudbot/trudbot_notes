String类是Java的基础类， 使用时， 不需要导包。

Java中所有的字符串， 都是String类。

**String类是一种不可变的数据类型。**

**String类的常用构造方法**
* 无参构造， String()
* 由字符数组构造， String(char[] value)

**创建字符串对象的方式**

```
String str1 = new String();//只能创建一个空字符串
char[] arr = {'a', 'b', 'c'};
String str2 = new String(arr);//由字符数组创建字符串
String str3 = "hello";
```

**String对象的特点**
* 通过new以数组创建字符串， 都会分配单独的内存空间
* 通过直接赋值创建字符串， 若字符串的内容与之前创建的某个字符串相同， 则两个字符串会指向同一块内存空间。

**字符串的比较**
标准库方法equals
使用格式：str1.equals(str2)
返回布尔类型的值

**字符串的长度**
str.length();

**获取字符串某索引处的字符**
str.charAt(index);
返回该索引处的字符

**字符串的拼接**

- 两个字符串的相加操作， 会将两个字符串前后拼接， 返回一个新的字符串。
- 函数：str1.concat(str2);将str2拼接到str1的末尾而形成一个新的字符串并返回

```
public class TEST {
    public static void main(String[] args) {
        String s = "hello";
        System.out.println(s + "hello");
        System.out.println(s);
        System.out.println(s.concat("java"));
        System.out.println(s);
    }
}
/*
hellohello
hello
hellojava
hello
*/
```
可以看到两种方法都不会改变原字符串, 要改变原字符串, 
可以用
str1 += str2;
或
str1 = str1.concat(str2);
