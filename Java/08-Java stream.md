#  Java中的数据结构

## 1.时间复杂度

- O(1)- (不管数据大小)数组的存取
- O(logn)-二分查找
- O(n)- (线性增长) 遍历数组
- O(n2)-(数据越多)冒泡排序ｗｄａｗｄａｄａｗｄａ
- O(n!)-n的阶层



![image-20220608143524895](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181209730.png)

## 2.ArrayList底层原理

> java语言只提供了数组
>
> ArrayList 不是java提供的是jdk发包提供的,java语言的编写的一个类

数组的长度是固定的,

arraylist是


## 3.LinkedList底层原理

```

```



## 4.Tree树形结构

```
public class TreeTest{
    public static void main(String[] args){

    }



    /**
     * TODO: 遍历树状节点
     *
     * @param node {@link Node}
     **/
    private void findAll(Node node){
        if (node.left != null) {
            findAll(node.left);
        }
        if (node.right != null) {
            findAll(node.right);
        }
        System.out.println(node);
    }

    /**
     * TODO: 创建一个树状链式结构
     *
     * @return {@link Node}
     **/
    private Node createNode(){
        Node node9 = new Node(9);
        Node node8 = new Node(8);
        Node node7 = new Node(7);
        Node node6 = new Node(6);
        Node node5 = new Node(5);
        Node node4 = new Node(4);
        Node node3 = new Node(3);
        Node node2 = new Node(2);

        node5.left = node3;
        node5.right = node8;

        node3.left = node2;
        node3.right = node4;

        node8.left = node6;
        node6.right = node7;

        node8.right = node9;

        node5.right = node9;
        return node5;
    }

    /**
     * 树状
     */
    @Data
    @Accessors(chain = true)
    class Node{
        int value;
        Node left;
        Node right;

        public Node(int value){
            this.value = value;
        }
    }
}
```

![image-20220616133623727](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181210490.png)

## 5.Hash算法源码

![image-20220609134649208](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181210052.png)

## 6.HashMap

```
        Map <String,String >stringMap5=new TreeMap<>();

        Map <String,String >stringMap2=new LinkedHashMap<>();

        Map <String,String >stringMap1=new HashMap<>();

        Map <String,String >stringMap4=new Hashtable<>();
        Map <String,String >stringMap3=new ConcurrentHashMap<>();

public interface NavigableMap<K,V> extends SortedMap<K,V> {

    //返回小于key的第一个元素：
    Map.Entry<K,V> lowerEntry(K key);

    //返回小于key的第一个键：
    K lowerKey(K key);

    //返回小于等于key的第一个元素：
    Map.Entry<K,V> floorEntry(K key);

    //返回小于等于key的第一个键：
    K floorKey(K key);

    //返回大于或者等于key的第一个元素：
    Map.Entry<K,V> ceilingEntry(K key);

    //返回大于或者等于key的第一个键：
    K ceilingKey(K key);

    //返回大于key的第一个元素：
    Map.Entry<K,V> higherEntry(K key);

    //返回大于key的第一个键：
    K higherKey(K key);

    //返回集合中第一个元素：
    Map.Entry<K,V> firstEntry();

    //返回集合中最后一个元素：
    Map.Entry<K,V> lastEntry();

    //返回集合中第一个元素，并从集合中删除：
    Map.Entry<K,V> pollFirstEntry();

    //返回集合中最后一个元素，并从集合中删除：
    Map.Entry<K,V> pollLastEntry();

    //返回倒序的Map集合：
    java.util.NavigableMap<K,V> descendingMap();

    NavigableSet<K> navigableKeySet();

    //返回Map集合中倒序的Key组成的Set集合：
    NavigableSet<K> descendingKeySet();

    java.util.NavigableMap<K,V> subMap(K fromKey, boolean fromInclusive,
                                       K toKey, boolean toInclusive);

    java.util.NavigableMap<K,V> headMap(K toKey, boolean inclusive);

    java.util.NavigableMap<K,V> tailMap(K fromKey, boolean inclusive);

    SortedMap<K,V> subMap(K fromKey, K toKey);

    SortedMap<K,V> headMap(K toKey);

    SortedMap<K,V> tailMap(K fromKey);
}
```



## 7.ConcurrentHashMap

![image-20220609161312145](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181210021.png)

![image-20220609161327372](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181210270.png)

## 8.Java集合框架组成

> Arrays and collections

这个类包含各种操作数组的方法(比如排序和搜索)。这个类还包含一个静态工厂，允许将数组视为列表。

如果指定的数组引用为空，这个类中的方法都会抛出NullPointerException，除非特别注明。

这个类中包含的方法的文档包含了实现的简要描述。这样的描述应该被视为实现注释，而不是规范的一部分。实现者应该可以自由地替换其他算法，只要规范本身得到遵守。(例如，sort(Object[])使用的算法不一定是MergeSort，但它必须是稳定的。)

这个类是Java集合框架的成员。

一种比较器，实现一组相互比较的元素的自然排序。当提供的比较器为空时可以使用。为了简化底层实现中的代码共享，compare方法只为它的第二个参数声明Object类型。数组类实现者的注释:与使用这个比较器的TimSort相比，ComparableTimSort是否提供了任何性能优势，这是一个经验问题。如果不是，你最好删除或绕过ComparableTimSort。目前还没有将它们分开进行并行排序的经验案例，所以所有公共Object parallelSort方法都使用相同的基于比较器的实现。





![image-20220609161613617](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181210591.png)

## 9.接口继承关系和实现

