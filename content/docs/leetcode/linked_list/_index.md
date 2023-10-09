---
# Title, summary, and page position.
linktitle: 链表
summary: 链表
weight: 2
icon: book
icon_pack: fas

# Page metadata.
title: 链表
date: "2022-09-09T00:00:00Z"
type: book # Do not modify.
---

# 单链表结构体定义

{{< tabs tabTotal="3">}}

{{< tab tabName="Go">}}

```golang
type ListNode struct {
    Val int
    Next *ListNode
}
```

{{< /tab >}}
{{< tab tabName="Python">}}

```python
class ListNode:
    def __init__(self, val, next=None):
        self.val = val
        self.next = next
```

{{< /tab >}}
{{< tab tabName="C++">}}

```cpp
struct ListNode {
    int val;  // 节点上存储的元素
    ListNode *next;  // 指向下一个节点的指针
    ListNode(int x) : val(x), next(NULL) {}  // 节点的构造函数
};
```

{{< /tab >}}

{{< /tabs >}}
