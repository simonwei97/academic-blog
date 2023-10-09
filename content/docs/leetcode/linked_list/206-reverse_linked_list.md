---
title: 206. 反转链表 (Reverse Linked List)
linktitle: 206. 反转链表
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
---

## 描述 (Description)

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

https://leetcode.cn/problems/reverse-linked-list/

**Example 1:**

![](/docs/leetcode/reverse_linked_list.jpeg)

> Input: head = [1,2,3,4,5]

> Output: [5,4,3,2,1]

**Example 2:**

> Input: head = [1,2]

> Output: [2,1]

**Example 3:**

> Input: head = []

> Output: []

## 提示 (Constraints)

- 链表中节点的数目范围是 `[0, 5000]`
- `-5000 <= Node.val <= 5000`

## 分析 (Analysis)

利用虚拟头结点进行删除。

## 代码 (Code)

- 时间复杂度：`O(n)`
- 空间复杂度：`O(1)`

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
type ListNode struct {
    Val int
    Next *ListNode
}

func reverseList(head *ListNode) *ListNode {
    var prev *ListNode
    for head != nil {
        //      1->2->3->4->5
        // tmp     2->3->4->5
        // null<-1
        tmp := head.Next
        head.Next = prev
        prev = head
        head = tmp
    }
    return prev
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```py
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next


```

{{< /tab >}}
{{< tab tabName="C++">}}

```cpp

```

{{< /tab >}}
{{< /tabs >}}
