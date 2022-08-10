> cin在为了与scanf保持同步，设置了一个缓冲区，为了保证各位混用两者的情况不会出错，利用这个缓冲区进行同步，不至于发生指针错误造成乱码，因此cin会牺牲一点点效率，而这一点点的效率，在大数据读取和运算的时候也会产生极大的影响，我们可以通过sync_with_stdio(false)的方式取消这个缓冲区，让cin变成和scanf一样的效率。

```
ios_base::sync_with_stdio(false);
```



解除cin与cout的绑定
```
cin.tie(NULL);
cout.tie(NULL);
```

