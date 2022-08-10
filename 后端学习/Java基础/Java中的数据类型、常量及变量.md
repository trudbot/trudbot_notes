java是强类型语言， 每一种数据都有明确的数据类型
# 基本数据类型
### 整形

java中有多种不同内存占用的整形
**byte**
占用一个字节， 表示范围是-128到127

**short**
占用两个字节
**int**
占用4个字节
**long**
占用8个字节

### 浮点型
**float**
4个字节
**double**
8个字节


### 字符型
**char**
2个字节， 0到65535

### 布尔型
**boolean**
1个字节， true or false

# 常量
有字符串常量、整数常量、浮点数常量、布尔常量及空常量， 除空常量外其他均可直接输出

如
```
public class output{
    public static void main(String[] args){
        System.out.println("hello world");
        System.out.println(199);
        System.out.println(3.14159);
    }
}
//注释格式与C相同
/*
hello world
199
3.14159
*/

```
空变量即null， 不可直接输出

# 变量

java中变量的声明与C相同
都是 类型 变量名；

**需要注意的几个地方**
Java中整形变量定义默认是int， 浮点型默认是double， 如下定义是错误的：
* long i = 100; // 无效， 其类型仍然是int
* float i = 3.14; //报错， float与double不兼容， 转换可能会损失。

要正确定义long或float类型的变量时， 应该以如下格式

```
long a = 10000000l;//数据后加l
float b = 3.14f;//数据后加f
```

### 数据类型转换
**自动类型转换**
可以将某些类型的常量或变量复制给不同类型的变量或常量，
如把short、char赋值给int
把int、long赋值给float、double

java类型转换只能从小到大， 不能反过来

**强制类型转换**
```
int i = 99.99; // 报错
int i = (int)99.99; // 不报错， i == 99
```
要注意的是即使用强制类型转换， int等类型也不能转换成boolean类型
### 一些琐碎的知识点

标识符命名规则：仅有字母数字下划线组成， 且不以数字开头， 区分大小写。

# 引用数据类型

在堆中存储的数据靠储存在栈中的引用来指向。
引用数据类型有数组、字符串、类以及接口等

引用数据类型和基本数据类型构成了Java的两大数据类型