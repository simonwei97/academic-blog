---
title: 92. 反转链表 II (Reverse Linked List II)
linktitle: 92. 反转链表 II
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 10
---

## 描述 (Description)

给你单链表的头指针 `head` 和两个整数 `left` 和 `right` ，其中 `left <= right` 。请你反转从位置 `left` 到位置 `right` 的链表节点，返回 **反转后的链表** 。

https://leetcode.cn/problems/reverse-linked-list-ii

**Example 1:**

> Input: head = [1,2,3,4,5], left = 2, right = 4

> Output: [1,4,3,2,5]

**Example 2:**

> Input: head = [5], left = 1, right = 1

> Output: [5]

## 提示 (Constraints)

- 链表中节点数目为 `n`
- `1 <= n <= 500`
- `-500 <= Node.val <= 500`
- `1 <= left <= right <= n`

## 分析 (Analysis)

利用虚拟头结点进行删除。穿针引线 + 翻转链表 。

`cur` 为翻转的第一个节点，即位置 `left` 所在的节点。
`next` 为 `cur` 的下一个节点。`pre` 为 `left` 位置前一个节点。

- 先将 `cur` 的下一个节点记录为 `next`；
- 把 `cur` 的下一个节点指向 `next` 的下一个节点；
- 把 `next` 的下一个节点指向 `pre` 的下一个节点；
- 把 `pre` 的下一个节点指向 `next`。

## 代码 (Code)

- 时间复杂度：`O(n)`，n 为链表长度，最多翻转一次链表。
- 空间复杂度：`O(1)`

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseBetween(head *ListNode, left int, right int) *ListNode {
    dummy := &ListNode{Val: -1, Next: head}

    pre := dummy
    for i := 0; i < left - 1; i++ {
        pre = pre.Next
    }

    cur := pre.Next
    for i := 0; i < right - left; i++ {
        next := cur.Next
        cur.Next = next.Next
        next.Next = pre.Next
        pre.Next = next
    }
    return dummy.Next
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseBetween(self, head: Optional[ListNode], left: int, right: int) -> Optional[ListNode]:
        dummy = ListNode()
        dummy.next = head

        pre = dummy
        for _ in range(left-1):
            pre = pre.next

        cur = pre.next
        for _ in range(right-left):
            _next = cur.next
            cur.next = _next.next
            _next.next = pre.next
            pre.next = _next

        return dummy.next
```

{{< /tab >}}
{{< tab tabName="C++">}}

```cpp
// TODO
```

{{< /tab >}}
{{< /tabs >}}
