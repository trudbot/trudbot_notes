#### 迭代器
**迭代器和 C++ 的指针非常类似**，它可以是需要的任意类型，通过迭代器可以指向容器中的某个元素，如果需要，还可以对该元素进行读/写操作。

1) 前向迭代器（forward iterator）
假设 p 是一个前向迭代器，则 p 支持 ++p，p++，*p 操作，还可以被复制或赋值，可以用 == 和 != 运算符进行比较。此外，两个正向迭代器可以互相赋值。

2) 双向迭代器（bidirectional iterator）
双向迭代器具有正向迭代器的全部功能，除此之外，假设 p 是一个双向迭代器，则还可以进行 --p 或者 p-- 操作（即一次向后移动一个位置）。

3) 随机访问迭代器（random access iterator）
随机访问迭代器具有双向迭代器的全部功能。除此之外，假设 p 是一个随机访问迭代器，i 是一个整型变量或常量，则 p 还支持以下操作：
p+=i：使得 p 往后移动 i 个元素。
p-=i：使得 p 往前移动 i 个元素。
p+i：返回 p 后面第 i 个元素的迭代器。
p-i：返回 p 前面第 i 个元素的迭代器。
p[i]：返回 p 后面第 i 个元素的引用。

此外，两个随机访问迭代器 p1、p2 还可以用 <、>、<=、>= 运算符进行比较。另外，表达式 p2-p1 也是有定义的，其返回值表示 p2 所指向元素和 p1 所指向元素的序号之差（也可以说是 p2 和 p1 之间的元素个数减一）。
|容器|迭代器类型|
|:-:|:-:|
array|	随机访问迭代器
vector|	随机访问迭代器
deque|	随机访问迭代器
list|	双向迭代器
set / multiset	|双向迭代器
map / multimap	|双向迭代器
forward_list	|前向迭代器
unordered_map / unordered_multimap|	前向迭代器
unordered_set / unordered_multiset|	前向迭代器
stack	|不支持迭代器
queue	|不支持迭代器

**迭代器的定义方法**
正向迭代器, 使用++会移动到下一个元素
```
容器名::iterator name;
```
逆向迭代器, 使用++会移动到上一个元素
```
容器名 ::reverse_iterator name;
```
常量迭代器, 只读权限的迭代器
```
容器名 :: const_iterator name;
容器名 :: const_reverse_iterator name;
```

# 序列式容器
* array<T,N>（数组容器）：表示可以存储 N 个 T 类型的元素，是 C++ 本身提供的一种容器。此类容器一旦建立，其长度就是固定不变的，这意味着不能增加或删除元素，只能改变某个元素的值；
* vector<T>（向量容器）：用来存放 T 类型的元素，是一个长度可变的序列容器，即在存储空间不足时，会自动申请更多的内存。使用此容器，在尾部增加或删除元素的效率最高（时间复杂度为 O(1) 常数阶），在其它位置插入或删除元素效率较差（时间复杂度为 O(n) 线性阶，其中 n 为容器中元素的个数）；
* deque<T>（双端队列容器）：和 vector 非常相似，区别在于使用该容器不仅尾部插入和删除元素高效，在头部插入或删除元素也同样高效，时间复杂度都是O(1)常数阶，但是在容器中某一位置处插入或删除元素，时间复杂度为 O(n) 线性阶；
* list<T>（链表容器）：是一个长度可变的、由 T 类型元素组成的序列，它以双向链表的形式组织元素，在这个序列的任何地方都可以高效地增加或删除元素（时间复杂度都为常数阶 O(1)），但访问容器中任意元素的速度要比前三种容器慢，这是因为 list<T> 必须从第一个元素或最后一个元素开始访问，需要沿着链表移动，直到到达想要的元素。
* forward_list<T>（正向链表容器）：和 list 容器非常类似，只不过它以单链表的形式组织元素，它内部的元素只能从第一个元素开始访问，是一类比链表容器快、更节省内存的容器。

