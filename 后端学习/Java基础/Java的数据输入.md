java中的数据输入要用到Java的一个类:Scanner

**导包**
```
import java.util.Scanner;
```

**创建对象**
```
Scanner s = new Scanner(System.in);
```

**获取输入**
```
s.next();
s.nextLine();
s.nextInt()
等等
```
**使用实操**

```
import java.util.Scanner;

public class TEST {
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        System.out.println(s.nextLine());
    }
}
/*
in:
Hello world
out:
Hello world
*/
```

