HashSet 基于 HashMap 来实现的，是一个**不允许有重复元素**的集合。

HashSet 允许有 null 值。

HashSet 是无序的，即不会记录插入的顺序。

### 初始化：

```java
HashSet<String> sites = new HashSet<String>();
```

### 判断元素是否存在

我们可以使用 contains() 方法来判断元素是否存在于集合当中:

```java
System.out.println(sites.contains("Taobao"));
```



remove();

clear();

size();