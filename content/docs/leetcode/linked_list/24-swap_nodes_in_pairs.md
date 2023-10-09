---
title: 24. 两两交换链表中的节点 (Swap Nodes In Pairs)
linktitle: 24. 两两交换链表中的节点
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 4
---

## 描述 (Description)

给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即只能进行**节点交换**）。

https://leetcode.cn/problems/swap-nodes-in-pairs/

**Example 1:**

> Input: head = [1,2,3,4]

> Output: [2,1,4,3]

**Example 2:**

> Input: head = []

> Output: []

**Example 3:**

> Input: head = [1]

> Output: [1]

## 提示 (Constraints)

- 链表中节点的数目在范围 `[0, 100]` 内
- `0 <= Node.val <= 100`

## 分析 (Analysis)

利用虚拟头结点进行。

## 代码 (Code)

- 时间复杂度：
  - `O(n)`：两两交换需要遍历整个链表，每次操作需要 `O(1)` 复杂度
- 空间复杂度：
  - `O(1)`：使用常数级的额外空间，不随 `N` 变化

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
func swapPairs(head *ListNode) *ListNode {
    dummy := &ListNode{Next: head}
    cur := dummy
    for cur.Next != nil && cur.Next.Next != nil {
        // cur->1->2->3->4
        // cur  1  2  3  4
        // cur->2->1->3->4
        tmp1 := cur.Next  // 1
        tmp2 := cur.Next.Next.Next // 3

        cur.Next = cur.Next.Next  // cur.Next.Next=2
        cur.Next.Next = tmp1
        cur.Next.Next.Next = tmp2

        cur = cur.Next.Next // 1
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
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(next=head)
        curr = dummy

        while curr.next and curr.next.next:
            tmp1 = curr.next
            tmp2 = curr.next.next.next

            curr.next = curr.next.next
            curr.next.next = tmp1
            curr.next.next.next = tmp2

            curr = curr.next.next

        return dummy.next
```

{{< /tab >}}

{{< /tabs >}}
