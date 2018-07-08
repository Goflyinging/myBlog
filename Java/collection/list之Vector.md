---
title: list之Vector
date: 2018-07-02
categories: collection
tags: [collection,list]
---
## Vector
```
public class Vector<E>
    extends AbstractList<E>
    implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```
　　Vector是矢量队列，它是JDK1.0版本添加的类。继承于AbstractList，实现了List, RandomAccess, Cloneable这些接口。
- Vector 继承了AbstractList，实现了List；所以，它是一个队列，支持相关的添加、删除、修改、遍历等功能。
- Vector 实现了RandmoAccess接口，即提供了随机访问功能。RandmoAccess是java中用来被List实现，为List提供快速访问功能的。在Vector中，我们即可以通过元素的序号快速获取元素对象；这就是快速随机访问。
- Vector 实现了Cloneable接口，即实现clone()函数。它能被克隆。  

　　和ArrayList不同，Vector中的操作是线程安全的。
```
public class Vector<E>
    extends AbstractList<E>
    implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```
### 构造方法
```
synchronized boolean        add(E object)
             void           add(int location, E object)
synchronized boolean        addAll(Collection<? extends E> collection)
synchronized boolean        addAll(int location, Collection<? extends E> collection)
synchronized void           addElement(E object)
synchronized int            capacity()
             void           clear()
synchronized Object         clone()
             boolean        contains(Object object)
synchronized boolean        containsAll(Collection<?> collection)
synchronized void           copyInto(Object[] elements)
synchronized E              elementAt(int location)
             Enumeration<E> elements()
synchronized void           ensureCapacity(int minimumCapacity)
synchronized boolean        equals(Object object)
synchronized E              firstElement()
             E              get(int location)
synchronized int            hashCode()
synchronized int            indexOf(Object object, int location)
             int            indexOf(Object object)
synchronized void           insertElementAt(E object, int location)
synchronized boolean        isEmpty()
synchronized E              lastElement()
synchronized int            lastIndexOf(Object object, int location)
synchronized int            lastIndexOf(Object object)
synchronized E              remove(int location)
             boolean        remove(Object object)
synchronized boolean        removeAll(Collection<?> collection)
synchronized void           removeAllElements()
synchronized boolean        removeElement(Object object)
synchronized void           removeElementAt(int location)
synchronized boolean        retainAll(Collection<?> collection)
synchronized E              set(int location, E object)
synchronized void           setElementAt(E object, int location)
synchronized void           setSize(int length)
synchronized int            size()
synchronized List<E>        subList(int start, int end)
synchronized <T> T[]        toArray(T[] contents)
synchronized Object[]       toArray()
synchronized String         toString()
synchronized void           trimToSize()
```

### 遍历方式

- 通过迭代器遍历
```
 for(Iterator iter = list.iterator(); iter.hasNext(); ) {
    iter.next();
}
```
- 随机访问，通过索引值去遍历

  ```
  Integer value = null;
  int size = vec.size();
  for (int i=0; i<size; i++) {
      value = (Integer)vec.get(i);        
  }
  ```

- foreach循环
```
Integer value = null;
for (Integer integ:vec) {
    value = integ;
}
```

- Enumeration遍历
```
Integer value = null;
Enumeration enu = vec.elements();
while (enu.hasMoreElements()) {
    value = (Integer)enu.nextElement();
}
```

### 总结
- elementData 是"Object[]类型的数组"，它保存了添加到Vector中的元素。elementData是个动态数组，如果初始化Vector时，没指定动态数组的大小，则使用默认大小10。随着Vector中元素的增加，Vector的容量也会动态增长，capacityIncrement是与容量增长相关的增长系数：
```
int newCapacity = oldCapacity + ((capacityIncrement > 0) ?capacityIncrement : oldCapacity)
```
- elementCount 是动态数组的实际大小。

- capacityIncrement 是动态数组的增长系数。