**array——静态顺序表**
准备工作
```
#include <array>
using namespace std;
```
创建容器
```
array<int, 10> values;//只创建， array不会默认初始化
array<int, 10> values{};//创建并初始化
array<int, 10> values{1, 2, 3};//赋一部分值并初始化
```
成员函数
```
//返回始/末的随机访问迭代器
.begin()
.end()

.at(int n)//返回指定索引处元素的引用
.size()//长度
.empty()//是否为空, 注意empty和size考察的都是数组的容量而不是实际的元素个数
```
访问array
```
array<int, 10> values{};
int i;

//1
i = values[1];
//2
i = values.at(1);
//3
i = get<N>(values);//N必须为常量
```
**vector——动态顺序表**
```
vector<elemType>
```
定义格式
```
vector<int> arr;
vector<int> arr{1, 2, 3};
```
常用成员方法
```
.begin()
.end()
.size()
.push_back(elemType val)
.emplace_back(elemType val)和push_back类似， 但参数可以为空， 即可以加入一个初始化的元素
.clean()
```

**访问**
```
vector<int> arr{1, 2};
int i = arr[0];
int& j = arr.at(0);//返回某位置元素的引用

//返回首尾元素的引用
int& k = arr.front();
int& m = arr.back();
```
**提前申请空间**
如要创建一个行数为row, 列数为column的矩阵
```
int row = 4, column = 3;
vector<vector<int>> matrix;
matrix.resize(row);
for(int i=0; i<row; i++){
    matrix[i].resize(column);
}

cout<< matrix[2][2];//0
```
这样就得到了一个4*3矩阵， 且全初始化为0
# 关联式容器
**pair**
键值对的类模板， 存储一个键值对
```
pair<string, int> pair1{"hello", 100};
cout<< pair1.first << " " << pair1.second<< endl;//hello 100
pair1.first = "world";
pair1.second = 10;
cout<< pair1.first << " " << pair1.second<< endl;//world 10
```

**map**
map是pair的集合
```
#include <map>
using namespace std;
```
创建map
```
map<string, int> myMap;
或
map<string, int> myMap{{"hello", 100}, {"world", 200}};
```
遍历map
```
map<string, int> myMap{{"hello", 100}, {"world", 200}};
for(auto& i:myMap){
    cout<< i.first<<":"<<i.second << endl;
}
//或
for(auto i = myMap.begin(); i!=myMap.end(); i++){
    cout<< i->first << ":" << i->second << endl;
}
```

> 在使用 map 容器存储多个键值对时，该容器会自动根据各键值对的键的大小，按照既定的规则进行排序。

如键是字符串则为字典序, 为整型则为数值序,默认都是升序
```
map<string, int> m{{"B", 100}, {"C", 300}, {"A", 200}};

for(auto &i : m){
    cout<<"<" <<i.first<<", "<<i.second<<">"<<" ";
}

//<A, 200> <B, 100> <C, 300>
```

map由键获取值
```
map<string, int> m{{"B", 100}, {"C", 300}, {"A", 200}};

cout << m["A"] <<endl;//200
cout << m.at("B")<<endl;//100
```
当使用map[key]取值时, 若key不存在, 会转为在map中添加一个键值对<key, value>, value的值时值类型的默认值,如整型为0.而使用at查找失败则直接抛出异常

```
map<string, int> m{{"B", 100}, {"C", 300}, {"A", 200}};

map<string, int> m{{"B", 100}, {"C", 300}, {"A", 200}};

cout<< m["D"]<<endl;//0, 不存在"D"这个键所以添加了键值对<"D", 0>
m["E"] = 5;//创建新键值对
m["A"] = 101;//更改键值对的值
cout<< m["E"]<< endl<<m["A"]<<endl;//5, 101
```

插入新键值对
```
map<string, int> m;
//1
m[key] = value;
//2
m.insert(pair<string, int>{key, value});
//3
m.emplace("foo", 2000);
//注意2, 3插入的key必须不能和map已有的key重复
```
其它的常用方法
```
.count(key), 返回key在map中的出现次数, 只会是0, 1
.clear()
.erase(key), 删除指定键值对
.find(key), 返回指向key处的双向迭代器, 查找失败返回map.end()
```

**set**
* set和map的不同之处在于, 存储在set中的键值对, 它的键和值必须是同类型且值相等.
* 基于 set 容器的这种特性，当使用 set 容器存储键值对时，只需要为其提供各键值对中的 value 值（也就是 key 的值）即可。
* set同样会为数据继续排序.
* ，C++ 标准为了防止用户修改容器中元素的值，对所有可能会实现此操作的行为做了限制，使得在正常情况下，用户是无法做到修改 set 容器中元素的值的。


