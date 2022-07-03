## 1 List

在Collection中，List集合是有序的，Developer可对其中每个元素的插入位置进行精确地控制，可以通过索引来访问元素，遍历元素。

在List集合中，我们常用到ArrayList和LinkedList这两个类。

其中，ArrayList底层通过数组实现，随着元素的增加而动态扩容。而LinkedList底层通过链表来实现，随着元素的增加不断向链表的后端增加节点。

ArrayList是Java集合框架中使用最多的一个类，是一个数组队列，线程不安全集合。

它继承于AbstractList，实现了List, RandomAccess, Cloneable, Serializable接口。
 (1)ArrayList实现List，得到了List集合框架基础功能；
 (2)ArrayList实现RandomAccess，获得了快速随机访问存储元素的功能，RandomAccess是一个标记接口，没有任何方法；
 (3)ArrayList实现Cloneable，得到了clone()方法，可以实现克隆功能；
 (4)ArrayList实现Serializable，表示可以被序列化，通过序列化去传输，典型的应用就是hessian协议。

它具有如下特点：

- 容量不固定，随着容量的增加而动态扩容（阈值基本不会达到）
- 有序集合（插入的顺序==输出的顺序）
- 插入的元素可以为null
- 增删改查效率更高（相对于LinkedList来说）
- 线程不安全

数据结构：（JDK1.7）



