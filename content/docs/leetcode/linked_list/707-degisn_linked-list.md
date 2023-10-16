---
title: 707. 设计链表 (Design Linked List)
linktitle: 707. 设计链表
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

## 描述 (Description)

https://leetcode.com/problems/design-linked-list/description/

你可以选择使用单链表或者双链表，设计并实现自己的链表。

单链表中的节点应该具备两个属性：`val` 和 next 。`val` 是当前节点的值，`next` 是指向下一个节点的指针/引用。

如果是双向链表，则还需要属性 `prev` 以指示链表中的上一个节点。假设链表中的所有节点下标从 `0` 开始。

实现 `MyLinkedList` 类：

- `MyLinkedList()` 初始化 `MyLinkedList` 对象。
- `int get(int index)` 获取链表中下标为 `index` 的节点的值。如果下标无效，则返回 -1 。
- `void addAtHead(int val)` 将一个值为 `val` 的节点插入到链表中第一个元素之前。在插入完成后，新节点会成为链表的第一个节点。
- `void addAtTail(int val)` 将一个值为 `val` 的节点追加到链表中作为链表的最后一个元素。
- `void addAtIndex(int index, int val)` 将一个值为 `val` 的节点插入到链表中下标为 `index` 的节点之前。如果 `index` 等于链表的长度，那么该节点会被追加到链表的末尾。如果 `index` 比长度更大，该节点将 不会插入到链表中。
- `void deleteAtIndex(int index)` 如果下标有效，则删除链表中下标为 `index` 的节点。

**Example 1:**

> Input: ["MyLinkedList", "addAtHead", "addAtTail", "addAtIndex", "get", "deleteAtIndex", "get"] > [[], [1], [3], [1, 2], [1], [1], [1]]

> Output: [null, null, null, null, 2, null, 3]

## 提示 (Constraints)

- `0 <= index, val <= 1000`

## 分析 (Analysis)

利用虚拟头结点进行删除。

## 代码 (Code)

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
type SingleNode struct {
    Val  int
    Next *SingleNode
}

type MyLinkedList struct {
    dummyHead *SingleNode
    Size      int
}

func Constructor() MyLinkedList {
    newNode := &SingleNode{
        Val: -999,
        Next: nil,
    }
    return MyLinkedList{
        dummyHead: newNode,
        Size: 0,
    }
}


func (this *MyLinkedList) Get(index int) int {
    if this == nil || index < 0 || index >= this.Size {
        return -1
    }

    curr := this.dummyHead.Next
    for i := 0; i < index; i++ {
        curr = curr.Next
    }
    return curr.Val
}


func (this *MyLinkedList) AddAtHead(val int)  {
    newNode := &SingleNode{Val: val}
    newNode.Next = this.dummyHead.Next
    this.dummyHead.Next = newNode
    this.Size++
    // this.AddAtIndex(0, val)
}


func (this *MyLinkedList) AddAtTail(val int)  {
    newNode := &SingleNode{Val: val}
    curr := this.dummyHead
    for curr.Next != nil {
        curr = curr.Next
    }

    curr.Next = newNode
    this.Size++
    // this.AddAtIndex(this.Size, val)
}


func (this *MyLinkedList) AddAtIndex(index int, val int)  {
    if index < 0 {
        index = 0
    } else if index > this.Size {
        return
    }

    newNode := &SingleNode{Val: val}
    curr := this.dummyHead
    for i := 0; i < index; i++ {
        curr = curr.Next
    }
    newNode.Next = curr.Next
    curr.Next = newNode
    this.Size++
}


func (this *MyLinkedList) DeleteAtIndex(index int)  {
    if index < 0 || index >= this.Size {
        return
    }

    curr := this.dummyHead
    for i := 0; i < index; i++ {
        curr = curr.Next
    }
    if curr.Next != nil {
        curr.Next = curr.Next.Next
    }
    this.Size--
}


/**
 * Your MyLinkedList object will be instantiated and called as such:
 * obj := Constructor();
 * param_1 := obj.Get(index);
 * obj.AddAtHead(val);
 * obj.AddAtTail(val);
 * obj.AddAtIndex(index,val);
 * obj.DeleteAtIndex(index);
 */
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```py
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class MyLinkedList:
    def __init__(self):
        self.dummy_head = ListNode()
        self.size = 0

    def get(self, index: int) -> int:
        if index < 0 or index >= self.size:
            return -1

        current = self.dummy_head.next
        for i in range(index):
            current = current.next

        return current.val

    def addAtHead(self, val: int) -> None:
        self.dummy_head.next = ListNode(val, self.dummy_head.next)
        self.size += 1

    def addAtTail(self, val: int) -> None:
        current = self.dummy_head
        while current.next:
            current = current.next
        current.next = ListNode(val)
        self.size += 1

    def addAtIndex(self, index: int, val: int) -> None:
        if index < 0 or index > self.size:
            return

        current = self.dummy_head
        for i in range(index):
            current = current.next
        current.next = ListNode(val, current.next)
        self.size += 1

    def deleteAtIndex(self, index: int) -> None:
        if index < 0 or index >= self.size:
            return

        current = self.dummy_head
        for i in range(index):
            current = current.next
        current.next = current.next.next
        self.size -= 1


# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)
```

{{< /tab >}}

{{< /tabs >}}
