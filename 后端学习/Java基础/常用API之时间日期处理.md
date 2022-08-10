#### Date类
> Date 类主要封装了系统的日期和时间的信息

**构造方法**
无参构造, 对象的时间为分配时的系统时间
```
Date date = new Date();
```
带参构造, 对象的时间为GMT时间+参数时间(ms)
```
Date date = new Date(1000);//GMT时间加上1s
```


**常用方法**
toString():显示对象的时间, 顺序为星期、月、日、小时、分、秒、年。

```
Date date = new Date();
System.out.println(date);
//Tue Jun 28 20:57:05 CST 2022
```

getTime(): 调用system接口, 返回当前时间与GMT时间的以ms为单位的差值

setTime(long time): 设置对象的时间, 以ms为单位, 与new Date(time)作用相同

#### SimpleDateFormat

SimpleDateFormat类能将GMT偏差时间以固定格式打印

**构造方法**
无参构造, 格式为默认格式
```
SimpleDateFormat formatter = new SimpleDateFormat();
System.out.println(formatter.format(new Date().getTime()));
//2022/6/28 下午10:02
```
由用户自定义格式
首先需要了解一些占位符
```
y     年
M     年中的月份
D     年中的天数
d     月份中的天数
H     一天中的小时数（0-23）
h     am/pm 中的小时数（1-12）
m     小时中的分钟数
s     分钟中的秒数
S     毫秒数
```
传入字符串作为解析的格式
如
```
SimpleDateFormat formatter = new SimpleDateFormat("yyyy_MM_dd");
System.out.println(formatter.format(new Date().getTime()));
//2022_06_28
```

**format**
String format(time)
返回传入时间的格式化字符串

**applyPattern**
重设格式
```
SimpleDateFormat formatter = new SimpleDateFormat("yyyy_MM_dd");
formatter.applyPattern("MM-dd hh:mm");
System.out.println(formatter.format(new Date().getTime()));
//06-28 10:12
```

#### Calendar

Calendar是一个抽象类， 它为特定瞬间与一组诸如 YEAR、MONTH、DAY_OF_MONTH、HOUR 等日历字段之间的转换提供了一些方法，并为操作日历字段（例如获得下星期的日期）提供了一些方法

**创建对象**
Calendar是抽象的， 所以要通过多态来创建它子类的对象

Calendar中提供了静态方法用于自动生成日历对象
```
Calendar c = Calendar.getInstance();
```

**获取日历字段的值**
Calendar类中定义了一组常量来代表日历字段, 使用get方法可以获取指定字段的值
```
Calendar c = Calendar.getInstance();
System.out.println(c.get(Calendar.YEAR));//2022
System.out.println(c.get(Calendar.MONTH));//5
System.out.println(c.get(Calendar.DATE));//29
```
值得一提的是, Calendar中的月是从0开始的, 所以要加上1才是正常的月份

getTime方法将当前日历类转换为Date类
```
Calendar c = Calendar.getInstance();
System.out.println(c.getTime());
//Wed Jun 29 09:57:03 CST 2022
```

**设置日历的字段**
使用set设置一个或多个字段
```
Calendar c = Calendar.getInstance();
c.set(2012, 6, 6);//设置多个字段
c.set(Calendar.YEAR, 2099);//设置单个字段
System.out.println(c.getTime());
//Mon Jul 06 09:59:10 CST 2099
```
使用add对指定的字段进行增加或减小固定值
```
Calendar c = Calendar.getInstance();
c.add(Calendar.YEAR, -100);
System.out.println(c.getTime());
//Thu Jun 29 10:05:49 CST 1922
```


