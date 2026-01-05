### 集合之Map

##### HashMap源码解析

​	HashMap map = new HashMap():

 * 在实例化以后，底层创建了长度是16的一维数组Entry[] table。

 * ...可能已经执行过多次put...

 * map.put(key1,value1):

 * 首先，调用key1所在类的hashCode()计算key1哈希值，此哈希值经过某种算法计算以后，得到在Entry数组中的存放位置。

 * 如果此位置上的数据为空，此时的key1-value1添加成功。 ----情况1

 * 如果此位置上的数据不为空，(意味着此位置上存在一个或多个数据(以链表形式存在)),比较key1和已经存在的一个或多个数据的哈希值：

 * 如果key1的哈希值与已经存在的数据的哈希值都不相同，此时key1-value1添加成功。----情况2

 * 如果key1的哈希值和已经存在的某一个数据(key2-value2)的哈希值相同，继续比较：调用key1所在类的equals(key2)方法，比较：如果equals()返回false:此时key1-value1添加成功。----情况3

 * 如果equals()返回true:使用value1替换value2。
    *

 * 补充：关于情况2和情况3：此时key1-value1和原来的数据以链表的方式存储。
    *

 * 在不断的添加过程中，会涉及到扩容问题，当超出临界值(且要存放的位置非空)时，扩容。默认的扩容方式：扩容为原来容量的2倍，并将原有的数据复制过来。
    *

   ###### jdk8 相较于jdk7在底层实现方面的不同：

 * 1. new HashMap():底层没有创建一个长度为16的数组

 * 2. jdk 8底层的数组是：Node[],而非Entry[]

 * 3. 首次调用put()方法时，底层创建长度为16的数组

 * 4. jdk7底层结构只有：数组+链表。jdk8中底层结构：数组+链表+红黑树。

 *         4.1 形成链表时，七上八下（jdk7:新的元素指向旧的元素。jdk8：旧的元素指向新的元素）
           4.2 当数组的某一个索引位置上的元素以链表形式存在的数据个数 > 8 且当前数组的长度 > 64时，此时此索引位置上的所数据改为使用红黑树存储(*<u>这里的红黑树存储根TreeMap或者TreeSet的红黑树有本质区别,这里只关心对象的Hash值进行红黑时二叉排列,而后者使用的是对象的排序接口实现的对象间排序</u>*)。
            *
           
 * DEFAULT_INITIAL_CAPACITY : HashMap的默认容量，16

 * DEFAULT_LOAD_FACTOR：HashMap的默认加载因子：0.75

 * threshold：扩容的临界值，=容量*填充因子：16 * 0.75 => 12

 * TREEIFY_THRESHOLD：Bucket中链表长度大于该默认值，转化为红黑树:8

 *      MIN_TREEIFY_CAPACITY：桶中的Node被树化时最小的hash表容量:64

##### Collecitons操作集合的工具类(包括Collection和Map)

reverse(List)：反转 List 中元素的顺序
shuffle(List)：对 List 集合元素进行随机排序
sort(List)：根据元素的自然顺序对指定 List 集合元素按升序排序
sort(List，Comparator)：根据指定的 Comparator 产生的顺序对 List 集合元素进行排序

binarySearch(List<? extends Comparable<? super T>> list, T key)二分法读取

swap(List，int， int)：将指定 list 集合中的 i 处元素和 j 处元素进行交换

Object max(Collection)：根据元素的自然顺序，返回给定集合中的最大元素
Object max(Collection，Comparator)：根据 Comparator 指定的顺序，返回给定集合中的最大元素
Object min(Collection)
Object min(Collection，Comparator)
int frequency(Collection，Object)：返回指定集合中指定元素的出现次数
void copy(List dest,List src)：将src中的内容复制到dest中
boolean replaceAll(List list，Object oldVal，Object newVal)：使用新值替换 List 对象的所有旧值

##### Arrays操作数组的工具类

toString返回数组的字符串形式

sort 排序(自然排序和定制排序)

binarySearch通过二分搜索法进行查找,要求必须排好序

copyOf 数组元素的复制

fill 数组元素的填充

equals 比较两个数组元素内容是否完全一致

asList将一组值,转换成list