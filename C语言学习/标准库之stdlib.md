stdlib.h是一个通用工具库, 里面有许多工具函数.

stdlib.h中有内存动态分配函数(malloc等).

**其它或许有用的函数**

abort():无参数无返回值, 使一个程序以异常的形式终止.
exit(n): 以正常的形式终止程序,返回n(一般写0)
system(str): 在windows中相当于在cmd界面输入str执行

*(伪)随机数生成*

rand(): 无参无返,根据随机数种子生成0~RAND_MAX之间的一个数, RANSD_MAX(很大)在头文件中被声明.
srand(n): 参数n类型为无符号整数,将n设为随机数种子,当没有设置种子时调用rand(),种子默认为1.

示例:生成1~100的随机数
```
# include <stdio.h>
# include <stdlib.h>
# include <time.h>


int randint(void)
{
    return rand()%100 + 1; //一个数num%i的结果一定是0~(i-1)
}

int main(void)
{
    srand((unsigned int)time(NULL)); //设置程序开始运行时的时间为种子
    
    for (int i=1; i<=5; i++)
        printf("%d\t", randint());
        
    return 0;
}
/*
运行三次:
71      92      25      53      59
1       92      63      15      87
90      59      87      35      43
*/
```

