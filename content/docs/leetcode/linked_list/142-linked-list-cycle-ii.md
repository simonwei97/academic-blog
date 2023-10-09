---
title: 142. 环形链表 II (Linked List Cycle II)
linktitle: 142. 环形链表 II
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 8
---

## 描述 (Description)

给定一个链表的头节点 `head` ，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

如果链表中有某个节点，可以通过连续跟踪 `next` 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 `0` 开始）。如果 `pos` 是 `-1`，则在该链表中没有环。注意：`pos` 不作为参数进行传递，仅仅是为了标识链表的实际情况。

**不允许修改** 链表。

https://leetcode.cn/problems/linked-list-cycle-ii/

**Example 1:**

> Input: head = [3,2,0,-4], pos = 1

> Output: 返回索引为 1 的链表节点

**Example 2:**

> Input: head = [1,2], pos = 0

> Output: 返回索引为 0 的链表节点

**Example 3:**

> Input: head = [1], pos = -1

> Output: null

## 提示 (Constraints)

- 链表中节点的数目范围在范围 `[0, 104]` 内
- `-10^5 <= Node.val <= 10^5`
- `pos` 的值为 `-1` 或者链表中的一个有效索引

## 分析 (Analysis)

可参考 [代码随想录 - 142.环形链表 II #思路](https://programmercarl.com/0142.%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8II.html#%E6%80%9D%E8%B7%AF)

利用 **快慢指针** 实现。

## 代码 (Code)

- 时间复杂度：
  - `O(n)`：`n` 代表链表 `head` 的长度。
- 空间复杂度：
  - `O(1)`：未使用额外空间存储

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
func detectCycle(head *ListNode) *ListNode {
    slow, fast := head, head
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
        if slow == fast {
            ptr := head
            for slow != ptr {
                slow = slow.Next
                ptr = ptr.Next
            }
            return ptr
        }
    }
    return nil
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
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                ptr = head
                while slow != ptr:
                    ptr = ptr.next
                    slow = slow.next
                return ptr

        return None
```

{{< /tab >}}

{{< /tabs >}}
