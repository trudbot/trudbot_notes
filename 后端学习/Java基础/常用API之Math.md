Math类封装了一些与数学有关的属性和方法。

Math类中的成员变量和方法都用static修饰, 因此都可以通过类名直接访问.

#### 常用常量

```
Math.PI
Math.E
```
都为double型
#### 常用方法

```
绝对值
Math.abs(int x)

//向上取整和向下取整, 但注意返回值为double
Math.ceil(double x)
Math.floor(duuble x)

//四舍五入, 返回值为Int
Math.round(double x)

//最大最小值, 当然有多种重载函数
Math.max(int a, int b)
Math.min(int a, int b)

//幂函数, a的b次幂, 返回值为double类型
Math.pow(a, b)

//平方根
Math.sqrt(double x)


