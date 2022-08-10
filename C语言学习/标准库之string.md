**常用函数**

strcpy(str1, str2); 将str2赋值给str1

strcat(str1, str2); 将str2拼接到str1后

strlen(str); 获取字符串长度

```
# include <stdio.h>
# include <string.h>

int main(void)
{
    char a[100], b[100];
    strcpy(a, "hello");
    strcpy(b, a);
    
    printf("a = \"%s\", b = \"%s\"\n", a, b);
    //a = "hello", b = "hello"
    
    strcat(b, a);
    printf("len(b) = %d\n", strlen(b));
    //len(b) = 10
    
    printf("%s", b);//hellohello
    
    return 0;
}

```
strcmp(str1, str2);
string compare
比较两个字符串，{
    str1与str2相同， 返回0
    str1小于str2， 返回负数
    str1大于str2， 返回正数
}
