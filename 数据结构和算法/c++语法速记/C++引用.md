引用可以看做是数据的一个别名，通过这个别名和原来的名字都能够找到这份数据。

```
int main() {
    int i = 100;
    int &j = i;
    cout << i << ", " << j << endl;//分别输出两个变量的值
    cout << &i << ", " << &j <<endl;//分别输出两个变量的地址
    return 0;
}
/*
100, 100
0x9d3ffffd94, 0x9d3ffffd94

*/

```
引用必须在定义的同时初始化，并且以后也要从一而终，不能再引用其它数据，这有点类似于常量（const 变量）。

常用引用作为函数形参以替代指针

```
void Swap(int &a, int &b){
    int temp = a;
    a = b;
    b = temp;
}

int main() {
    int i = 2, j = 3;
    cout << i << ", " << j << endl;
    Swap(i, j);
    cout << i << ", " << j << endl;
}
```
当不希望引用更改原始数据时, 可以用const修饰引用变量
```
int const &i = j;
或
const int &i = j;
```
引用也可以作为函数返回值, 但不能返回局部变量的引用

