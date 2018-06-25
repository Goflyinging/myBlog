---
title: list之ArrayList
date: 2018-06-24
categories: collection
tags: [collection,list]
---
## ArrayList

ArrayList 是 List 接口的可变数组的实现

### 实现的接口
- 继承 AbstractList (实现了 List 接口)
- Cloneable 可克隆
- Serializable 可序列化
- RandomAccess 为List提供快速访问功能(RandomAccess 为空接口，只是一个可以快速访问的标识)，比如在Collections 使用 list instanceof RandomAccess，所以该接口只是一个标识

### 构造方法
- 不带参数的构造方法 创建一个空数据即默认大小为0，当调用add*方法时会对其进行初始化，add方法默认创建大小为10的数据

- 创建指定长度数组，小于 0 抛出异常，等于0 会创建一个空数组，即EMPTY_ELEMENTDATA

- 根据集合创建数组，创建长度为集合长度的数组并拷贝

### 增删查方法

- get(int index) 获取指定位置的集合对象

- iterator 调用迭代器遍历list集合

- set 方法，指定位置赋值，检查 index ，如果不合法则抛出异常

- add 方法，末尾位置添加，如果超出，扩容1.5倍；

- add(int index,Object obj) 指定位置添加，检查 index ，如不合法则抛出异常。指定位置插入时，会将原来的数组以 index 为界，将 index 后的数据后移一位，后移的实现通过 System.arraycopy 方法实现。再在 index 位置插入需要插入的数据。 System.arraycopy 为 Native 层的方法，可以高效复制数组元素。

- remove(int index) 根据索引删除，直接操作数组，返回值为被移除的对象。将该对象所在位置之后的数组内容复制到从该位置开始，将末尾置为 null

- remove(Object obj) 根据对象删除，遍历数组，如果存在，将该对象所在位置之后的数组内容复制到从该位置开始，将末尾置为 null
### Fail-Fast机制
　　ArrayList也采用了快速失败的机制，通过记录modCount参数来实现。在面对并发的修改时，迭代器很快就会完全失败，而不是冒着在将来某个不确定时间发生任意不确定行为的风险。
### 总结
- 底层使用数组实现，顺序存储。
- 当我们可预知要保存的元素的多少时，要在构造 ArrayList 实例时，就指定其容量，以避免数组扩容的发生。或者根据实际需求，通过调用ensureCapacity 方法来手动增加 ArrayList 实例的容量。
- ArrayList基于数组实现，可以通过下标索引直接查找到指定位置的元素，因此查找效率高，但每次插入或删除元素，就要大量地移动元素，插入删除元素的效率低。
- ArrayList中允许元素为null，在remove(Object o)，将o分为null和不为null两种情况处理。
