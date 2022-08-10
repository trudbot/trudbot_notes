**导包**
```
import java.util.HashMap;
```
**HashMap类定义**
```
HashMap<K, V>
```
K是键的类型
V是值的类型

**new对象**
如
```
HashMap<String, Integer> hash = new HashMap<>();
```

**增加键值对**
```
hash.put("hello", 100);
```
更新键值对的值时也是用put, 此时put会返回原来的值
**根据键取值**
```
V get(K key);

如
int value = hash.get("hello");
```

**是否存在某个键**
```
boolean containsKey(K key);
```

**是否存在某个值**
```
boolean containsValue(V value);
```

**哈希表是否为空**
```
boolean isEmpty();
```

**删除键值对**
```
V remove(K key);
```
返回所删除键值对的值

**哈希表中键值对个数**
```
int size();
```



