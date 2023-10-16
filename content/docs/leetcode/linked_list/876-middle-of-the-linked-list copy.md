---
title: 876. 链表的中间结点 (Middle of the Linked List)
linktitle: 876. 链表的中间结点
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 9
---

## 描述 (Description)

给你单链表的头结点 `head` ，请你找出并返回链表的中间结点。

如果有两个中间结点，则返回第二个中间结点。

https://leetcode.com/problems/middle-of-the-linked-list/

**Example 1:**

> Input: head = [1,2,3,4,5]

> Output: [3,4,5]

**Example 2:**

> Input: head = [1,2,3,4,5,6]

> Output: [4,5,6]

## 提示 (Constraints)

- 链表的结点数范围是 `[1, 100]`
- `1 <= Node.val <= 100`

## 分析 (Analysis)

利用 **快慢指针** 实现。

## 代码 (Code)

- 时间复杂度：
  - $O(n)$：`n` 代表链表 `head` 的长度。
- 空间复杂度：
  - $O(1)$：未使用额外空间存储

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
func middleNode(head *ListNode) *ListNode {
    slow, fast := head, head
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
    }
    return slow
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
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        return slow
```

{{< /tab >}}

{{< /tabs >}}