集合类存放于 Java.util 包中，主要有 3 种：set(集）、list(列表包含 Queue）和 map(映射)。

> 1. Collection：Collection 是集合 List、Set、Queue 的最基本的接口。
> 2. Iterator：迭代器，可以通过迭代器遍历集合中的数据
> 3. Map：是映射表的基础接口

![image-20220602095719883](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181210230.png)

### List

Java 的 List 是非常常用的数据类型。List 是有序的 Collection。Java List 一共三个实现类：

> 分别是ArrayList、Vector 和 LinkedList。  

![image-20220602095659090](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181210283.png)

**ArrayList（数组）**

ArrayList 是最常用的 List 实现类，内部是通过数组实现的，它允许对元素进行快速随机访问。数组的缺
点是每个元素之间不能有间隔，当数组大小不满足时需要增加存储能力，就要将已经有数组的数据复制
到新的存储空间中。当从 ArrayList 的中间位置插入或者删除元素时，需要对数组进行复制、移动、代
价比较高。因此，它适合随机查找和遍历，不适合插入和删除。



**Vector（数组实现、线程同步）**

Vector 与 ArrayList 一样，也是通过数组实现的，不同的是它支持线程的同步，即某一时刻只有一
个线程能够写 Vector，避免多线程同时写而引起的不一致性，但实现同步需要很高的花费，因此，访问
它比访问 ArrayList 慢。



**LinkList（链表）**

LinkedList 是用链表结构存储数据的，很适合数据的动态插入和删除，随机访问和遍历速度比较慢。另
外，他还提供了 List 接口中没有定义的方法，专门用于操作表头和表尾元素，可以当作堆栈、队列和双
向队列使用。  



### Set

Set 注重独一无二的性质,该体系集合用于存储无序(存入和取出的顺序不一定相同)元素，值不能重复。

> 对象的相等性本质是对象 hashCode 值（java 是依据对象的内存地址计算出的此序号）判断的，如果想要
> 让两个不同的对象视为相等的，就必须覆盖 Object 的 hashCode 方法和 equals 方法。  

![image-20220602100045799](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181211313.png)

####  **HashSet（Hash 表）**

哈希表边存放的是哈希值。HashSet 存储元素的顺序并不是按照存入时的顺序（和 List 显然不同） 而是
按照哈希值来存的所以取数据也是按照哈希值取得。

>元素的哈希值是通过元素的hashcode 方法来获取的, HashSet 首先判断两个元素的哈希值，如果哈希值一样，接着会比较equals 方法 如果 equls 结果为
>true ，HashSet 就视为同一个元素。如果 equals 为 false 就不是同一个元素。

哈希值相同 equals 为 false 的元素是怎么存储呢,就是在同样的哈希值下顺延（可以认为哈希值相同的元
素放在一个哈希桶中）。也就是哈希一样的存一列。如图 1 表示 hashCode 值不相同的情况；图 2 表示
hashCode 值相同，但 equals 不相同的情况。  

![image-20220602100355859](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181211434.png)

> HashSet 通过 hashCode 值来确定元素在内存中的位置。一个 hashCode 位置上可以存放多个元素  

#### **TreeSet（二叉树）**

> 1. TreeSet()是使用二叉树的原理对新 add()的对象按照指定的顺序排序（升序、降序），每增加一个
>    对象都会进行排序，将对象插入的二叉树指定的位置。
>
> 2. Integer 和 String 对象都可以进行默认的 TreeSet 排序，而自定义类的对象是不可以的，自己定义
>    的类必须实现 Comparable 接口，并且覆写相应的 compareTo()函数，才可以正常使用。
>
> 3. 在覆写 compare()函数时，要返回相应的值才能使 TreeSet 按照一定的规则来排序
>
> 4. 比较此对象与指定对象的顺序。如果该对象小于、等于或大于指定对象，则分别返回负整数、零或
>    正整数。  

#### **LinkedHashSet（HashSet+LinkedHashMap）**

对于 LinkedHashSet 而言，它继承与 HashSet、又基于 LinkedHashMap 来实现的。
LinkedHashSet 底层使用 LinkedHashMap 来保存所有元素，它继承与 HashSet，其所有的方法操作上
又与 HashSet 相同，因此 LinkedHashSet 的实现上非常简单，只提供了四个构造方法，并通过传递一
个标识参数，调用父类的构造器，底层构造一个 LinkedHashMap 来实现，在相关操作上与父类
HashSet 的操作相同，直接调用父类 HashSet 的方法即可。  

### Map

![image-20220602102159931](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181211783.png)

#### HashMap（数组+链表+红黑树）

HashMap 根据键的 hashCode 值存储数据，大多数情况下可以直接定位到它的值，因而具有很快的访问速度，但遍历顺序却是不确定的。 HashMap最多只允许一条记录的键为null，允许多条记录的值为null。HashMap 非线程安全，即任一时刻可以有多个线程同时写 HashMap，可能会导致数据的不一致。如果需要满足线程安全，可以用 Collections 的 synchronizedMap 方法使 HashMap 具有线程安全的能力，或者使用 ConcurrentHashMap。我们用下面这张图来介绍HashMap 的结构。  

#### JAVA7 实现  

![image-20220602102324378](assets/image-20220602102324378.png)

大方向上，HashMap 里面是一个数组，然后数组中每个元素是一个单向链表。上图中，每个绿色的实体是嵌套类 Entry 的实例，Entry 包含四个属性：key, value, hash 值和用于单向链表的 next。

1. capacity：当前数组容量，始终保持 2^n，可以扩容，扩容后数组大小为当前的 2 倍。

2. loadFactor：负载因子，默认为 0.75。  

3. threshold：扩容的阈值，等于 capacity * loadFactor  

#### JAVA8实现

Java8 对 HashMap 进行了一些修改，最大的不同就是利用了红黑树，所以其由 数组+链表+红黑树 组成。
根据 Java7 HashMap 的介绍，我们知道，查找的时候，根据 hash 值我们能够快速定位到数组的具体下标，但是之后的话，需要顺着链表一个个比较下去才能找到我们需要的，时间复杂度取决于链表的长度，为 O(n)。为了降低这部分的开销，在 Java8 中，当链表中的元素超过了 8 个以后，会将链表转换为红黑树，在这些位置进行查找的时候可以降低时间复杂度为 O(logN)。  

![image-20220602103027613](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181211349.png)ConcurrentHashMap

**Segment 段**
ConcurrentHashMap 和 HashMap 思路是差不多的，但是因为它支持并发操作，所以要复杂一些。整个 ConcurrentHashMap 由一个个 Segment 组成，Segment 代表”部分“或”一段“的意思，所以很多地方都会将其描述为分段锁。注意，行文中，我很多地方用了“槽”来代表一个 segment。
**线程安全（Segment 继承 ReentrantLock 加锁）**



简单理解就是，ConcurrentHashMap 是一个 Segment 数组，Segment 通过继承 ReentrantLock 来进行加锁，所以每次需要加锁的操作锁住的是一个 segment，这样只要保证每个 Segment 是线程安全的，也就实现了全局的线程安全。  



# Collections和Arrays

## [Collections工具类](https://www.cnblogs.com/fysola/p/6021134.html)

### 排序操作

Collections提供以下方法对List进行排序操作

void reverse(List list)：反转

void shuffle(List list),随机排序

void sort(List list),按自然排序的升序排序

void sort(List list, Comparator c);定制排序，由Comparator控制排序逻辑

void swap(List list, int i , int j),交换两个索引位置的元素

void rotate(List list, int distance),旋转。当distance为正数时，将list后distance个元素整体移到前面。当distance为负数时，将 list的前distance个元素整体移到后面。

下面简单演示Collections操作List

```java
 1 package collection;
 2 
 3 import java.util.ArrayList;
 4 import java.util.Collections;
 5 import java.util.Comparator;
 6 
 7 public class CollectionsTest {
 8     public static void main(String[] args) {
 9         ArrayList nums =  new ArrayList();
10         nums.add(8);
11         nums.add(-3);
12         nums.add(2);
13         nums.add(9);
14         nums.add(-2);
15         System.out.println(nums);
16         Collections.reverse(nums);
17         System.out.println(nums);
18         Collections.sort(nums);
19         System.out.println(nums);
20         Collections.shuffle(nums);
21         System.out.println(nums);
22         //下面只是为了演示定制排序的用法，将int类型转成string进行比较
23         Collections.sort(nums, new Comparator() {
24             
25             @Override
26             public int compare(Object o1, Object o2) {
27                 // TODO Auto-generated method stub
28                 String s1 = String.valueOf(o1);
29                 String s2 = String.valueOf(o2);
30                 return s1.compareTo(s2);
31             }
32             
33         });
34         System.out.println(nums);
35     }
36 }
```

执行结果，

```java
1 [8, -3, 2, 9, -2]
2 [-2, 9, 2, -3, 8]
3 [-3, -2, 2, 8, 9]
4 [9, -2, 8, 2, -3]
5 [-2, -3, 2, 8, 9]
```

### 查找，替换操作

int binarySearch(List list, Object key), 对List进行二分查找，返回索引，注意List必须是有序的

int max(Collection coll),根据元素的自然顺序，返回最大的元素。 类比int min(Collection coll)

int max(Collection coll, Comparator c)，根据定制排序，返回最大元素，排序规则由Comparatator类控制。类比int min(Collection coll, Comparator c)

void fill(List list, Object obj),用元素obj填充list中所有元素

int frequency(Collection c, Object o)，统计元素出现次数

int indexOfSubList(List list, List target), 统计targe在list中第一次出现的索引，找不到则返回-1，类比int lastIndexOfSubList(List source, list target).

boolean replaceAll(List list, Object oldVal, Object newVal), 用新元素替换旧元素。

下面示范简单用法，

```java
 1 package collection.collections;
 2 
 3 import java.util.ArrayList;
 4 import java.util.Collections;
 5 
 6 public class CollectionsTest {
 7     public static void main(String[] args) {
 8         ArrayList num =  new ArrayList();
 9         num.add(3);
10         num.add(-1);
11         num.add(-5);
12         num.add(10);
13         System.out.println(num);
14         System.out.println(Collections.max(num));
15         System.out.println(Collections.min(num));
16         Collections.replaceAll(num, -1, -7);
17         System.out.println(Collections.frequency(num, 3));
18         Collections.sort(num);
19         System.out.println(Collections.binarySearch(num, -5));
20     }
21 }
```



执行结果，

```java
1 [3, -1, -5, 10]
2 10
3 -5
4 1
5 1
```

 

### 同步控制

Collections中几乎对每个集合都定义了同步控制方法，例如 SynchronizedList(), SynchronizedSet()等方法，来将集合包装成线程安全的集合。下面是Collections将普通集合包装成线程安全集合的用法，



```java
 1 package collection.collections;
 2 
 3 import java.util.ArrayList;
 4 import java.util.Collection;
 5 import java.util.Collections;
 6 import java.util.HashMap;
 7 import java.util.HashSet;
 8 import java.util.List;
 9 import java.util.Map;
10 import java.util.Set;
11 
12 public class SynchronizedTest {
13     public static void main(String[] args) {
14         Collection c = Collections.synchronizedCollection(new ArrayList());
15         List list = Collections.synchronizedList(new ArrayList());
16         Set s = Collections.synchronizedSet(new HashSet());
17         Map m = Collections.synchronizedMap(new HashMap());
18     }
19 }
```

设置不可变（只读）集合

Collections提供了三类方法返回一个不可变集合，

emptyXXX(),返回一个空的只读集合（这不知用意何在？）

singleXXX()，返回一个只包含指定对象，只有一个元素，只读的集合。

unmodifiablleXXX()，返回指定集合对象的只读视图。

用法如下，

```java
 1 package collection.collections;
 2 
 3 import java.util.Collection;
 4 import java.util.Collections;
 5 import java.util.HashMap;
 6 import java.util.List;
 7 import java.util.Map;
 8 import java.util.Set;
 9 
10 public class UnmodifiableCollection {
11     public static void main(String[] args) {
12         List lt = Collections.emptyList();
13         Set st = Collections.singleton("avs");
14         
15         Map mp = new HashMap();
16         mp.put("a",100);
17         mp.put("b", 200);
18         mp.put("c",150);
19         Map readOnlyMap = Collections.unmodifiableMap(mp);
20         
21         //下面会报错
22         lt.add(100);
23         st.add("sdf");
24         mp.put("d", 300);
25     }
26 }
```

 执行结果，

```java
1 Exception in thread "main" java.lang.UnsupportedOperationException
2     at java.util.AbstractList.add(Unknown Source)
3     at java.util.AbstractList.add(Unknown Source)
4     at collection.collections.UnmodifiableCollection.main(UnmodifiableCollection.java:22)
```

## [Java中Arrays详解](https://www.cnblogs.com/wei-jing/p/10540192.html)

###  一、Arrays类的定义

https://blog.csdn.net/qq_44458489/article/details/105651408

Arrays类位于 java.util 包中，主要包含了操纵数组的各种方法

使用时导包:import java.util.Arrays

二、Arrays常用函数（都是静态的)

1.void Arrays.sort()

void Array.sort(Object[] array)

功能：对数组按照升序排序

示例

```java
        int[] nums = {2,5,0,4,6,-10};
        Arrays.sort(nums);
        for(int i :nums)
            System.out.print(i+" ");
        /* 之前:2 5 0 4 6 -10 
         * 结果:-10 0 2 4 5 6 
         */
```

Arrays.sort(Object[] array, int from, int to)

功能：对数组元素指定范围进行排序（排序范围是从元素下标为from,到下标为to-1的元素进行排序）

示例

```java
int[] nums = {2,5,0,4,1,-10};
        //对前四位元素进行排序
        Arrays.sort(nums, 0, 4);
        for(int i :nums)
            System.out.print(i+" ");
        /* 之前:2 5 0 4 1 -10
         * 结果:0 2 4 5 1 -10 
         */
```



 2.Arrays.fill(Object[] array,Object object)

功能：可以为数组元素填充相同的值

```java
int[] nums = {2,5,0,4,1,-10};
        Arrays.fill(nums, 1);
        for(int i :nums)
            System.out.print(i+" ");
        /* 之前:2 5 0 4 1 -10
         * 结果:1 1 1 1 1 1 
         */
```

Arrays.fill(Object[] array,int from,int to,Object object)

功能：对数组的部分元素填充一个值,从起始位置到结束位置，取头不取尾

```java
int[] nums = {2,5,0,4,1,-10};
        //对数组元素下标2到4的元素赋值为3
        Arrays.fill(nums,2,5,3);
        for(int i :nums)
            System.out.print(i+" ");
        /* 之前:2 5 0 4 1 -10
         * 结果:2 5 3 3 3 -10 
         */
```

3.Arrays.toString(Object[] array)

功能：返回数组的字符串形式

示例

```java
        int[] nums = {2,5,0,4,1,-10};
        System.out.println(Arrays.toString(nums));
        /*
         * 结果:[2, 5, 0, 4, 1, -10]
         */
```

4.Arrays.deepToString(Object[][] arrays)

功能：返回多维数组的字符串形式

示例

```java
int[][] nums = {{1,2},{3,4}};
        System.out.println(Arrays.deepToString(nums));
        /*
         * 结果:[[1, 2], [3, 4]]
         */
```

Arrays.equals(Object [], Object [])
功能：比较数组元素是否相等


	import java.util.Arrays;
	public class Test {
	
	public static void main(String[] args) {
		int[] arr1 = {1, 2, 3};
		int[] arr2 = {1, 2, 3};
		System.out.println(Arrays.equals(arr1, arr2)); //true
	}
	}



分析：如果是arr1.equals(arr2),则返回false，因为equals比较的是两个对象的地址，不是里面的数，而Arrays.equals重写了equals，所以，这里能比较元素是否相等。
补充：如果还是不用Arrays.equals，那么如何重写equals来比较两个数组的元素是否相等呢？ 代码如下：



	public class Test {
	public static void main(String[] args) {
		int[] arr1 = {1, 2, 3};
		int[] arr2 = {1, 2, 3};
		System.out.println(Test.isEquals(arr1, arr2)); //true
	}
	
	// Compare the contents of two int arrays
	public static boolean isEquals(int[] a, int[] b) {
		if (a == null || b == null) {
			return false;
		}
		if (a.length != b.length) {
			return false;
		}
		for (int i = 0; i < a.length; ++i) {
			if (a[i] != b[i]) {
				return false;
			}
		}
		return true;
	}}


Arrays.binarySearch(Object[] a, Object key)
功能：二分查找法找指定元素的索引值（下标）
注意：数组一定是排好序的，否则会出错。找到元素，只会返回最后一个位置

	import java.util.Arrays;
	public class Test {
	public static void main(String[] args) {
		int[] arr = {10, 20, 30, 40, 50};
		System.out.println(Arrays.binarySearch(arr, 20)); //1
	}}


分析：能找到该元素，返回下标为1（0开始）



	import java.util.Arrays;
	public class Test {
	
	public static void main(String[] args) {
		int[] arr = {10, 20, 30, 40, 50};
		System.out.println(Arrays.binarySearch(arr, 35)); //-4
	}}



分析：找不到元素，返回-x，从-1开始数，返回-4



	import java.util.Arrays;
	public class Test {
	public static void main(String[] args) {
		int[] arr = {10, 20, 30, 40, 50};
		System.out.println(Arrays.binarySearch(arr, 0, 3, 30)); //2
	}}


分析：从0到3位（不包括）找30，找到了，在第2位，返回2



	import java.util.Arrays;
	public class Test {
	public static void main(String[] args) {
		int[] arr = {10, 20, 30, 40, 50};
		System.out.println(Arrays.binarySearch(arr, 0, 3, 40)); //-4
	}}



分析：从0到3位（不包括）找40，找不到，从-1开始数，返回-4

Arrays.copyOf(int[] original, int newLength)
Arrays.copyOfRange(int[] original, int from, int to)
功能：截取数组


	import java.util.Arrays;
	public class Test {
	public static void main(String[] args) {
		int[] arr = {10, 20, 30, 40, 50};
		int[] arr1 = Arrays.copyOf(arr, 3);
		output(arr1); //10 20 30 
	}
	
	public static void output(int[] a) {
		for (int i = 0; i < a.length; i++) {
			System.out.printf(a[i] + " ");
		}
	}}



分析：截取arr数组的3个元素赋值给姓数组arr1



	import java.util.Arrays;
	public class Test {
	public static void main(String[] args) {
		int[] arr = {10, 20, 30, 40, 50};
		int[] arr1 = Arrays.copyOfRange(arr, 1, 3); //20 30 
		output(arr1);
	}
	
	public static void output(int[] a) {
		for (int i = 0; i < a.length; i++) {
			System.out.printf(a[i] + " ");
		}
	}
	}re

分析：从第1位（0开始）截取到第3位（不包括）



# Steam流式编程

特地感谢鲁班大叔的分享，原学习地址：[Java8 Stream流式编程爱 撸码就是快，流式编程好 代码传家宝](https://www.bilibili.com/video/BV1Mp4y1S7Em)
以下是学习过程整理的笔记

## 1、简介

[Stream](https://so.csdn.net/so/search?q=Stream&spm=1001.2101.3001.7020) 流处理，首先要澄清的是 java8 中的 Stream 与 I/O 流 InputStream 和 OutputStream 是完全不同的概念。
Stream 机制是针对集合迭代器的增强。流允许你用声明式的方式处理数据集合（通过查询语句来表达，而不是临时编写一个实现）

## 2、创建对象流的三种方式

1. 由集合对象创建流。对支持流处理的对象调用 **stream()**。支持流处理的对象包括 `Collection` 集合及其子类

```java
List<Integer> list = Arrays.asList(1,2,3);
Stream<Integer> stream = list.stream();
```

1. 由数组创建流。通过静态方法 **Arrays**.**stream()** 将数组转化为流（Stream）

```java
IntStream stream = Arrays.stream(new int[]{3, 2, 1});
```

1. 通过静态方法 **Stream.of()** ，但是底层其实还是调用 Arrays.stream()

```java
Stream<Integer> stream = Stream.of(1, 2, 3);
```

注意：
还有两种比较特殊的流

- 空流：**Stream.empty()**
- 无限流：**Stream.generate()** 和 **Stream.iterate()**。可以配合 **limit()** 使用可以限制一下数量

```java
// 接受一个 Supplier 作为参数
Stream.generate(Math::random).limit(10).forEach(System.out::println);
// 初始值是 0，新值是前一个元素值 + 2
Stream.iterate(0, n -> n + 2).limit(10).forEach(System.out::println);
```

## 3、流处理的特性

1. 不存储数据
2. 不会改变数据源
3. 不可以重复使用

测试用例：

```java
package com.godfrey.stream.features;

import org.junit.Assert;
import org.junit.Test;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

/**
 * 流特性
 *
 * @author godfrey
 * @since 2021-08-15
 */
class StreamFeaturesTest {

    /**
     * 流的简单例子
     */
    @Test
    public void test1() {
        List<Integer> list = Stream.of(1, 2, 5, 9, 7, 3).filter(val -> val > 2).sorted().collect(Collectors.toList());
        for (Integer item : list) {
            System.out.println(item);
        }
    }

    /**
     * 流不会改变数据源
     */
    @Test
    public void test2() {
        List<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(1);
        Assert.assertEquals(3, list.stream().distinct().count());
        Assert.assertEquals(4, list.size());
    }

    /**
     * 流不可以重复使用
     */
    @Test(expected = IllegalStateException.class)
    public void test3() {
        Stream<Integer> integerStream = Stream.of(1, 2, 3);
        Stream<Integer> newStream = integerStream.filter(val -> val > 2);
        integerStream.skip(1);
    }
}
```

首先，**test1()** 向我们展示了流的一般用法，由下图可见，源数据流经管道，最后输出结果数据。

![stream-pipeline](assets/a075ebf9655b0b1d1d4e3c5b2f5d7245-165491090971333.png)

然后，我们先看 **test3()**，源数组产生的流对象 **integerStream** 在调用 **filter()** 之后，数据立即流向了 **newStream**。
正因为流“不保存数据”的特性，所以重复利用 **integerStream** 再次调用 **skip(1)** 方法，会抛出一个 **IllegalStateException** 的异常：

java.lang.IllegalStateException: stream has already been operated upon or closed

所以说流不存储数据，且流不可以重复使用。

最后，我们来看 **test2()**，尽管我们对 **list** 对象生成的流 **list.stream()** 做了去重操作 **distinct()** ，但是并不影响源数据对象 **list**。

## 4、流处理的操作类型

Stream 的所有操作连起来组合成了管道，管道有两种操作：
第一种，中间操作（intermediate）。调用中间操作方法返回的是一个新的流对象
第二种，终值操作（terminal）。在调用该方法后，将执行之前所有的中间操作，并返回结果

## 5、流处理的执行顺序

为了更好地演示效果，我们首先要了解一下 **Stream.peek()** 方法， 这个方法和 **Stream.forEach()** 使用方法类似，都接受 `Consumer` 作为参数

| 流操作方法 | 流操作类型 |
| ---------- | ---------- |
| peek()     | 中间操作   |
| forEach()  | 终值操作   |

所以，我们可以用 peek 来证明流的执行顺序。
我们定义一个 Apple 对象：

```java
package com.godfrey.stream.order;

/**
 * @author godfrey
 * @since 2021-08-15
 */
public class Apple {

    /**
     * 编号
     */
    private int id;

    /**
     * 颜色
     */
    private String color;

    /**
     * 重量
     */
    private int weight;

    /**
     * 产地
     */
    private String birthplace;

    public Apple(int id, String color, int weight, String birthplace) {
        this.id = id;
        this.color = color;
        this.weight = weight;
        this.birthplace = birthplace;
    }
    //Setter、Getter省略
}
```

然后创建多个苹果放到 appleStore 中

```java
public class StreamTest {

    private static final List<Apple> appleStore = Arrays.asList(
            new Apple(1, "red", 500, "湖南"),
            new Apple(2, "red", 100, "天津"),
            new Apple(3, "green", 300, "湖南"),
            new Apple(4, "green", 200, "天津"),
            new Apple(5, "green", 100, "湖南")
    );
    public static void main(String[] args) {
        appleStore.stream().filter(apple -> apple.getWeight() > 100)
                .peek(apple -> System.out.println("通过第1层筛选 " + apple))
                .filter(apple -> "green".equals(apple.getColor()))
                .peek(apple -> System.out.println("通过第2层筛选 " + apple))
                .filter(apple -> "湖南".equals(apple.getBirthplace()))
                .peek(apple -> System.out.println("通过第3层筛选 " + apple))
                .collect(Collectors.toList());
    }
}
```

测试结果如下：![在这里插入图片描述](assets/0a956518e0e043b7a22f3c6a41621af4-165491090971435.png)

以上测试例子的执行顺序示意图：

![stream-execute-sequence](assets/3c0bf4d6e1e45193bb0900a7f9e8fbfd-165491090971437.png)

总之，执行顺序会走一个“之”字形

注意：
如果我们注释掉 **.collect(Collectors.toList())**， 我们会发现一行语句也不会打印出来。
这刚好证明了：

通过连续执行多个操作倒便就组成了 Stream 中的执行管道（pipeline）。需要注意的是这些管道被添加后并不会真正执行，只有等到调用终值操作之后才会执行。

## 6、用流收集数据与 SQL 统计函数

**Collector** 被指定和四个函数一起工作，并实现累加 entries 到一个可变的结果容器，并可选择执行该结果的最终变换。 这四个函数就是：

| 接口函数      | 作用                           | 返回值         |
| ------------- | ------------------------------ | -------------- |
| supplier()    | 创建并返回一个新的可变结果容器 | Supplier       |
| accumulator() | 把输入值加入到可变结果容器     | BiConsumer     |
| combiner()    | 将两个结果容器组合成一个       | BinaryOperator |
| finisher()    | 转换中间结果为终值结果         | Function       |

**Collectors** 则是重要的工具类，提供给我一些 *Collector* 实现。
Stream 接口中 **collect()** 就是使用 *Collector* 做参数的。
其中，`collect(Supplier<R> supplier, BiConsumer<R, ? super T> accumulator, BiConsumer<R, R> combiner)` 无非就是比 *Collector* 少一个 finisher，本质上是一样的！

遍历在传统的 javaEE 项目中数据源比较单一而且集中，像这类的需求都我们可能通过关系数据库中进行获取计算。
现在的互联网项目数据源成多样化有：关系数据库、NoSQL、Redis、mongodb、ElasticSearch、Cloud Server 等。这时就需我们从各数据源中汇聚数据并进行统计。
Stream + Lambda的组合就是为了让 Java 语句更像查询语句，取代繁杂的 for 循环。

```sql
CREATE TABLE `applestore` (
  `id` INT NOT NULL AUTO_INCREMENT COMMENT '编号',
  `color` VARCHAR (50) COMMENT '颜色',
  `weight` INT COMMENT '重量',
  `birthplace` VARCHAR (50) COMMENT '产地',
  PRIMARY KEY (`id`)
) COMMENT = '水果商店';
```

另外还有数据初始化语句

```sql
INSERT INTO applestore VALUES (1, "red", 500,"湖南");
INSERT INTO applestore VALUES (2, "red", 100,"湖南");
INSERT INTO applestore VALUES (3, "green", 300, "湖南");
INSERT INTO applestore VALUES (4, "green", 200, "天津");
INSERT INTO applestore VALUES (5, "green", 100, "湖南");
```

测试用例：

```java
public class StreamStatisticsTest {
    
    List<Apple> appleStore;
    
    @Before
    public void initData() {
        appleStore = Arrays.asList(
                new Apple(1, "red", 500, "湖南"),
                new Apple(2, "red", 100, "天津"),
                new Apple(3, "green", 300, "湖南"),
                new Apple(4, "green", 200, "天津"),
                new Apple(5, "green", 100, "湖南")
        );
    }

    @Test
    public void test1() {
        Integer weight1 = appleStore.stream().collect(Collectors.summingInt(apple -> apple.getWeight()));
        System.out.println(weight1);
        Integer weight2 = appleStore.stream().collect(Collectors.summingInt(Apple::getWeight));
        System.out.println(weight2);
    }
}
```

### 6.1、求和

- Collectors.summingInt()
- Collectors.summingLong()
- Collectors.summingDouble()

![sum](assets/e0ec8398b0d8b0b5b457d4fec55b30b1-165491090971439.png)

通过引用 `import static java.util.stream.Collectors.summingInt` 就可以直接调用 **summingInt()**
**Apple::getWeight()** 可以写为 **apple -> apple.getWeight()**，求和函数的参数是结果转换函数 **Function**

### 6.2、求平均值

- Collectors.averagingInt()
- Collectors.averagingKLong()
- Collectors.averagingDouble()

![average](assets/13ed5a27dea71db38827d1ba248073a5-165491090971441.png)

### 6.3、归约

- Collectors.reducing()

```java
@Test
public void reduce() {
    Integer sum = appleStore.stream().collect(reducing(0, Apple::getWeight, (a, b) -> a + b));
    System.out.println(sum);
}
```

![reducing](assets/8a2098d0695975e09c37344fab4d5ffa-165491090971443.png)

- 归约就是为了遍历数据容器，将每个元素对象转换为特定的值，通过累积函数，得到一个最终值。
- 转换函数，函数输入参数的对象类型是跟 Stream 中的 T 一样的对象类型，输出的对象类型的是和初始值一样的对象类型
- 累积函数，就是把转换函数的结果与上一次累积的结果进行一次合并，如果是第一次累积，那么取初始值来计算
  累积函数还可以作用于两个 Stream 合并时的累积，这个可以结合 groupingBy 来理解
- 初始值的对象类型，和每一次累积函数输出值的对象类型是相同的，这样才能一直进行累积函数的运算。
- 归约不仅仅可以支持加法，还可以支持比如乘法以及其他更高级的累积公式。

计数只是归约的一种特殊形式

- Collectors.counting(): 初始值为 **0**，转换函数 **f(x)=1**（x 就是 Stream 的 T 类型），累积函数就是“做加法”

### 6.4、分组

- Collectors.groupingBy()
  分组就和 SQL 中的 **GROUP BY** 十分类似，所以 **groupingBy()** 的所有参数中有一个参数是 **Collector**接口，这样就能够和 求和/求平均值/归约 一起使用。
  ![groupingBy](assets/7e3e4186eb0a5ed170910d3468a91e07-165491090971445.png)
- 传入参数的接口是 Function 接口，实现这个接口可以是实现从 A 类型到 B 类型的转换
- 其中有一个方法可以传入参数 `Supplier mapFactory`,这个可以通过自定义 Map工厂，来创建自定义的分组 Map

分区只是分组的一种特殊形式

- Collectors.partitioningBy() 传入参数的是 Predicate 接口，
- 分区相当于把流中的数据，分组分成了“正反两个阵营”

## 7、数值流

我们之前在求和时用到的例子，`appleStore.stream().collect(summingInt(Apple::getWeight))`，我就被 IDEA 提醒：
appleStore.stream().collect(summingInt(Apple::getWeight))

The ‘collect(summingInt())’ can be replaced with ‘mapToInt().sum()’

这就告诉我们可以先转化为数值流，然后再用 IntStream 做求和。

Java8引入了三个原始类型特化流接口：IntStream，LongStream，DoubleStream，分别将流中的元素特化为 int，long，double。
普通对象流和原始类型特化流之间可以相互转化
![stream-map](assets/e358ecf397ec6dbc71aa68e1d256e294-165491090971547.png)

- 其中 IntStream 和 LongStream 可以调用 asDoubleStream 变为 DoubleStream，但是这是单向的转化方法。
- IntStream#boxed() 可以得到 Stream ,这个也是一个单向方法，支持数值流转换回对象流，LongStream 和 DoubleStream 也有类似的方法。

### 7.1、生成一个数值流

- **IntStream.range(int startInclusive, int endExclusive)**
- **IntStream.rangeClosed(int startInclusive, int endInclusive)**
- range 和 rangeClosed 的区别在于数值流是否包含 end 这个值。range 代表的区间是 [start, end) , rangeClosed 代表的区间是 [start, end]
- LongStream 也有 range 和 rangeClosed 方法，但是 DoubleStream 没有！

### 7.2、flatMap

- Stream.flatMap 就是流中的每个对象，转换产生一个对象流。
- Stream.flatMapToInt 指定流中的每个对象，转换产生一个 IntStream 数值流；类似的，还有 flatMapToLong，flatMapToDouble
- IntStream.flatMap 数值流中的每个对象，转换产生一个数值流

flatMap 可以代替一些嵌套循环来开展业务：
比如我们要求勾股数（即 a*a+b*b=c*c 的一组数中的 a，b，c），且我们要求 a 和 b 的范围是 [1,100],我们在 Java8之前会这样写：

```java
@Test
public void testJava() {
    List<int[]> resultList = new ArrayList<>();
    for (int a = 1; a <= 100; a++) {
        for (int b = a; b <= 100; b++) {
            double c = Math.sqrt(a * a + b * b);
            if (c % 1 == 0) {
                resultList.add(new int[]{a, b, (int) c});
        	}
    	}
	}

    int size = resultList.size();
	for (int i = 0; i < size && i < 5; i++) {
    	int[] a = resultList.get(i);
    	System.out.println(a[0] + " " + a[1] + " " + a[2]);
	}
}   
```

Java8之后，我们可以用上 flatMap：

```java
@Test
public void flatMap() {
    Stream<int[]> stream = IntStream.rangeClosed(1, 100)
        .boxed()
        .flatMap(a -> IntStream.rangeClosed(a, 100)
                 .filter(b -> Math.sqrt(a * a + b * b) % 1 == 0)
                 .mapToObj(b -> new int[]{a, b, (int) Math.sqrt(a * a + b * b)})
    );
    stream.limit(5).forEach(a -> System.out.println(a[0] + " " + a[1] + " " + a[2]));
}
```

创建一个从 1 到 100 的数值范围来创建 a 的值。对每个给定的 a 值，创建一个三元数流。
flatMap 方法在做映射的同时，还会把所有生成的三元数流扁平化成一个流。

## 总结

- Stream 主要包括对象流和数值流两大类
- **Stream.of()** , **Arrays.stream()** , **Collection.stream()** ,**Stream.generate()** , **Stream.iterate()** 方法创建对象流
- **IntStream.range()** 和 **IntStream.rangeClosed()** 可以创建数值流，对象流和数值流可以相互转换
- Collector 收集器接口，可以实现归约，统计函数（求和，求平均值，最大值，最小值），分组等功能
- 流的执行，需要调用终值操作。流中每个元素执行到不能继续执行下去，才会转到另一个元素执行。而不是分阶段迭代数据容器中的所有元素！
- flatMap 可以给流中的每个元素生成一个对应的流，并且扁平化为一个流

文章知识点与官方知识档案匹配，可进一步学习相关知识

[Java技能树](https://edu.csdn.net/skill/java/java-77d7a80503af4222b7fdd0a06d1daf30)[行为抽象和Lambda](https://edu.csdn.net/skill/java/java-77d7a80503af4222b7fdd0a06d1daf30)[流](https://edu.csdn.net/skill/java/java-77d7a80503af4222b7fdd0a06d1daf30)24640 人正在系统学习中



# Stream 使用

[快学Java](javascript:void(0);) *2022-03-06 18:00*

每天傍晚18:00一起成长！

![图片](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181212590.png)

先贴上几个案例，水平高超的同学可以挑战一下：

1. ​	从员工集合中筛选出salary大于8000的员工，并放置到新的集合里。
2. 统计员工的最高薪资、平均薪资、薪资之和。
3. 将员工按薪资从高到低排序，同样薪资者年龄小者在前。
4. 将员工按性别分类，将员工按性别和地区分类，将员工按薪资是否高于8000分为两部分。

用传统的迭代处理也不是很难，但代码就显得冗余了，跟Stream相比高下立判。

## 1 Stream概述

Java 8 是一个非常成功的版本，这个版本新增的`Stream`，配合同版本出现的 `Lambda` ，给我们操作集合（Collection）提供了极大的便利。

那么什么是`Stream`？

> `Stream`将要处理的元素集合看作一种流，在流的过程中，借助`Stream API`对流中的元素进行操作，比如：筛选、排序、聚合等。

`Stream`可以由数组或集合创建，对流的操作分为两种：

1. 中间操作，每次返回一个新的流，可以有多个。
2. 终端操作，每个流只能进行一次终端操作，终端操作结束后流无法再次使用。终端操作会产生一个新的集合或值。

另外，`Stream`有几个特性：

1. stream不存储数据，而是按照特定的规则对数据进行计算，一般会输出结果。
2. stream不会改变数据源，通常情况下会产生一个新的集合或一个值。
3. stream具有延迟执行特性，只有调用终端操作时，中间操作才会执行。

## 2 Stream的创建

`Stream`可以通过集合数组创建。

1、通过 `java.util.Collection.stream()` 方法用集合创建流

```
List<String> list = Arrays.asList("a", "b", "c");
// 创建一个顺序流
Stream<String> stream = list.stream();
// 创建一个并行流
Stream<String> parallelStream = list.parallelStream();
```

2、使用`java.util.Arrays.stream(T[] array)`方法用数组创建流

```
int[] array={1,3,5,6,8};
IntStream stream = Arrays.stream(array);
```

3、使用`Stream`的静态方法：`of()、iterate()、generate()`

```
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6);

Stream<Integer> stream2 = Stream.iterate(0, (x) -> x + 3).limit(4);
stream2.forEach(System.out::println); // 0 2 4 6 8 10

Stream<Double> stream3 = Stream.generate(Math::random).limit(3);
stream3.forEach(System.out::println);
```

输出结果：

> 0 3 6 9 0.6796156909271994 0.1914314208854283 0.8116932592396652

**`stream`和`parallelStream`的简单区分：** `stream`是顺序流，由主线程按顺序对流执行操作，而`parallelStream`是并行流，内部以多线程并行执行的方式对流进行操作，但前提是流中的数据处理没有顺序要求。例如筛选集合中的奇数，两者的处理不同之处：

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

如果流中的数据量足够大，并行流可以加快处速度。[Java 8 创建 Stream 的 10 种方式，](http://mp.weixin.qq.com/s?__biz=MzI3ODcxMzQzMw==&mid=2247490117&idx=3&sn=bb3697ac16082a9d3001ad7036366f9c&chksm=eb539f73dc241665a7340767fbdc61eb0a16b9994c7784aa40ee08604b8fccbd066557f0bea6&scene=21#wechat_redirect)这篇推荐看下哦。

除了直接创建并行流，还可以通过`parallel()`把顺序流转换成并行流：

```
Optional<Integer> findFirst = list.stream().parallel().filter(x->x>6).findFirst();
```

## 3 Stream的使用

在使用stream之前，先理解一个概念：`Optional` 。

> `Optional`类是一个可以为`null`的容器对象。如果值存在则`isPresent()`方法会返回`true`，调用`get()`方法会返回该对象。更详细说明请见：菜鸟教程Java 8 Optional类

**接下来，大批代码向你袭来！我将用20个案例将Stream的使用整得明明白白，只要跟着敲一遍代码，就能很好地掌握。**

![图片](assets/640-16549491382921.png)

### 案例使用的员工类

[这是后面案例中使用的员工类：](http://mp.weixin.qq.com/s?__biz=MzI3ODcxMzQzMw==&mid=2247524678&idx=3&sn=a153fd4fae16c357d55414e067d7bf25&chksm=eb50e470dc276d6676c923b597cbd28cf29e7a31393f1f03afedaf22f6aaf9e0e5517b9bdb32&scene=21#wechat_redirect)

```
List<Person> personList = new ArrayList<Person>();
personList.add(new Person("Tom", 8900, "male", "New York"));
personList.add(new Person("Jack", 7000, "male", "Washington"));
personList.add(new Person("Lily", 7800, "female", "Washington"));
personList.add(new Person("Anni", 8200, "female", "New York"));
personList.add(new Person("Owen", 9500, "male", "New York"));
personList.add(new Person("Alisa", 7900, "female", "New York"));

class Person {
 private String name;  // 姓名
 private int salary; // 薪资
 private int age; // 年龄
 private String sex; //性别
 private String area;  // 地区

 // 构造方法
 public Person(String name, int salary, int age,String sex,String area) {
  this.name = name;
  this.salary = salary;
  this.age = age;
  this.sex = sex;
  this.area = area;
 }
 // 省略了get和set，请自行添加

}
```

### [3.1 遍历/匹配（foreach/find/match）](http://mp.weixin.qq.com/s?__biz=MzI3ODcxMzQzMw==&mid=2247524678&idx=3&sn=a153fd4fae16c357d55414e067d7bf25&chksm=eb50e470dc276d6676c923b597cbd28cf29e7a31393f1f03afedaf22f6aaf9e0e5517b9bdb32&scene=21#wechat_redirect)

`Stream`也是支持类似集合的遍历和匹配元素的，只是`Stream`中的元素是以`Optional`类型存在的。`Stream`的遍历、匹配非常简单。另外，Java 8 系列教程和示例全部整理好了，微信搜索Java技术栈，在后台发送：Java，可以在线阅读。

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
// import已省略，请自行添加，后面代码亦是

public class StreamTest {
 public static void main(String[] args) {
        List<Integer> list = Arrays.asList(7, 6, 9, 3, 8, 2, 1);

        // 遍历输出符合条件的元素
        list.stream().filter(x -> x > 6).forEach(System.out::println);
        // 匹配第一个
        Optional<Integer> findFirst = list.stream().filter(x -> x > 6).findFirst();
        // 匹配任意（适用于并行流）
        Optional<Integer> findAny = list.parallelStream().filter(x -> x > 6).findAny();
        // 是否包含符合特定条件的元素
        boolean anyMatch = list.stream().anyMatch(x -> x < 6);
        System.out.println("匹配第一个值：" + findFirst.get());
        System.out.println("匹配任意一个值：" + findAny.get());
        System.out.println("是否存在大于6的值：" + anyMatch);
    }
}
```

### 3.2 筛选（filter）

筛选，是按照一定的规则校验流中的元素，将符合条件的元素提取到新的流中的操作。

![图片](assets/640-16549491382932.png)

**案例一：筛选出`Integer`集合中大于7的元素，并打印出来**

```
public class StreamTest {
 public static void main(String[] args) {
  List<Integer> list = Arrays.asList(6, 7, 3, 8, 1, 2, 9);
  Stream<Integer> stream = list.stream();
  stream.filter(x -> x > 7).forEach(System.out::println);
 }
}
```

预期结果：

> 8 9

**案例二：筛选员工中工资高于8000的人，并形成新的集合。** 形成新集合依赖`collect`（收集），后文有详细介绍。

```
public class StreamTest {
 public static void main(String[] args) {
  List<Person> personList = new ArrayList<Person>();
  personList.add(new Person("Tom", 8900, 23, "male", "New York"));
  personList.add(new Person("Jack", 7000, 25, "male", "Washington"));
  personList.add(new Person("Lily", 7800, 21, "female", "Washington"));
  personList.add(new Person("Anni", 8200, 24, "female", "New York"));
  personList.add(new Person("Owen", 9500, 25, "male", "New York"));
  personList.add(new Person("Alisa", 7900, 26, "female", "New York"));

  List<String> fiterList = personList.stream().filter(x -> x.getSalary() > 8000).map(Person::getName)
    .collect(Collectors.toList());
  System.out.print("高于8000的员工姓名：" + fiterList);
 }
}
```

运行结果：

> 高于8000的员工姓名：[Tom, Anni, Owen]

### 3.3 聚合（max/min/count)

`max`、`min`、`count`这些字眼你一定不陌生，没错，在mysql中我们常用它们进行数据统计。Java stream中也引入了这些概念和用法，极大地方便了我们对集合、数组的数据统计工作。

最新 Java 核心技术教程和示例源码：https://github.com/javastacks/javastack

![图片](assets/640-16549491382933.png)

**案例一：获取`String`集合中最长的元素。**

```
public class StreamTest {
 public static void main(String[] args) {
  List<String> list = Arrays.asList("adnm", "admmt", "pot", "xbangd", "weoujgsd");

  Optional<String> max = list.stream().max(Comparator.comparing(String::length));
  System.out.println("最长的字符串：" + max.get());
 }
}
```

输出结果：

> 最长的字符串：weoujgsd

**案例二：获取`Integer`集合中的最大值。**

```
public class StreamTest {
 public static void main(String[] args) {
  List<Integer> list = Arrays.asList(7, 6, 9, 4, 11, 6);

  // 自然排序
  Optional<Integer> max = list.stream().max(Integer::compareTo);
  // 自定义排序
  Optional<Integer> max2 = list.stream().max(new Comparator<Integer>() {
   @Override
   public int compare(Integer o1, Integer o2) {
    return o1.compareTo(o2);
   }
  });
  System.out.println("自然排序的最大值：" + max.get());
  System.out.println("自定义排序的最大值：" + max2.get());
 }
}
```

输出结果：

> 自然排序的最大值：11 自定义排序的最大值：11

**案例三：获取员工工资最高的人。**

```
public class StreamTest {
 public static void main(String[] args) {
  List<Person> personList = new ArrayList<Person>();
  personList.add(new Person("Tom", 8900, 23, "male", "New York"));
  personList.add(new Person("Jack", 7000, 25, "male", "Washington"));
  personList.add(new Person("Lily", 7800, 21, "female", "Washington"));
  personList.add(new Person("Anni", 8200, 24, "female", "New York"));
  personList.add(new Person("Owen", 9500, 25, "male", "New York"));
  personList.add(new Person("Alisa", 7900, 26, "female", "New York"));

  Optional<Person> max = personList.stream().max(Comparator.comparingInt(Person::getSalary));
  System.out.println("员工工资最大值：" + max.get().getSalary());
 }
}
```

输出结果：

> 员工工资最大值：9500

**案例四：计算`Integer`集合中大于6的元素的个数。**

```
import java.util.Arrays;
import java.util.List;

public class StreamTest {
 public static void main(String[] args) {
  List<Integer> list = Arrays.asList(7, 6, 4, 8, 2, 11, 9);

  long count = list.stream().filter(x -> x > 6).count();
  System.out.println("list中大于6的元素个数：" + count);
 }
}
```

输出结果：

> list中大于6的元素个数：4

### 3.4 映射(map/flatMap)

映射，可以将一个流的元素按照一定的映射规则映射到另一个流中。分为`map`和`flatMap`：

- `map`：接收一个函数作为参数，该函数会被应用到每个元素上，并将其映射成一个新的元素。
- `flatMap`：接收一个函数作为参数，将流中的每个值都换成另一个流，然后把所有流连接成一个流。

![图片](assets/640-16549491382944.png)

**案例一：英文字符串数组的元素全部改为大写。整数数组每个元素+3。**

```
public class StreamTest {
 public static void main(String[] args) {
  String[] strArr = { "abcd", "bcdd", "defde", "fTr" };
  List<String> strList = Arrays.stream(strArr).map(String::toUpperCase).collect(Collectors.toList());

  List<Integer> intList = Arrays.asList(1, 3, 5, 7, 9, 11);
  List<Integer> intListNew = intList.stream().map(x -> x + 3).collect(Collectors.toList());

  System.out.println("每个元素大写：" + strList);
  System.out.println("每个元素+3：" + intListNew);
 }
}
```

输出结果：

> 每个元素大写：[ABCD, BCDD, DEFDE, FTR] 每个元素+3：[4, 6, 8, 10, 12, 14]

点击关注公众号，Java干货及时送达![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

![img](assets/0.png)

**Java技术栈**

专注分享Java技术干货，包括多线程、JVM、Spring Boot、Spring Cloud、Intellij IDEA、Dubbo、Zookeeper、Redis、架构设计、微服务、消息队列、Git、面试题、程序员攻略、最新动态等。

512篇原创内容



公众号

[**案例二：将员工的薪资全部增加1000。**

](http://mp.weixin.qq.com/s?__biz=MzI3ODcxMzQzMw==&mid=2247535563&idx=2&sn=2f28d811947f61f9690336b433831c19&chksm=eb50cefddc2747ebf647ce65467630ba9f010b1558f9bd5e5156700bcdc17baf788ad0c94a86&scene=21#wechat_redirect)

```
public class StreamTest {
 public static void main(String[] args) {
  List<Person> personList = new ArrayList<Person>();
  personList.add(new Person("Tom", 8900, 23, "male", "New York"));
  personList.add(new Person("Jack", 7000, 25, "male", "Washington"));
  personList.add(new Person("Lily", 7800, 21, "female", "Washington"));
  personList.add(new Person("Anni", 8200, 24, "female", "New York"));
  personList.add(new Person("Owen", 9500, 25, "male", "New York"));
  personList.add(new Person("Alisa", 7900, 26, "female", "New York"));

  // 不改变原来员工集合的方式
  List<Person> personListNew = personList.stream().map(person -> {
   Person personNew = new Person(person.getName(), 0, 0, null, null);
   personNew.setSalary(person.getSalary() + 10000);
   return personNew;
  }).collect(Collectors.toList());
  System.out.println("一次改动前：" + personList.get(0).getName() + "-->" + personList.get(0).getSalary());
  System.out.println("一次改动后：" + personListNew.get(0).getName() + "-->" + personListNew.get(0).getSalary());

  // 改变原来员工集合的方式
  List<Person> personListNew2 = personList.stream().map(person -> {
   person.setSalary(person.getSalary() + 10000);
   return person;
  }).collect(Collectors.toList());
  System.out.println("二次改动前：" + personList.get(0).getName() + "-->" + personListNew.get(0).getSalary());
  System.out.println("二次改动后：" + personListNew2.get(0).getName() + "-->" + personListNew.get(0).getSalary());
 }
}
```

[输出结果：](http://mp.weixin.qq.com/s?__biz=MzI3ODcxMzQzMw==&mid=2247535563&idx=2&sn=2f28d811947f61f9690336b433831c19&chksm=eb50cefddc2747ebf647ce65467630ba9f010b1558f9bd5e5156700bcdc17baf788ad0c94a86&scene=21#wechat_redirect)

> 一次改动前：Tom–>8900 一次改动后：Tom–>18900 二次改动前：Tom–>18900 二次改动后：Tom–>18900

**案例三：将两个字符数组合并成一个新的字符数组。**

```
public class StreamTest {
 public static void main(String[] args) {
  List<String> list = Arrays.asList("m,k,l,a", "1,3,5,7");
  List<String> listNew = list.stream().flatMap(s -> {
   // 将每个元素转换成一个stream
   String[] split = s.split(",");
   Stream<String> s2 = Arrays.stream(split);
   return s2;
  }).collect(Collectors.toList());

  System.out.println("处理前的集合：" + list);
  System.out.println("处理后的集合：" + listNew);
 }
}
```

输出结果：

> 处理前的集合：[m-k-l-a, 1-3-5] 处理后的集合：[m, k, l, a, 1, 3, 5]

### 3.5 归约(reduce)

推荐阅读：[最新 Java 核心技术教程，都在这了！](http://mp.weixin.qq.com/s?__biz=MzI3ODcxMzQzMw==&mid=2247519294&idx=2&sn=c4ad9ae745568439d7070a175f20c3ef&chksm=eb500908dc27801ead52ebf17490aaa5d1d983e2dfc536b4273f77cbd6c2c1cc9bd9a9bc0685&scene=21#wechat_redirect)

归约，也称缩减，顾名思义，是把一个流缩减成一个值，能实现对集合求和、求乘积和求最值操作。

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

**案例一：求`Integer`集合的元素之和、乘积和最大值。**

```
public class StreamTest {
 public static void main(String[] args) {
  List<Integer> list = Arrays.asList(1, 3, 2, 8, 11, 4);
  // 求和方式1
  Optional<Integer> sum = list.stream().reduce((x, y) -> x + y);
  // 求和方式2
  Optional<Integer> sum2 = list.stream().reduce(Integer::sum);
  // 求和方式3
  Integer sum3 = list.stream().reduce(0, Integer::sum);

  // 求乘积
  Optional<Integer> product = list.stream().reduce((x, y) -> x * y);

  // 求最大值方式1
  Optional<Integer> max = list.stream().reduce((x, y) -> x > y ? x : y);
  // 求最大值写法2
  Integer max2 = list.stream().reduce(1, Integer::max);

  System.out.println("list求和：" + sum.get() + "," + sum2.get() + "," + sum3);
  System.out.println("list求积：" + product.get());
  System.out.println("list求和：" + max.get() + "," + max2);
 }
}
```

输出结果：

> list求和：29,29,29 list求积：2112 list求和：11,11

**案例二：求所有员工的工资之和和最高工资。**

```
public class StreamTest {
 public static void main(String[] args) {
  List<Person> personList = new ArrayList<Person>();
  personList.add(new Person("Tom", 8900, 23, "male", "New York"));
  personList.add(new Person("Jack", 7000, 25, "male", "Washington"));
  personList.add(new Person("Lily", 7800, 21, "female", "Washington"));
  personList.add(new Person("Anni", 8200, 24, "female", "New York"));
  personList.add(new Person("Owen", 9500, 25, "male", "New York"));
  personList.add(new Person("Alisa", 7900, 26, "female", "New York"));

  // 求工资之和方式1：
  Optional<Integer> sumSalary = personList.stream().map(Person::getSalary).reduce(Integer::sum);
  // 求工资之和方式2：
  Integer sumSalary2 = personList.stream().reduce(0, (sum, p) -> sum += p.getSalary(),
    (sum1, sum2) -> sum1 + sum2);
  // 求工资之和方式3：
  Integer sumSalary3 = personList.stream().reduce(0, (sum, p) -> sum += p.getSalary(), Integer::sum);

  // 求最高工资方式1：
  Integer maxSalary = personList.stream().reduce(0, (max, p) -> max > p.getSalary() ? max : p.getSalary(),
    Integer::max);
  // 求最高工资方式2：
  Integer maxSalary2 = personList.stream().reduce(0, (max, p) -> max > p.getSalary() ? max : p.getSalary(),
    (max1, max2) -> max1 > max2 ? max1 : max2);

  System.out.println("工资之和：" + sumSalary.get() + "," + sumSalary2 + "," + sumSalary3);
  System.out.println("最高工资：" + maxSalary + "," + maxSalary2);
 }
}
```

输出结果：

> 工资之和：49300,49300,49300 最高工资：9500,9500

### 3.6 收集(collect)

`collect`，收集，可以说是内容最繁多、功能最丰富的部分了。从字面上去理解，就是把一个流收集起来，最终可以是收集成一个值也可以收集成一个新的集合。

> `collect`主要依赖`java.util.stream.Collectors`类内置的静态方法。

#### 3.6.1 归集(toList/toSet/toMap)

因为流不存储数据，那么在流中的数据完成处理后，需要将流中的数据重新归集到新的集合里。`toList`、`toSet`和`toMap`比较常用，另外还有`toCollection`、`toConcurrentMap`等复杂一些的用法。

下面用一个案例演示`toList`、`toSet`和`toMap`：

```java
public class StreamTest {
 public static void main(String[] args) {
  List<Integer> list = Arrays.asList(1, 6, 3, 4, 6, 7, 9, 6, 20);
  List<Integer> listNew = list.stream().filter(x -> x % 2 == 0).collect(Collectors.toList());
  Set<Integer> set = list.stream().filter(x -> x % 2 == 0).collect(Collectors.toSet());

  List<Person> personList = new ArrayList<Person>();
  personList.add(new Person("Tom", 8900, 23, "male", "New York"));
  personList.add(new Person("Jack", 7000, 25, "male", "Washington"));
  personList.add(new Person("Lily", 7800, 21, "female", "Washington"));
  personList.add(new Person("Anni", 8200, 24, "female", "New York"));

  Map<?, Person> map = personList.stream().filter(p -> p.getSalary() > 8000)
    .collect(Collectors.toMap(Person::getName, p -> p));
  System.out.println("toList:" + listNew);
  System.out.println("toSet:" + set);
  System.out.println("toMap:" + map);
 }
}
```

运行结果：

> toList：[6, 4, 6, 6, 20] toSet：[4, 20, 6] toMap：{Tom=mutest.Person@5fd0d5ae, Anni=mutest.Person@2d98a335}

#### 3.6.2 统计(count/averaging)

`Collectors`提供了一系列用于数据统计的静态方法：

- 计数：`count`
- 平均值：`averagingInt`、`averagingLong`、`averagingDouble`
- 最值：`maxBy`、`minBy`
- 求和：`summingInt`、`summingLong`、`summingDouble`
- 统计以上所有：`summarizingInt`、`summarizingLong`、`summarizingDouble`

**案例：统计员工人数、平均工资、工资总额、最高工资。**

```
public class StreamTest {
 public static void main(String[] args) {
  List<Person> personList = new ArrayList<Person>();
  personList.add(new Person("Tom", 8900, 23, "male", "New York"));
  personList.add(new Person("Jack", 7000, 25, "male", "Washington"));
  personList.add(new Person("Lily", 7800, 21, "female", "Washington"));

  // 求总数
  Long count = personList.stream().collect(Collectors.counting());
  // 求平均工资
  Double average = personList.stream().collect(Collectors.averagingDouble(Person::getSalary));
  // 求最高工资
  Optional<Integer> max = personList.stream().map(Person::getSalary).collect(Collectors.maxBy(Integer::compare));
  // 求工资之和
  Integer sum = personList.stream().collect(Collectors.summingInt(Person::getSalary));
  // 一次性统计所有信息
  DoubleSummaryStatistics collect = personList.stream().collect(Collectors.summarizingDouble(Person::getSalary));

  System.out.println("员工总数：" + count);
  System.out.println("员工平均工资：" + average);
  System.out.println("员工工资总和：" + sum);
  System.out.println("员工工资所有统计：" + collect);
 }
}
```

运行结果：

> 员工总数：3 员工平均工资：7900.0 员工工资总和：23700 员工工资所有统计：DoubleSummaryStatistics{count=3, sum=23700.000000,min=7000.000000, average=7900.000000, max=8900.000000}

#### 3.6.3 分组(partitioningBy/groupingBy)

- 分区：将`stream`按条件分为两个`Map`，比如员工按薪资是否高于8000分为两部分。
- 分组：将集合分为多个Map，比如员工按性别分组。有单级分组和多级分组。

![图片](assets/640-16549491382945.png)

**案例：将员工按薪资是否高于8000分为两部分；将员工按性别和地区分组**

```
public class StreamTest {
 public static void main(String[] args) {
  List<Person> personList = new ArrayList<Person>();
  personList.add(new Person("Tom", 8900, "male", "New York"));
  personList.add(new Person("Jack", 7000, "male", "Washington"));
  personList.add(new Person("Lily", 7800, "female", "Washington"));
  personList.add(new Person("Anni", 8200, "female", "New York"));
  personList.add(new Person("Owen", 9500, "male", "New York"));
  personList.add(new Person("Alisa", 7900, "female", "New York"));

  // 将员工按薪资是否高于8000分组
        Map<Boolean, List<Person>> part = personList.stream().collect(Collectors.partitioningBy(x -> x.getSalary() > 8000));
        // 将员工按性别分组
        Map<String, List<Person>> group = personList.stream().collect(Collectors.groupingBy(Person::getSex));
        // 将员工先按性别分组，再按地区分组
        Map<String, Map<String, List<Person>>> group2 = personList.stream().collect(Collectors.groupingBy(Person::getSex, Collectors.groupingBy(Person::getArea)));
        System.out.println("员工按薪资是否大于8000分组情况：" + part);
        System.out.println("员工按性别分组情况：" + group);
        System.out.println("员工按性别、地区：" + group2);
 }
}
```

输出结果：

```
员工按薪资是否大于8000分组情况：{false=[mutest.Person@2d98a335, mutest.Person@16b98e56, mutest.Person@7ef20235], true=[mutest.Person@27d6c5e0, mutest.Person@4f3f5b24, mutest.Person@15aeb7ab]}  

员工按性别分组情况：{female=[mutest.Person@16b98e56, mutest.Person@4f3f5b24, mutest.Person@7ef20235], male=[mutest.Person@27d6c5e0, mutest.Person@2d98a335, mutest.Person@15aeb7ab]}  

员工按性别、地区：{female={New York=[mutest.Person@4f3f5b24, mutest.Person@7ef20235], Washington=[mutest.Person@16b98e56]}, male={New York=[mutest.Person@27d6c5e0, mutest.Person@15aeb7ab], Washington=[mutest.Person@2d98a335]}}  
```

#### 3.6.4 接合(joining)

`joining`可以将stream中的元素用特定的连接符（没有的话，则直接连接）连接成一个字符串。

```
public class StreamTest {
 public static void main(String[] args) {
  List<Person> personList = new ArrayList<Person>();
  personList.add(new Person("Tom", 8900, 23, "male", "New York"));
  personList.add(new Person("Jack", 7000, 25, "male", "Washington"));
  personList.add(new Person("Lily", 7800, 21, "female", "Washington"));

  String names = personList.stream().map(p -> p.getName()).collect(Collectors.joining(","));
  System.out.println("所有员工的姓名：" + names);
  List<String> list = Arrays.asList("A", "B", "C");
  String string = list.stream().collect(Collectors.joining("-"));
  System.out.println("拼接后的字符串：" + string);
 }
}
```

运行结果：

> 所有员工的姓名：Tom,Jack,Lily 拼接后的字符串：A-B-C

#### 3.6.5 归约(reducing)

`Collectors`类提供的`reducing`方法，相比于`stream`本身的`reduce`方法，增加了对自定义归约的支持。

```
public class StreamTest {
 public static void main(String[] args) {
  List<Person> personList = new ArrayList<Person>();
  personList.add(new Person("Tom", 8900, 23, "male", "New York"));
  personList.add(new Person("Jack", 7000, 25, "male", "Washington"));
  personList.add(new Person("Lily", 7800, 21, "female", "Washington"));

  // 每个员工减去起征点后的薪资之和（这个例子并不严谨，但一时没想到好的例子）
  Integer sum = personList.stream().collect(Collectors.reducing(0, Person::getSalary, (i, j) -> (i + j - 5000)));
  System.out.println("员工扣税薪资总和：" + sum);

  // stream的reduce
  Optional<Integer> sum2 = personList.stream().map(Person::getSalary).reduce(Integer::sum);
  System.out.println("员工薪资总和：" + sum2.get());
 }
}
```

运行结果：

> 员工扣税薪资总和：8700 员工薪资总和：23700

### 3.7 排序(sorted)

sorted，中间操作。有两种排序：

- sorted()：自然排序，流中元素需实现Comparable接口
- sorted(Comparator com)：Comparator排序器自定义排序

[**案例：将员工按工资由高到低（工资一样则按年龄由大到小）排序**](http://mp.weixin.qq.com/s?__biz=MzI3ODcxMzQzMw==&mid=2247538317&idx=2&sn=baad0e54773d69c3d96f32667957a11e&chksm=eb50d3bbdc275aadb0d742940e0be274c873627ab4828c5d861dd391d135408088abb8bda792&scene=21#wechat_redirect)

```
public class StreamTest {
 public static void main(String[] args) {
  List<Person> personList = new ArrayList<Person>();

  personList.add(new Person("Sherry", 9000, 24, "female", "New York"));
  personList.add(new Person("Tom", 8900, 22, "male", "Washington"));
  personList.add(new Person("Jack", 9000, 25, "male", "Washington"));
  personList.add(new Person("Lily", 8800, 26, "male", "New York"));
  personList.add(new Person("Alisa", 9000, 26, "female", "New York"));

  // 按工资升序排序（自然排序）
  List<String> newList = personList.stream().sorted(Comparator.comparing(Person::getSalary)).map(Person::getName)
    .collect(Collectors.toList());
  // 按工资倒序排序
  List<String> newList2 = personList.stream().sorted(Comparator.comparing(Person::getSalary).reversed())
    .map(Person::getName).collect(Collectors.toList());
  // 先按工资再按年龄升序排序
  List<String> newList3 = personList.stream()
    .sorted(Comparator.comparing(Person::getSalary).thenComparing(Person::getAge)).map(Person::getName)
    .collect(Collectors.toList());
  // 先按工资再按年龄自定义排序（降序）
  List<String> newList4 = personList.stream().sorted((p1, p2) -> {
   if (p1.getSalary() == p2.getSalary()) {
    return p2.getAge() - p1.getAge();
   } else {
    return p2.getSalary() - p1.getSalary();
   }
  }).map(Person::getName).collect(Collectors.toList());

  System.out.println("按工资升序排序：" + newList);
  System.out.println("按工资降序排序：" + newList2);
  System.out.println("先按工资再按年龄升序排序：" + newList3);
  System.out.println("先按工资再按年龄自定义降序排序：" + newList4);
 }
}
```

[运行结果：](http://mp.weixin.qq.com/s?__biz=MzI3ODcxMzQzMw==&mid=2247538317&idx=2&sn=baad0e54773d69c3d96f32667957a11e&chksm=eb50d3bbdc275aadb0d742940e0be274c873627ab4828c5d861dd391d135408088abb8bda792&scene=21#wechat_redirect)

> 按工资自然排序：[Lily, Tom, Sherry, Jack, Alisa] 按工资降序排序：[Sherry, Jack, Alisa,Tom, Lily] 先按工资再按年龄自然排序：[Sherry, Jack, Alisa, Tom, Lily] 先按工资再按年龄自定义降序排序：[Alisa, Jack, Sherry, Tom, Lily]

### 3.8 提取/组合

流也可以进行合并、去重、限制、跳过等操作。

![图片](assets/640-16549491382946.png)

```
public class StreamTest {
 public static void main(String[] args) {
  String[] arr1 = { "a", "b", "c", "d" };
  String[] arr2 = { "d", "e", "f", "g" };

  Stream<String> stream1 = Stream.of(arr1);
  Stream<String> stream2 = Stream.of(arr2);
  // concat:合并两个流 distinct：去重
  List<String> newList = Stream.concat(stream1, stream2).distinct().collect(Collectors.toList());
  // limit：限制从流中获得前n个数据
  List<Integer> collect = Stream.iterate(1, x -> x + 2).limit(10).collect(Collectors.toList());
  // skip：跳过前n个数据
  List<Integer> collect2 = Stream.iterate(1, x -> x + 2).skip(1).limit(5).collect(Collectors.toList());

  System.out.println("流合并：" + newList);
  System.out.println("limit：" + collect);
  System.out.println("skip：" + collect2);
 }
}
```

运行结果：

> 流合并：[a, b, c, d, e, f, g] limit：[1, 3, 5, 7, 9, 11, 13, 15, 17, 19] skip：[3, 5, 7, 9, 11]

