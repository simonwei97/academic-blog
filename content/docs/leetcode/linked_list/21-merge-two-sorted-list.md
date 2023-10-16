---
title: 21. 合并两个有序链表 (Merge Two Sorted List)
linktitle: 21. 合并两个有序链表
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 10
---

## 描述 (Description)

将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

https://leetcode.com/problems/merge-two-sorted-lists/

**Example 1:**

> Input: l1 = [1,2,4], l2 = [1,3,4]

> Output: [1,1,2,3,4,4]

**Example 2:**

> Input: l1 = [], l2 = []

> Output: []

**Example 3:**

> Input: l1 = [], l2 = [0]

> Output: [0]

## 提示 (Constraints)

- 两个链表的节点数目范围是 `[0, 50]`
- `-100 <= Node.val <= 100`
- `l1` 和 `l2` 均按 **非递减顺序** 排列

## 分析 (Analysis)

迭代：依次比较 `l1` 和 `l2` 两个链表，那个链表的头结点小，将其加入结果中，依次往后移。

## 代码 (Code)

- 时间复杂度：
  - `O(m+n)`：`m` 和 `n` 分别代表两个链表的长度。
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
func mergeTwoLists(list1 *ListNode, list2 *ListNode) *ListNode {
    prehead := &ListNode{Val: -1}

    prev := prehead
    for list1 != nil && list2 != nil {
        if list1.Val <= list2.Val {
            prev.Next = list1
            list1 = list1.Next
        } else {
            prev.Next = list2
            list2 = list2.Next
        }
        prev = prev.Next
    }

    if list1 != nil {
        prev.Next = list1
    } else {
        prev.Next = list2
    }

    return prehead.Next
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```py
TODO
```

{{< /tab >}}

{{< /tabs >}}
