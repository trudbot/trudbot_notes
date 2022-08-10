**对容器的排序**
sort(first, last);
对容器[first, last)范围进行排序
stable_sort(first, last);//稳定排序

first和last必须为随机访问迭代器, 所以只支持普通数组和array、vector和dequeue。
对普通数组进行排序
```
int main() {
    int arr[] = {3, 1, 2, -1};
    sort(arr, arr+4);
    for(int i : arr){
        cout<< i << " ";
    }
}
//-1 1 2 3
```
对容器进行排序
```
int main() {
    vector<int> arr{3, 8, 3, 2, 4};
    sort(arr.begin(), arr.end());
    for(int i : arr){
        cout<< i << " ";
    }
}
//2 3 3 4 8
```

**二分查找**



