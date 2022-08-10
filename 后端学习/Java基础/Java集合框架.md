数组与集合的区别如下：
1. 数组长度不可变化而且无法保存具有映射关系的数据；集合类用于保存数量不确定的数据，以及保存具有映射关系的数据。

2. 数组元素既可以是基本类型的值，也可以是对象；集合只能保存对象。

Java中的集合分为单列集合以及双列集合(存储映射), 分别对应Collection接口和Map接口.

## Collection接口

单列集合中又有三个继承了Collection的子接口, 分别是List、Queue和Set， 即有序集合、队列集合和无序集合
![单列集合](https://note.youdao.com/yws/res/8083/WEBRESOURCEde069742ab0d7be76fc0c54d412b738d)

**Collection中的常见方法**
返回值类型|方法名及参数| 解释
:-:|:-:|:-:
boolean| add(E e) |确保此集合包含指定的元素（可选操作）。  
boolean |addAll(Collection<? extends E> c)| 将指定集合中的所有元素添加到此集合中（可选操作）。  
void| clear()| 从此集合中删除所有元素（可选操作）。  
boolean |contains(Object o)| 如果此collection包含指定的元素，则返回 true 。  
boolean |containsAll(Collection<?> c)| 如果此集合包含指定集合中的所有元素，则返回 true 。  
boolean| equals(Object o)| 将指定对象与此集合进行比较以获得相等性。 
int |hashCode() |返回此集合的哈希码值。  
boolean| isEmpty() |如果此集合不包含任何元素，则返回 true 。  
Iterator<E>| iterator() |返回此集合中元素的迭代器。  
boolean |remove(Object o)| 从此集合中移除指定元素的单个实例（如果存在）（可选操作）。  
boolean| removeAll(Collection<?> c)| 删除此集合的所有元素，这些元素也包含在指定的集合中（可选操作）。  
boolean| retainAll(Collection<?> c)| 仅保留此集合中包含在指定集合中的元素（可选操作）。  
int |size() |返回此集合中的元素数。  
Object[]| toArray()| 返回包含此集合中所有元素的数组。  

**Collection的迭代器遍历**
Collection的实现类获取元素的方法各有不同， 但相同的是它们都继承了Collection接口的迭代器方法， 所以我们都可以用迭代器来遍历它们。

我们先以多态的方式创建一个元素类型为Integer的ArrayList对象
```
Collection<Integer> arr = new ArrayList<>();
```

用Collection接口中的iterator方法返回迭代器, 并用相同类型的迭代器接口变量接收
```
Iterator<Integer> i = arr.iterator();
```
iterator接口中的方法hasNext返回后面是否还有元素的Boolean值, next方法将当前迭代器向后移并且返回元素值. 
注意最开始迭代器指向第一个元素的前一个位置.
由此我们可以对Collection进行遍历
```
public static void main(String[] args) {
    Collection<Integer> arr = new ArrayList<>();
    arr.add(10);
    arr.add(20);
    arr.add(30);
    Iterator<Integer> i = arr.iterator();
    while(i.hasNext()) {
        System.out.println(i.next());
    }
}
/*
10
20
30

*/
```
在idea中使用快捷键itit+回车可以快速生成迭代器遍历循环

**并发修改异常**
当在使用迭代器来访问Collection中的元素时, 如果对Collection进行了修改(增加或删除元素), 就会引发并发修改异常.

因为在迭代器的next的方法中会对集合更改次数做判断, 判断是否等于遍历前的次数, 否则抛出异常

**Collection的foreach遍历**
如
```
    public static void main(String[] args) {
        TreeSet<String> set = new TreeSet<>();
        set.add("hello"); set.add("world"); set.add("java");

        for (String s : set) {
            if(s.equals("hello")) {
                System.out.println("Yes");
                break;
            }
        }
    }
```
在idea中使用快捷键I+回车可以快速生成foreach

foreach循环的内部原理其实仍然是一个迭代器, 所以不能在foreach循环途中对集合进行更改

#### List接口
List集合代表一个有序、可重复集合，集合中每个元素都有其对应的顺序索引。List集合默认按照元素的添加顺序设置元素的索引，可以通过索引（类似数组的下标）来访问指定位置的集合元素。

**List接口特有的方法**
返回值类型|方法名及参数|描述
:-:|:-:|:-:
void|add(int index, E elem) |在指定位置插入元素
E | remove(int index)|删除并返回指定位置的元素
E | set(int index, E elem) | 修改指定位置的元素并返回原来的值
E | get(int index) | 获取指定位置的元素

**List特有的遍历方式**
因为List中每一个元素都有其对应的索引, 所以可以通过索引来遍历List
```
public static void main(String[] args) {
    List list = new Vector<Integer>();
    list.add(1); list.add(2); list.add(3);

    for(int i=0; i<list.size(); i++)
        System.out.print(list.get(i) + " ");
}
```

**List专属迭代器**
```
public static void main(String[] args) {
    List list = new ArrayList<Integer>();
    list.add(1); list.add(2); list.add(3);

    ListIterator<Integer> listIterator = list.listIterator();
    while (listIterator.hasNext()) {
        Integer next = listIterator.next();
        System.out.print(next + " ");
    }
    System.out.println("\n----------------");
    while (listIterator.hasPrevious()) {
        Integer next =  listIterator.previous();
        System.out.print(next + " ");
    }
}
/*
1 2 3 
----------------
3 2 1 
*/
```
ListIterator中有add以及set方法,  使用迭代器中的方法改变集合中的元素不会导致并发修改异常

**Stack API**
Stack继承自Vector
```
.push(E e), 将元素e压栈, 并返回元素e
.pop(E e), 删除栈顶元素, 并返回
.empty(), 栈是否为空
.peek(), 返回栈顶元素
```
**线性表**
ArrayList：顺序表
LinkedList: 双向链表

成员方法基本相同
ArrayList查找效率高
LinkedList增删效率高

**LinkedList特有方法**
由于LinkedList是双向链表， 因此对两端的操作较为方便
```
getLast
getFirst
addFirst
addLast
removeFirst
removeLast
```

#### Set接口
Set集合的特点是元素不可重复, 且不支持随机访问

**HashSet**
顾名思义, HashSet通过哈希值来确定元素的存储位置, 是最常用的Set实现类
```
add
clear
contains
isEmpty
remove
size
iterator
```

**LinkedHashSet**
LinkedHashSet是HashSet的一个子类，具有HashSet的特性，也是根据元素的hashCode值来决定元素的存储位置。但它使用链表维护元素的次序，元素的顺序与添加顺序一致。由于LinkedHashSet需要维护元素的插入顺序，因此性能略低于HashSet，但在迭代访问Set里的全部元素时有很好的性能

**TreeSet**
TreeSet是预排序的集合, 类似于C++中的set, 底层实现是红黑树.

TreeSet排序方式分为自然排序和定制排序, 
* 使用无参构造方法创建TreeSet对象时, 使用自然排序
自然排序状态下, 如果试图将一个对象添加到TreeSet集合中，则该对象必须实现Comparable接口，否则会抛出异常。

Java常用类中已经实现了Comparable接口的类有以下几个：
```
♦ BigDecimal、BigDecimal以及所有数值型对应的**包装类**：按照它们对应的数值大小进行比较。

♦ Charchter：按照字符的unicode值进行比较。

♦ Boolean：true对应的包装类实例大于false对应的包装类实例。

♦ String：按照字符串中的字符的unicode值进行比较。

♦ Date、Time：后面的时间、日期比前面的时间、日期大。

```
* 另一种方法是, 创建TreeSet对象时传入Comparator


*以下一个学生类来实现Comparable接口*
```
public class Student implements Comparable<Student>{
    int score;
    String name;

    public Student(int score, String name) {
        this.score = score;
        this.name = name;
    }

    @Override
    public int compareTo(Student stu) {
        return this.score < stu.score ? -1 : 1;
    }

    public void Show() {
        System.out.println("姓名: " + this.name + ", 分数: " + this.score);
    }
}
```
注意compareTo若返回0, TreeSet认为这两个对象是相等的, 则旧对象会被覆盖为新对象.
若要控制为正常稳定的升序, 当前对象关键值小时应返回-1, 否则返回1
以下时测试类的实现
```
public class TEST {

    public static void main(String[] args) {
        TreeSet<Student> treeSet = new TreeSet<>();
        treeSet.add(new Student(100, "张三"));
        treeSet.add(new Student(80, "李四"));
        treeSet.add(new Student(90, "王五"));
        treeSet.add(new Student(90, "赵六"));

        for (Student student : treeSet) {
            student.Show();
        }

    }
}
/*
姓名: 李四, 分数: 80
姓名: 王五, 分数: 90
姓名: 赵六, 分数: 90
姓名: 张三, 分数: 100

*/
```

*以下通过实现Comparator接口来完成相同的功能*
创建类Human作为示例的类
```
public class Human {
    private int age;
    private String name;

    public Human(int age, String name) {
        this.age = age;
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public String getName() {
        return name;
    }
}
```
使用匿名类实现Comparator接口, 只需实现其中的compare方法即可
```
public class TEST {

    public static void main(String[] args) {
        Comparator<Human> HumanComparator= new Comparator<Human>(){
            @Override
            public int compare(Human o1, Human o2) {
                return o1.getAge() < o2.getAge() ? -1 : 1;
            }
        };

        TreeSet<Human> treeSet = new TreeSet<>(HumanComparator);
        treeSet.add(new Human(18, "张三"));
        treeSet.add(new Human(15, "李四"));
        treeSet.add(new Human(20, "王五"));
        treeSet.add(new Human(15, "赵六"));

        for (Human human : treeSet) {
            System.out.println(human.getName() + " " + human.getAge());
        }
    }
}
/*
李四 15
赵六 15
张三 18
王五 20

*/

```

#### Map接口

Map是键值对的集合， 其中键不能重复

**Map接口中定义的方法**
```
.clear() //清空集合
.containsKey(K key) //是否存在指定键
.isEmpty() //集合是否为空
.keySet() //返回键集合, 用Set接口多态接收
.values() //返回值的collection集合形式
.put(K key, V value) //若集合中不存在key则增加键值对{key, value}, 存在则将key对应的值更新为value
.get(K key) //返回传入键对应的值, 不存在则返回null
.remove(K k) //删除键值对
.size() //返回键值对个数
```

**Map常用的实现类**
HashMap, 通过哈希表实现
TreeMap, TreeMap继承了Map的子接口SortedMap, 由红黑树实现, 同TreeSet, 分为自然排序和定制排序

##### Map的遍历
以如下Map举例
```
Map<String, Integer> map = new HashMap<>();
map.put("one", 1);
map.put("two", 2);
map.put("three", 3);
```
**只遍历键或值**
foreach遍历keySet或valueCollection即可
```
for (String s : map.keySet()) {
    System.out.print(s + " ");
}
System.out.println();
for (Integer integer : map.values()) {
    System.out.print(integer + " ");
}

/*
one two three 
1 2 3 
*/
```
**通过键获取值来遍历键值对**
效率较低, 不建议使用
```
for(String s : map.keySet())  {
    System.out.println(s + " " + map.get(s));
}
/*
one 1
two 2
three 3

*/
```
**通过entry遍历键值对**
Map接口中有一个内部接口Entry<K, V>, 它用于保存Map中键值对的映射.

使用Map中的方法entrySet可以获取所有键值对的映射的集合
方法为
```
Set<Map.Entry<K, V>> entrySet();
```

entry接口中常用方法为
```
.getKey() //获取键值对的键
.getValue() //获取键值对的值
.setValue(V val) //将当前键值对的值更新, 并返回原值
```
使用set接收
```
Set<Map.Entry<String, Integer>> entrySet = map.entrySet();
```

使用foreach遍历
```
for(Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " " + entry.getValue());
}
/*
one 1
two 2
three 3

*/
```
同Map.Entry遍历, 可以在遍历的时候更新值, 但不能增删键值对
