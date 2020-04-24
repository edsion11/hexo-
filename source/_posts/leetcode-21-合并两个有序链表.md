---
title: leetcode-21-合并两个有序链表
date: 2020-04-20 15:27:03
tags:
  - leetcode
  - 递归
  - 双指针
---

#### 题目

将两个升序链表合并为一个新的升序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

#### 示例

```java
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

看到这道题第一个思路就是遍历其中一个链表，依次插入另一个链表。这个方法在官方解释为“迭代法”。
即我们假设`l1`元素严格比`l2`元素少，我们可以将`l2`中的元素逐一插入`l1`中正确的位置。

#### 算法思路

首先建立一个新链表，指向空，接着建立一个“哨兵节点”`prevNode`用于不断`next`下一个添加新元素。重复遍历判断`l1`和`l2`的值，两者较小值插入，然后`prevNode.next`。一直到最后其中一个链表到达尾部指向 `null`,此时另一个链表剩余值一定比目前这个值大，所以直接连接在`prevNode`后面即可。具体实现如下：

```javascript
var mergeTwoLists = function (l1, l2) {
  var prevHead = new ListNode(-1)
  var prevNode = prevHead
  while (l1 != null && l2 != null) {
    if (l1.val <= l2.val) {
      prevNode.next = l1
      l1 = l1.next
    } else {
      prevNode.next = l2
      l2 = l2.next
    }
    prevNode = prevNode.next
  }
  prevNode.next = l1 ? l1 : l2
  return prevHead.next
}
```

另一种方法是用递归方法，递归思想：递归的定义操作`merge`,比较两个链表头部较小的一个与剩下元素的`merge`操作结果合并。

#### 递归算法思路

先判断递归终值，即判断`l1` ,`l2`为`null`的时候，`return`的值。递归内容：如果`l1`的`val`值更小，则将`l1.next`与排序好的链表头相接，`l2`同理。

##### 具体实现如下

```javascript
var mergeLists = function (l1, l2) {
  if (l1 === null) {
    return l2
  }
  if (l2 === null) {
    return l1
  }
  if (l1.val < l2.val) {
    l1.next = mergeLists(l1.next, l2)
    return l1
  } else {
    l2.next = mergeLists(l1, l2.next)
    return l2
  }
}
```
