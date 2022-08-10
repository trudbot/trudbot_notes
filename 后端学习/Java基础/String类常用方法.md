**valueof**
静态方法, 作用是把一些基本类型的数据转换为字符串形式
如
```
String s = String.valueof(100);
```

**split**
String[] split(String regex) 
将字符串以传入字符串为间隔进行分割
返回分割后的子串数组
```
String s = "19, 20, 33, 22";
String[] arr = s.split(", ");
System.out.println(Arrays.toString(arr));
//[19, 20, 33, 22]
```

**replace**
String replace(target, replacement);
将字符串中的与target匹配的子串替换为指定的字符串, 不改变原字符串, 而是将改变后的内容返回
```
String s = "19, 20, 33, 22";
s = s.replace(", ", "|");
System.out.println(s);
//19|20|33|22
```


