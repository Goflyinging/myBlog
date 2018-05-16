---
title: memory analyzer tool
date: 2018-05-16
categories: jvm
tags: [jvm,mat]
---
# memory analyzer tool
##  基本概念
###  Shallow Heap
Shallow size就是对象本身占用内存的大小，不包含其引用的对象内存，也就是对象头(Mark Word（标记字段）和 class Pointer（类型指针）)加成员变量（不是成员变量的值）的总和。
- 常规对象（非数组）的ShallowSize由其成员变量的数量和类型决定
- 数组的shallow size有数组元素的类型（对象类型、基本类型）和数组长度决定

###  Retained Heap
retained heap值的计算方式是将retained set中的所有对象大小叠加。或者说，由于X被释放，导致其它所有被释放对象（包括被递归释放的）所占的heap大小。
####  Retained Set
当X被回收时那些将被GC回收的对象集合。

把内存中的对象看成下图中的节点，并且对象和对象之间互相引用。这里有一个特殊的节点GC Roots，这就是reference chain的起点。
![](/img/jvm/retained_objects.png "Retained Set")
从obj1入手，上图中蓝色节点代表仅仅只有通过obj1才能直接或间接访问的对象。因为可以通过GC Roots访问，所以左图的obj3不是蓝色节点；而在右图却是蓝色，因为它已经被包含在retained集合内。所以对于左图，obj1的retained size是obj1、obj2、obj4的shallow size总和；右图的retained size是obj1、obj2、obj3、obj4的shallow size总和。obj2的retained size可以通过相同的方式计算。

###  Path to GC Roots
查看一个对象到RC Roots的引用链
通常在排查内存泄漏的时候，我们会选择exclude all phantom/weak/soft etc.references,
意思是查看排除虚引用/弱引用/软引用等的引用链，因为被虚引用/弱引用/软引用的对象可以直接被GC给回收，我们要看的就是某个对象否还存在Strong 引用链（在导出HeapDump之前要手动出发GC来保证），如果有，则说明存在内存泄漏，然后再去排查具体引用。

###  查看当前Object所有引用,被引用的对象
####  List objects with （以Dominator Tree的方式查看）
- incoming references 引用到该对象的对象
- outcoming references 被该对象引用的对象
####  Show objects by class （以class的方式查看）
- incoming references 引用到该对象的对象
- outcoming references 被该对象引用的对象

##  相关功能
###  Histogram （直方图）视图
- Objects:类的对象的数量。
- Shallow Heap：就是对象本身占用内存的大小，不包含对其他对象的引用，也就是对象头加成员变量（不是成员变量的值）的总和。
- Retained Heap：是该对象自己的shallow size，加上从该对象能直接或间接访问到对象的shallow size之和。换句话说，retained size是该对象被GC之后所能回收到内存的总和。
###  Dominator Tree（支配树）视图
在此视图中列出了每个对象与其引用关系的树状结构，同时包含了占用内存的大小和百分比。

###  Top consumers
这里显示了内存中最大的对象有哪些，他们对应的类是哪些，类加载器classloader是哪些。

###  Leak Suspects
通过MA自动分析泄漏的原因
