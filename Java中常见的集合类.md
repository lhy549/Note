# 一、集合类 #

## Java集合类通常分为Set、List、Map和Queue4大体系。 ##

Java集合类主要由2个接口派生过来：Collection接口和Map接口！

Set代表无序的、不允许有重复元素的集合，

List代表有序的、允许有重复元素的集合，

Map代表具有映射关系的集合，

Queue代表队列集合。

## 什么是集合类？ 

 集合类主要负责保存、盛装其他数据，因此又将集合类称为容器类，本质上是一种数据结构！

 就是一种为了对多个对象进行操作而进行存储的方式。

**集合类与数组的区别是什么？**

数组：可以存储对象，也可以存储基本数据类型，但是一次只能存储一种类型，数组长度固定。

集合：只能存储对象，长度可变，可以存储不同类型的对象。

为什么出现那么多种集合的原因是什么？
　　每一种(集合)容器对数据的存储方式都有所不同，这个存储方式为：数据结构。

# 二、Collection接口 #

Collection是一个集合接口。

Collection的子接口：

Set，List，Queue这几个子接口。下面将会详细说明。
    
1.增加对象：boolean add(Object object) 如果集合中没有object，那么添加它并返回true；

　　　　　　如果集合中存在object（且该集合不能包含重复元素），则返回false。

