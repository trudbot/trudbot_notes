需要包含头文件iostream
```
#include <iostream>
```
常用cin(输入)、cout(输出)， 它们都是iostream中提前创建好的对象
为了使用方便我们导入std命名空间
```
using namespace std;
```
**cout**
使用的格式是需要在输出的字符串前紧跟<<
如输出hello, world
```
cout<<"hello, world\n";
```
连续输出, 用多个<<就可以
```
cout<<"hello"<<", "<< "world" << "\n";
```
endl 表示end line， 可以用来代替"\n"
```
cout << "hello world" << endl;
```
同时cout和cin会自动分析数据的类型, 在使用时不需要考虑输出的数据类型.
```
int i = 100;
cout << i << endl;
```
**cin**
```
int main() {
    cout << "please enter a number and a string:" << endl;
    string str;
    int n;
    cin>> str;
    cout << "your input is " << "<" << n << "> " << "and " << str <<endl;
    cout << "end";
    return 0;
}
```
cin同样会根据接收数据的变量的类型的不同而执行不同的读取策略
要注意的是输入运算符>>在读入下一个输入项前会忽略前一项后面的空格


**cin.getline\(char\* buf, int len\);**
用于读取一行, buf为字符数组, len为最大读取长度

**cin.get();**
读入一个字符, 并返回

