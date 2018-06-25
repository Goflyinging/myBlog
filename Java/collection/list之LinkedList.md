---
title: list之LinkedList
date: 2018-06-24
categories: collection
tags: [collection,list]
---
## LinkedList

LinkedList是List和Deque接口的双向链表的实现。实现了所有可选列表操作，并允许包括null值。
``` java
private static class Node<E> {
    E item;    // 当前节点所包含的值
    Node<E> next;   //下一个节点
    Node<E> prev;    //上一个节点
    Node(Node<E> prev, E element, Node<E> next) {
        this.item = element;
        this.next = next;
        this.prev = prev;
    }
}

```

### 实现的接口
- 继承 AbstractSequentialList，AbstractSequentialList 实现了get(int index)、set(int index, E element)、add(int index, E element) 和 remove(int index)这些随机访问的函数，那么LinkedList也实现了这些随机访问的接口。
- 实现了List接口
- 实现了Deque接口，Deque操作提供了offerFirst(E e)、offerLast(E e)、peekFirst()、peekLast()、pollFirst()、pollLast()、push(E e)、pop()、removeFirstOccurrence(Object o)、removeLastOccurrence(Object o)这些方法。
- Cloneable 可克隆
- Serializable 可序列化

### 构造方法
- LinkedList(Collection<? extends E> c)
- LinkedList()

### 查 增 改 删方法

- getFirst()、getLast()、listIterator、get(int index)、peek()查看第一个元素、element()查看第一个元素，若为null将抛出异常、poll()弹出第一个元素，并将其从链表中删除。peekFirst()、peekLast()、pollFirst() 、pollLast()同理.

- add(E e)、addLast(E e)、addFirst(E e)、add(int index, E element)、push(E e)

- set(int index, E element)

- remove(Object o)、remove(int index)、pop()、clear()

### Fail-Fast机制
　　LinkedList也采用了快速失败的机制，通过记录modCount参数来实现。在面对并发的修改时，迭代器很快就会完全失败，而不是冒着在将来某个不确定时间发生任意不确定行为的风险。
### 总结
- LinkedList是List接口的双向链表非同步实现，并允许包括null在内的所有元素。
- LinkedList可用于实现栈和队列
