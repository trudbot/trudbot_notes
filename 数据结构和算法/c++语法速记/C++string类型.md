需要包含头文件string
```
#include <string>
```

**复制操作**
形如
```
str1 = str2;
```
表示把str2的内容复制到str1
如
```
int main() {
    string str = "hello world";
    cout << str << endl;
}
```
**连接操作**
```str3 = str1 + str2```
将str1 和str2首尾相连并复制到str3
同时字符串也可以直接加字符类型
```
str += 'A';
```

**长度**
```str.size();```或 ```str.length();```

如
```
int main() {
    string str1 = "abc", str2 = "edf";
    str1 = str1 + str2;
    cout << str1+", " << str1.size() << endl;
}
//abcedf, 6

```
**比较**
直接使用==, != , < , > , <= , >=来比较两个字符串,
```
int main() {
    string str1 = "abc", str2 = "edf";
    bool flag = str1 < str2;
    cout << flag;
}

```
**随机访问**
```
int main() {
    string str = "abcdef";
    for(int i=0; i<str.length(); i++){
        cout << str[i] << " ";
    }
}
```
也支持foreach
```
int main() {
    string str = "abcdef";
    for(char i : str){
        cout << i << " ";
    }
}
```
```
a b c d e f
```

**是否为空**
```str.empty();```
**读入一整行**
cin中读入字符串类似于scanf, 遇空格回车tab都会结束
使用getline读入一整行
```
getline(cin, str);
```

