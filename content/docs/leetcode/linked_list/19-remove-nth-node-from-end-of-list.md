---
title: 19.删除链表的倒数第N个节点 (Swap Nodes In Pairs)
linktitle: 19.删除链表的倒数第N个节点
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
---

## 描述 (Description)

给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

https://leetcode.cn/problems/remove-nth-node-from-end-of-list/

**Example 1:**

> Input: head = [1,2,3,4,5], n = 2

> Output: [1,2,3,5]

**Example 2:**

> Input: head = [1], n = 1

> Output: []

**Example 3:**

> Input: head = [1,2], n = 1

> Output: [1]

## 提示 (Constraints)

- 链表中结点的数目为 sz
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

## 分析 (Analysis)

利用 **虚拟头结点** 和 **快慢指针** 实现。

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
func removeNthFromEnd(head *ListNode, n int) *ListNode {
    dummy := &ListNode{Next: head, Val: 0}
    slow := dummy
    fast := dummy
    for n > 0 && fast != nil {
        fast = fast.Next
        n--
    }

    fast = fast.Next // n + 1，让slow指向删除节点的上一个节点
    for fast != nil {
        fast = fast.Next
        slow = slow.Next
    }
    slow.Next = slow.Next.Next
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
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        fast, slow = dummy, dummy
        for i in range(n):
            fast = fast.next

        fast = fast.next
        while fast:
            fast = fast.next
            slow = slow.next

        slow.next = slow.next.next
        return dummy.next
```

{{< /tab >}}

{{< /tabs >}}
