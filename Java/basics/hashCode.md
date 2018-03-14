---
title: hashCode
date: 2018-03-14
categories: basics
tags: [basics,java]
---

## hashCode 重写方法

- 把某个非零的常数值，比如说17，保存在一个名为 result 的 int 类型的变量中。
- 对于对象中每个关键域f（指 equals 方法中涉及的每个域），完成以下步骤：
  - 为该域计算 int 类型的散列码 c :
    - 如果该域是 boolean 类型，则计算 (f ? 1 : 0) .
    - 如果该域是 byte 、 char 、 short 或者 int 类型，则计算 (int)f 。
    - 如果该域是 long 类型，则计算 (int)(f ^ (f >>> 32)) 。
    - 如果该域是 float 类型，则计算 Float.floatToIntBits(f) 。
    - 如果该域是 double 类型，则计算 Double.doubleToLongBits(f) ，然后按照上面步骤为得到的 long 类型值计算散列值。
    - 如果该域是一个对象引用，并且该域的 equals 方法通过递归地调用 equals 的方式来比较这个域，则同样为这个域递归地调用 hashCode 。如果需要更复杂的比较，则为这个域计算一个“范式（canonical representation）”，然后针对这个范式调用 hashCode 。如果这个域的值为 null ，则返回0（或者其他某个常数，但通常是0）。
    - 如果该域是一个数组，则要把每一个元素当做单独的域来处理。也就是说，递归地应
用上述规则，对每个重要的元素计算一个散列码，然后根据步骤2.b中的做法把这些散列
值组合起来。如果数组域中的每个元素都很重要，可以利用发行版本1.5中增加的其中一个 Arrays.hashCode 方法。
  - 按照下面的公式，把步骤2.a中计算得到的散列码 c 合并到 result 中：
result = 31 * result + c;
- 返回result。
- 写完了 hashCode 方法之后，问问自己“相等的实例是否都具有相等的散列码”。要编写单
元测试来验证你的推断。如果相等实例有着不相等的散列码，则要找出原因，并修正错
误。
