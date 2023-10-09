---
title: 141. 环形链表 I (Linked List Cycle I)
linktitle: 141. 环形链表 I
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 7
---

## 描述 (Description)

给你一个链表的头节点 `head` ，判断链表中是否有环。

如果链表中有某个节点，可以通过连续跟踪 `next` 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 `0` 开始）。注意：`pos` 不作为参数进行传递 。仅仅是为了标识链表的实际情况。

如果链表中存在环 ，则返回 `true` 。 否则，返回 `false` 。

**不允许修改** 链表。

https://leetcode.cn/problems/linked-list-cycle-i/

**Example 1:**

> Input: head = [3,2,0,-4], pos = 1

> Output: true

**Example 2:**

> Input: head = [1,2], pos = 0

> Output: true

**Example 3:**

> Input: head = [1], pos = -1

> Output: false

## 提示 (Constraints)

- 链表中节点的数目范围在范围 `[0, 104]` 内
- `-10^5 <= Node.val <= 10^5`
- `pos` 的值为 `-1` 或者链表中的一个 **有效索引**

## 分析 (Analysis)

利用 **快慢指针** 实现。

## 代码 (Code)

- 时间复杂度：
  - `O(n)`：`n` 代表链表 `head` 的长度。
- 空间复杂度：
  - `O(1)`：只使用了两个指针的额外空间。

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
func hasCycle(head *ListNode) bool {
    if head == nil || head.Next == nil {
        return false
    }

    slow, fast := head, head.Next
    for fast != nil && fast.Next != nil && slow != fast {
        slow = slow.Next
        fast = fast.Next.Next
    }

    return slow == fast
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        if not head or not head.next:
            return False

        slow, fast = head, head.next
        while fast and fast.next and slow != fast:
            slow = slow.next
            fast = fast.next.next

        return slow == fast
```

{{< /tab >}}

{{< /tabs >}}
