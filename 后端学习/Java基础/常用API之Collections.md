封装了一些对集合的算法, 其中方法都通过类名调用

> 此类仅包含对集合进行操作或返回集合的静态方法。 它包含对集合进行操作的多态算法，“包装器”，它返回由指定集合支持的新集合，以及其他一些可能性和结束。 
如果提供给它们的集合或类对象为null，则此类的方法都抛出NullPointerException 。 

### 常用方法
对集合排序, 求集合中的最大最小值
集合中元素类需实现Comparable接口或在调用时传入对应的Comparator的实现类
```
Collections.sort(collection, comparator)
Collections.max(collection, comparator)
Collections.min(collection, comparator)

```


将List中的元素反转
```
reverse(List<?> list)
```