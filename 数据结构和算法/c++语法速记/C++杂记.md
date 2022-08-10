**数组初始化**
* 静态区的bool数组, 自动初始化为全false
* 静态区的int数组, 自动初始化为0
*bool 数组初始化*
```
全false
bool arr[100] = {0};

全true
boo arr[100];
memset(arr, 1, sizeof arr);
```

*int 数组初始化*
使用memset对int数组进行初始化时, 一般只初始化0或-1, 因为memset是按字节拷贝的

以及较为特殊的
```
int arr[20];
//初始化为一个非常大的值(0x3f3f3f3f), 与int的上限同一个数量级
memset(arr, 0x3f, sizeof arr);
```