　　　　　　另外：集合中存储的都是对象的引用（地址）。(Object可以放入任何对象）

2.获取长度：int size（）： 返回此集合中的元素个数。

3.删除元素：

　　　　　void clear（）： 清楚集合中的所有元素（除非该集合不支持clear方法）。
　　　　　boolean remove（Object o）： 删除集合中所有e.equals（e）==true的元素，并返回true。否则返回false。

　　　　　（Arraylist中改写为：移除相等的首个元素）
　　　　　Boolean removeAll（Cellection c）： 移除和集合c 的交集中的元素。

4.判断元素：
　　　　　Boolean contains（Object o）：判断集合中是否包含元素（对象）o。
　　　　　boolean containsAll（Collection c）：判断集合c是否是调用集合的子集。

5.交集： boolean retainAll（Cellection c）： 仅保留和集合c的交集。

三、元素的取出（迭代器）
　　　　　　迭代器： 就是一个Iterator接口的子类对象，封装了取出其绑定集合的元素的方式。

　　　　　　　　步骤： 1、通过调用集合的 Iterator iterator（）方法返回该集合的迭代器，
　　　　　　　　　　　 2、将此迭代器赋值给 一个 Iterator 型对象引用。 
　　　　　　　　　　　 3、通过此引用，调用迭代器的方法操作集合：
　　　　　　　　　　　　　　1）、boolean hasNext（）：如果集合中任有元素可以迭代，则返回true。
　　　　　　　　　　　　　　2）、Object next（）：返回迭代的下一个元素（列表中还在）。
　　　　　　　　　　　　　　3）、void remove（）：从迭代器指向的集合中 移除 迭代器返回的最后一个元素。

　　　　　　　　注意：你不能同时用迭代器和集合同时去操作同一组元素， 有可能会抛出并发异常。
　　　　　　　　原因：迭代器已经创建， 之后通过集合方法操作的元素过程（比如说增加），迭代器并不知道集合做了什么操作，还是只能
　　　　　　　　　　　按照原来的元素列表操作，就会发生错误。 

 
List(子接口):有序的、允许有重复元素的集合

特点：元素是有序的， 而且元素可以重复。该类集合中有索引。	

List集合特有的常见方法：

1、凡是可以操作索引的的方法都是List特有的方法。
* 增：
 
　　void add(int index ，Object object)；
　　Boolean add（int index， Collection c）；

* 删：
 
　　remove（index）：返回了移除的元素。

* 改：
 
　　set（index， element）：在指定角标放入指定元素，返回原来的元素。

- 查：

　　get（index）：返回index上的元素
　　subList（start，end）：返回一个自己列表（依赖于原集合）

　**注意：List集合特有的迭代器：listIterator（）； 列表迭代器 （注意与iterator区别）**

### listIterator：  ###

1、定义：

　　是iteretor的子接口。
　　在进行迭代操作的时候，不能使用集合方法对同组元素进行操作（原因在iterator讲解处）。
　　而iterator的操作方法又比较少（只有判断、查找、删除，没有添加），局限了对元素组的课操作性。
　　所以在list集合中就定义了新的迭代器： listIterator。

2、listIterator中新增的方法：
　　　(1)、void add（）： 在返回的元素后面的加入一个新元素
　　　(2)、void set（object）： 使用新元素替换返回的最后一个元素。
　　　(3)、Boolean hasPrevious（）： 逆向遍历列表（相对应： hasNext（））

　　　　list 集合在涉及到需要判断元素是否相同时，底层调用的都是equals方法。（contains、 remove方法等） 

### list集合下，常见三大集合 ###

- ArrayList：底层数据结构使用数组结构： 查询速度快。但是增删稍慢。（线程不同步，数组0.5倍延长）　　
- Linkedlist：底层使用链表数据结构： 增删速度快，但是查询慢。　　　　
- Vector：底层是数组数据结构：查询赠删慢（线程同步，数组百分百延长）已经被ArrayList取代。

## Set(子接口):无序的、不允许有重复元素的集合 ##

特点：元素是无序（存入和取出的顺序不一定一致）的，而且元素不能重复。 该类集合中没有索引。

Set集合下常见的子类集合：
　　　HashSet：底层数据结构式： 哈希表。
　　　TreeSet：	

### HashSet: 

特点：元素无序（存入和取出的顺序一定不一样），而且元素唯一，没有索引。

底层数据： 底层使用哈希表作为数据结构。

元素唯一性： 是通过元素的两个方法： hashCode 和 equals 来完成的。
　　　　　　　如果两个元素的HashCode值相同，就会判断equals是否为true。
　　　　　　　如果两个元素的HashCode值不同，就不会调用equals方法。

**注意：对于判断元素是否存在、删除等操作，都依赖于元素的hashCode、equals等方法。**

　　　哈希表：给定表M，存在函数f(key)，对任意给定的关键字值key，代入函数后若能得到包含该关键字的记录在表中的地址，
　　　则称表M为哈希(Hash)表，函数f(key)为哈希(Hash) 函数。	

　　（哈希值与内存地址值之间的关系：默认的哈希值是内存地址值计算的哈希值，但是只是为了给人看的，真正在
　　　内存中还是依靠内存地址值来进行运算的，而不是哈希值）	

### TreeSet: 

底层数据结构： 二叉树 （保证元素唯一性的方法是保证compareTo 方法return 0）

比较方式： 方式一、就是让元素自己具有比较性，元素需要实现comparable接口，重写其中得compareTo方法，这个排序叫做自然排序（默认排序）

　　1、 无序性（按照输入元素类中自定义的compareTo方法来排定存储对象。）	

　　2、 单一性（通过判断元素类中自定义的compareTo方法放回值是否为0来判断元素是否相等。）

　　3、 让需要存入到TreeSet中的元素，实现comparable接口，该接口中定义了一个public int compareTo方法	

　　4、 compareTo 方法：我们需要在类定义中重写该方法， public int compareTo， 
　　　　　使得： 当有e.compareTo(e1)时， 
　　　　　如果e大于e1则返回正数，当e小于e1则返回负数， 等于则返回0.
　　　　　而且当有e等于e1时， 可以定义附属判断条件来判断 两个对象的大小。

**注意：TreeSet 本情况的所有的底层比较原理只是调用了元素的compareTo方法，与 equals等方法都无关。**
　　　　　　（add、contains、remove等需要用到比较的方法）
　　　　　　所以我们定义所有的比较都返回正数，那么靠遍历迭代器取出的元素顺序和存入顺序一样。
　　　　　　如果定义所有的比较都返回负数，那么靠遍历迭代器去除的元素顺序和存入的顺序相反。
　　　　　　如果定义所有比较都返回0 ，那么就只能存入一个元素，最后也只能取出一个元素。

# 三.Map接口 #

map也是一个接口集合，只不过和Collection不同的是，map是以键值对的方式存储数据。
Map代表具有映射关系的集合

map下的子接口:










