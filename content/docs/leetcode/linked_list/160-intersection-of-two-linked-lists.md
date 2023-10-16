---
title: 160. 相交链表 (Intersection of Two Linked Lists)
linktitle: 160. 相交链表
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 6
---

## 描述 (Description)

给你两个单链表的头节点 `headA` 和 `headB` ，请你找出并返回两个单链表相交的起始节点。如果两个链表不存在相交节点，返回 `null` 。

图示两个链表在节点 `c1` 开始相交：

https://leetcode.com/problems/intersection-of-two-linked-lists/

**Example 1:**

> Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3

> Output: Intersected at '8'

**Example 2:**

> Input: intersectVal = 2, listA = [1,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1

> Output: Intersected at '2'

**Example 3:**

> Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2

> Output: null

## 提示 (Constraints)

- `listA` 中节点数目为 `m`
- `listB` 中节点数目为 `n`
- `1 <= m, n <= 3 * 104`
- `1 <= Node.val <= 105`
- `0 <= skipA <= m`
- `0 <= skipB <= n`
- 如果 `listA` 和 `listB` 没有交点，`intersectVal` 为 `0`
- 如果 `listA` 和 `listB` 有交点，`intersectVal == listA[skipA] == listB[skipB]`

## 分析 (Analysis)

利用 **双指针** 实现。

- 如果链表相交，则会在中途出现相等的情况，此时进行返回。
- 如果链表不想交，中途不会出现相等，最后一直走到链表尾部，得到 `nil`。

## 代码 (Code)

- 时间复杂度：
  - `O(m+n)`：`m` 和 `n` 分别代表链表 `headA` 和 `headB` 的长度。
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
func getIntersectionNode(headA, headB *ListNode) *ListNode {
    if headA == nil || headB == nil {
        return nil
    }
    la, lb := headA, headB
    for la != lb {
        if la != nil {
            la = la.Next
        } else {
            la = headB
        }

        if lb != nil {
            lb = lb.Next
        } else {
            lb = headA
        }
    }
    return la
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
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        if not headA or not headB:
            return None
        la, lb = headA, headB
        while la != lb:
            la = la.next if la else headB
            lb = lb.next if lb else headA

        return la
```

{{< /tab >}}

{{< /tabs >}}
