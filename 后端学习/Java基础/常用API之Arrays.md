> 该类包含用于操作数组的各种方法（例如排序和搜索）。 此类还包含一个静态工厂，允许将数组视为列表。 

**toString**
将数组中的内容转换为一个字符串
```
int[] arr = {3, 8, 3, 2, 4};
System.out.println(Arrays.toString(arr));
//[3, 8, 3, 2, 4]
```
**sort()**
直接升序排序
```
int[] arr = {3, 8, 3, 2, 4};
Arrays.sort(arr);
System.out.println(Arrays.toString(arr));
//[2, 3, 3, 4, 8]
```
指定范围排序
```
int[] arr = {3, 8, 3, 2, 4};
Arrays.sort(arr, 1, 4);
System.out.println(Arrays.toString(arr));
//[3, 2, 3, 8, 4]
```

**fill()**
向数组填充特定值
```
int[] arr = new int[10];
Arrays.fill(arr, 100);
System.out.println(Arrays.toString(arr));
```


