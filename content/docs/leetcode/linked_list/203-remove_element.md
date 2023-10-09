---
title: 203. 移除链表元素 (Remove Linked List Elements)
linktitle: 203. 移除链表元素
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## 描述 (Description)

给你一个链表的头节点 `head` 和一个整数 `val` ，请你删除链表中所有满足 `Node.val == val` 的节点，并返回 **新的头节点** 。

https://leetcode.cn/problems/remove-linked-list-elements/

**Example 1:**

![](/docs/leetcode/removelinked-list.jpeg)

> Input: head = [1,2,6,3,4,5,6], val = 6

> Output: [1,2,3,4,5]

**Example 2:**

> Input: head = [], val = 1

> Output: []

**Example 3:**

> Input: head = [7,7,7,7], val = 7

> Output: []

## 提示 (Constraints)

- 列表中的节点数目在范围 `[0, 104]` 内
- `1 <= Node.val <= 50`
- `0 <= val <= 50`

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

func removeElements(head *ListNode, val int) *ListNode {
    if head == nil {
        return head
    }
    dummy := &ListNode{Val: 0}
    dummy.Next = head
    cur := dummy
    for cur.Next != nil {
        if cur.Next.Val == val {
            cur.Next = cur.Next.Next
        } else {
            cur = cur.Next
        }
    }
    return dummy.Next
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```py
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        dummy_head = ListNode(next = head)
        current = dummy_head
        while current.next:
            if current.next.val == val:
                current.next = current.next.next
            else:
                current = current.next

        return dummy_head.next
```

{{< /tab >}}
{{< tab tabName="C++">}}

```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* dummy = new ListNode(0);
        dummy->next = head;
        ListNode* cur = dummy;
        while (cur->next != NULL) {
            if(cur->next->val == val) {
                ListNode* tmp = cur->next;
                cur->next = cur->next->next;
                delete tmp;
            } else {
                cur = cur->next;
            }
        }
        head = dummy->next;
        delete dummy;
        return head;
    }
};
```

{{< /tab >}}
{{< /tabs >}}