定义set
```
set<int> mySet{30, 20, 10};
set<int> mySet;
```

插入键值对
```
set<int> mySet;
mySet.insert(val);
//mySet.insert({val1, val2, val3...});
mySet.emplace(val);//两种方法仅插入一个元素效果相同, 但emplace效率更高
```

删除数据
```
.erase(val)
.clear()
```
# 哈希容器(无序关联式容器)
在无序容器中, 键值对是无序的, 存储位置取决于key

**unordered_map**
unordered_map和map大部分操作相同

当使用 [ ] 运算符向 unordered_map 容器中添加键值对时，分为 2 种情况：
* 当 [ ] 运算符位于赋值号（=）右侧时，则新添加键值对的键为 [ ] 运算符内的元素，其值为键值对要求的值类型的默认值（string 类型默认值为空字符串）；
* 当 [ ] 运算符位于赋值号（=）左侧时，则新添加键值对的键为 [ ] 运算符内的元素，其值为赋值号右侧的元素。

unordered\_map 类模板中，还提供有 at() 成员方法，和使用 [ ] 运算符一样，at() 成员方法也需要根据指定的键，才能从容器中找到该键对应的值；不同之处在于，如果在当前容器中查找失败，该方法不会向容器中添加新的键值对，而是直接抛出out\_of_range异常。

unordered_map也可以用迭代器遍历
通过 find() 方法得到的是一个正向迭代器，该迭代器的指向分以下 2 种情况：
* 当 find() 方法成功找到以指定元素作为键的键值对时，其返回的迭代器就指向该键值对；
* 当 find() 方法查找失败时，其返回的迭代器和 end() 方法返回的迭代器一样，指向容器中最后一个键值对之后的位置。

**栈和队列**
```
#include <stack>
using namespace std;
```
创建
```
stack<int> s;
```
入栈
```
s.push(val);
```
出栈
```
s.pop();//仅仅将栈顶元素删除, 无返回值
```
获取栈顶的值
```
s.top(); //返回栈顶元素的引用
```
其它
```
s.size();
s.empty();
s.swap(s1);//将s和s1的内容交换
s.emplace(val);
```

**queue**
```
#include <queue>
using namespace std;
```
empty()	如果 queue 中没有元素的话，返回 true。
size()	返回 queue 中元素的个数。
front()	返回 queue 中第一个元素的引用。如果 queue 是常量，就返回一个常引用；如果 queue 为空，返回值是未定义的。
back()	返回 queue 中最后一个元素的引用。如果 queue 是常量，就返回一个常引用；如果 queue 为空，返回值是未定义的。
push(const T& obj)	在 queue 的尾部添加一个元素的副本。这是通过调用底层容器的成员函数 push_back() 来完成的。
emplace()	在 queue 的尾部直接添加一个元素。
push(T&& obj)	以移动的方式在 queue 的尾部添加元素。这是通过调用底层容器的具有右值引用参数的成员函数 push_back() 来完成的。
pop()	删除 queue 中的第一个元素。
swap(queue<T> &other_queue)

**priority_queue**
优先队列, 函数与queue基本相同

```
//升序队列
priority_queue <int,vector<int>,greater<int> > q;
//降序队列
priority_queue <int,vector<int>,less<int> >q;

//greater和less是std实现的两个仿函数
//（就是使一个类的使用看上去像一个函数。
//其实现就是类中实现一个operator()，这个类就有了类似函数的行为，就是一个仿函数类了）
```

当使用基本数据类型的升序队列时, 
可直接定义
```
priority_queue<int> maxHeap;
```
用pair做优先队列元素的例子
```cpp
#include <iostream>
#include <queue>
#include <vector>
using namespace std;
int main() 
{
    priority_queue<pair<int, int> > a;
    pair<int, int> b(1, 2);
    pair<int, int> c(1, 3);
    pair<int, int> d(2, 5);
    a.push(d);
    a.push(c);
    a.push(b);
    while (!a.empty()) 
    {
        cout << a.top().first << ' ' << a.top().second << '\n';
        a.pop();
    }
}
```
```
2 5
1 3
1 2
```