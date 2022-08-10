**算术运算符**
```
+ - * / %
```
运算符用法与运算规则与C相同
算术表达式中若有多个类型的参与， 那么所有的数据的类型都会被提升到表达式中的最高等级的类型， 即向‘上’转换
如一个char 类型的变量与int类型的变量进行运算， char类型的值会暂时转换为int 类型， 所以结果为int类型

同理整形与浮点型进行运算结果为浮点型


字符串的相加即把两个字符串前后拼接
```
public class HelloWorld {
    public static void main(String[] args){
        System.out.println("hello"+" "+"world");
    }
}
//hello world
```
注意， 任何的类型的量与字符串进行相加， 都会先转换为字符串， 然后拼接
```
public class HelloWorld {
    public static void main(String[] args){
        System.out.println("hello" + 100 + 0);//hello1000
        System.out.println(1 + 99 + "dollars");//100dollars
        //顺序执行
        
    }
}
```

**赋值运算符**
```
+
+=
-=
*=
/=
%=
```
要注意的是 a += i 与 a = a + i 类似的形式有时侯并不等价
如
```
int i = 1;
i += 1;
i = i+1;//两者等价
```  
```
short i = 1;
i += 1;//正常
i = i + 1;//报错, 因为1默认是int类型
```
**自增自减运算符**
```
++
--
```
与C相同
**关系运算符**
```
==
!=
>
>=
<
<=
```
==若比较的是基本数据类型， 则比较值；若为对象， 则比较内存地址
关系运算的结果是布尔类型
```
public class HelloWorld {
    public static void main(String[] args){
        System.out.println(1 == 2);
    }
}
//false
```

**逻辑运算符**
```
& 与
| 或
^ 异或
！非
```

```
&& 短路与
|| 短路或
```

&（|）和 &&（||）的区别是， &(|)两边的表达式都会运行并判断， 
而&&（||）只要左边的表达式为假(真）， 右边的表达式将不会被执行

```
public class HelloWorld {
    public static void main(String[] args){
        int i=1, j=2;
        System.out.println((i++)>10 && (j++>10));//false
        System.out.println("i:"+i+"  j:"+j);//i:2  j:3
        i = 1;
        j = 2;
        System.out.println((i++)>10 && (j++>10));//false
        System.out.println("i:"+i+"  j:"+j);//i:2  j:2
    }
}
```
**三元表达式**

关系式 ？ 表达式1 ： 表达式2；
Java的三元表达式中表达式12只能为值，且不能为空， 所以三元表达式一定有一个值。

如
```
max = i>j ? i : j;
```


