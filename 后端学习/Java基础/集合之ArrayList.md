ArrayList即列表， 是可变长度的数组实现
类名为ArrayList<E>, E为列表中数据的类型
**常用构造方法**
创建一个空列表
ArrayList<type> listName = new ArrayList<>();

type为列表中元素的类型， 且必须为引用类型
如
```
ArrayList<string> list = new ArrayList<>();//后面的尖括号中也可以加上String
ArrayList list = new ArrayList();//也可以不指定类型
ArrayList list = new ArrayList(100); //构造时可以指定一个初始容量
```

**增加元素**
在列表末尾添加一个元素
```
public class TEST {
    public static void main(String[] args) {
        ArrayList<String > list = new ArrayList<>();
        list.add("hello");
        list.add("world");
    }
}
```
在指定索引处添加元素， 索引若不合理会报错
```
public class TEST {
    public static void main(String[] args) {
        ArrayList<String > list = new ArrayList<>();
        list.add(0, "hello");//返回值为boolean类型, 代表是否添加成功
    }
}
```

**打印列表**
使用println函数可以直接打印列表
```
public class TEST {
    public static void main(String[] args) {
        ArrayList<String > list = new ArrayList<>();
        list.add("hello");
        list.add("world");
        list.add(1, "java");
        System.out.println(list);
    }
}

//[hello, java, world]
```

**常用的方法**
```
public class TEST {
    public static void main(String[] args) {
        ArrayList<String > list = new ArrayList<>();
        list.add("hello");
        list.add("world");
        list.add("java");
        System.out.println(list);//[hello, world, java]
        
        //列表是否为空, 返回boolean类型
        System.out.println(list.isEmpty());//false
        
        //列表中的元素个数
        System.out.println(list.size());//3
        
        //查找指定内容在列表中第一次出现的索引, 未找到返回-1
        System.out.println(list.indexOf("world"));//1
        
        //改变列表指定索引位置的内容
        list.set(list.indexOf("java"), "javaee");
        System.out.println(list);//[hello, world, javaee]
        
        //获取列表指定索引处的内容
        System.out.println(list.get(0));//hello
        
        //按索引删除元素, 返回值为被删除的元素
        System.out.println(list.remove(1));//world
        
        //按值删除元素, 返回值为boolean, 代表是否成功删除该内容
        System.out.println(list.remove("java"));//false
    }
}
```
**列表的遍历**
跟数组一样, 列表的遍历也有两种方式
```
import java.util.ArrayList;

public class TEST {
    public static void main(String[] args) {
        ArrayList<String > list = new ArrayList<>();
        list.add("hello");
        list.add("world");
        list.add("java");

        for(int i=0; i<list.size(); i++){
            String s = list.get(i);
            System.out.println(s);
        }

        for(String s : list){
            System.out.println(s);
        }
    }
}
```