![img](https:////upload-images.jianshu.io/upload_images/5621908-36ce970172e9c687.png?imageMogr2/auto-orient/strip|imageView2/2/w/933/format/webp)

LinkedList是一个双向链表，每一个节点都拥有指向前后节点的引用。相比于ArrayList来说，LinkedList的随机访问效率更低。

它继承AbstractSequentialList，实现了List, Deque, Cloneable, Serializable接口。
 (1)LinkedList实现List，得到了List集合框架基础功能；
 (2)LinkedList实现Deque，Deque 是一个双向队列，也就是既可以先入先出，又可以先入后出，说简单些就是既可以在头部添加元素，也可以在尾部添加元素；
 (3)LinkedList实现Cloneable，得到了clone()方法，可以实现克隆功能；
 (4)LinkedList实现Serializable，表示可以被序列化，通过序列化去传输，典型的应用就是hessian协议。

数据结构：（JDK1.7）



![img](https:////upload-images.jianshu.io/upload_images/5621908-3c2ee31c5af228ca.png?imageMogr2/auto-orient/strip|imageView2/2/w/1171/format/webp)

### 1.1 List常用方法



```tsx
A:添加功能
boolean add(E e):向集合中添加一个元素
void add(int index, E element):在指定位置添加元素
boolean addAll(Collection<? extends E> c)：向集合中添加一个集合的元素。
    
B:删除功能
void clear()：删除集合中的所有元素
E remove(int index)：根据指定索引删除元素，并把删除的元素返回
boolean remove(Object o)：从集合中删除指定的元素
boolean removeAll(Collection<?> c):从集合中删除一个指定的集合元素。

C:修改功能
E set(int index, E element):把指定索引位置的元素修改为指定的值，返回修改前的值。

D:获取功能
E get(int index)：获取指定位置的元素
Iterator iterator():就是用来获取集合中每一个元素。

E:判断功能
boolean isEmpty()：判断集合是否为空。
boolean contains(Object o)：判断集合中是否存在指定的元素。
boolean containsAll(Collection<?> c)：判断集合中是否存在指定的一个集合中的元素。

F:长度功能
int size():获取集合中的元素个数

G:把集合转换成数组
Object[] toArray():把集合变成数组。
```

### 1.2 ArrayList基本操作



```cpp
public class ArrayListTest {
    public static void main(String[] agrs){
        //创建ArrayList集合：
        List<String> list = new ArrayList<String>();
        System.out.println("ArrayList集合初始化容量："+list.size());

        //添加功能：
        list.add("Hello");
        list.add("world");
        list.add(2,"!");
        System.out.println("ArrayList当前容量："+list.size());

        //修改功能：
        list.set(0,"my");
        list.set(1,"name");
        System.out.println("ArrayList当前内容："+list.toString());

        //获取功能：
        String element = list.get(0);
        System.out.println(element);

        //迭代器遍历集合：(ArrayList实际的跌倒器是Itr对象)
        Iterator<String> iterator =  list.iterator();
        while(iterator.hasNext()){
            String next = iterator.next();
            System.out.println(next);
        }
        
        //for循环迭代集合：
        for(String str:list){
            System.out.println(str);
        }

        //判断功能：
        boolean isEmpty = list.isEmpty();
        boolean isContain = list.contains("my");

        //长度功能：
        int size = list.size();

        //把集合转换成数组：
        String[] strArray = list.toArray(new String[]{});

        //删除功能：
        list.remove(0);
        list.remove("world");
        list.clear();
        System.out.println("ArrayList当前容量："+list.size());
    }
}
```

### 1.3 LinkedList基本操作



```csharp
public class LinkedListTest {
    public static void main(String[] agrs){
        List<String> linkedList = new LinkedList<String>();
        System.out.println("LinkedList初始容量："+linkedList.size());

        //添加功能：
        linkedList.add("my");
        linkedList.add("name");
        linkedList.add("is");
        linkedList.add("jiaboyan");
        System.out.println("LinkedList当前容量："+ linkedList.size());

        //修改功能:
        linkedList.set(0,"hello");
        linkedList.set(1,"world");
        System.out.println("LinkedList当前内容："+ linkedList.toString());

        //获取功能：
        String element = linkedList.get(0);
        System.out.println(element);

        //遍历集合：(LinkedList实际的跌倒器是ListItr对象)
        Iterator<String> iterator =  linkedList.iterator();
        while(iterator.hasNext()){
            String next = iterator.next();
            System.out.println(next);
        }
        //for循环迭代集合：
        for(String str:linkedList){
            System.out.println(str);
        }

        //判断功能：
        boolean isEmpty = linkedList.isEmpty();
        boolean isContains = linkedList.contains("jiaboyan");

        //长度功能：
        int size = linkedList.size();

        //删除功能：
        linkedList.remove(0);
        linkedList.remove("jiaboyan");
        linkedList.clear();
        System.out.println("LinkedList当前容量：" + linkedList.size());
    }
}
```

### 1.4 ArrayList和LinkedList比较

（1）元素新增性能比较：

查看了网上很多的例子，很多都说，在新增操作时，ArrayList效率不如LinkedList，因为ArrayList底层是数组实现，在动态扩容时，性能有所损耗，而LinkedList不存在数组扩容机制，所以LinkedList效率更高。那么结果究竟怎样，来看下面的数据！



```csharp
public class ListTest {

    //迭代次数
    public static int ITERATION_NUM = 100000;

    public static void main(String[] agrs) {
        insertPerformanceCompare();
    }

    //新增性能比较：
    public static void insertPerformanceCompare() {
        Thread.sleep(5000);

        System.out.println("LinkedList新增测试开始");
        long start = System.nanoTime();
        List<Integer> linkedList = new LinkedList<Integer>();
        for (int x = 0; x < ITERATION_NUM; x++) {
            linkedList.add(x);
        }
        long end = System.nanoTime();
        System.out.println(end - start);

        System.out.println("ArrayList新增测试开始");
        start = System.nanoTime();
        List<Integer> arrayList = new ArrayList<Integer>();
        for (int x = 0; x < ITERATION_NUM; x++) {
            arrayList.add(x);
        }
        end = System.nanoTime();
        System.out.println(end - start);
    }
}
```

结果：

结果与预想的有些不太一样，ArrayList的新增性能并不低。

究其原因，可能是经过JDK近几年的更新发展，对于数组复制的实现进行了优化，以至于ArrayList的性能也得到了提高。

![img](https:////upload-images.jianshu.io/upload_images/5621908-38702eda9162d0b2.png?imageMogr2/auto-orient/strip|imageView2/2/w/913/format/webp)

（2）元素获取比较：

由于LinkedList是链表结构，没有角标的概念，没有实现RandomAccess接口，不具备随机元素访问功能，所以在get方面表现的差强人意，ArrayList再一次完胜。



```csharp
public class ListTest {

    //迭代次数，集合大小：
    public static int ITERATION_NUM = 100000;

    public static void main(String[] agrs) {
        getPerformanceCompare();
    }

    //获取性能比较：
    public static void getPerformanceCompare() {
        Thread.sleep(5000);
        
        //填充ArrayList集合：
        List<Integer> arrayList = new ArrayList<Integer>();
        for (int x = 0; x < ITERATION_NUM; x++) {
            arrayList.add(x);
        }

        //填充LinkedList集合：
        List<Integer> linkedList = new LinkedList<Integer>();
        for (int x = 0; x < ITERATION_NUM; x++) {
            linkedList.add(x);
        }

        //创建随机数对象：
        Random random = new Random();

        System.out.println("LinkedList获取测试开始");
        long start = System.nanoTime();
        for (int x = 0; x < ITERATION_NUM; x++) {
            int j = random.nextInt(x + 1);
            int k = linkedList.get(j);
        }
        long end = System.nanoTime();
        System.out.println(end - start);

        System.out.println("ArrayList获取测试开始");
        start = System.nanoTime();
        for (int x = 0; x < ITERATION_NUM; x++) {
            int j = random.nextInt(x + 1);
            int k = arrayList.get(j);
        }
        end = System.nanoTime();
        System.out.println(end - start);
    }
}
```

结果：

从结果中可以看到，ArrayList在随机访问方面表现的十分优秀，比LinkedList强了很多，基本上保持在10多倍以上。