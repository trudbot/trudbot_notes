**导入Random类**
import java.util.Random;

**new一个Random对象**
Random name = new Random(long seed);

创建random对象时可以指定种子, 也可以不直接指定(使用系统时间的毫秒数作为种子)

**获取随机数**
name.nextint(bound);

返回一个[0, bound)之间的一个整数

```
import java.util.Random;

public class HelloWorld {
    public static void main(String[] args){
        Random r = new Random();
        int i = 0;
        while(i < 70)
        {
            i = r.nextInt(100);
            System.out.println(i);
        }
    }
}
/*
69
67
46
50
10
83

*/
```
