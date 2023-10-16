---
title: 344. 反转字符串 (Reverse String)
linktitle: 344. 反转字符串
type: book
date: "2022-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## 描述

编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 `s` 的形式给出。

不要给另外的数组分配额外的空间，你必须**原地修改输入数组**、使用 $O(1)$ 的额外空间解决这一问题。

https://leetcode.com/problems/reverse-string/

**Example 1:**

> Input: s = ["h","e","l","l","o"]

> Output: ["o","l","l","e","h"]

**Example 2:**

> Input: s = ["H","a","n","n","a","h"]

> Output: ["h","a","n","n","a","H"]

## 提示 (Constraints)

- `1 <= s.length <= 10^5`
- `s[i]` 都是 `ASCII` 码表中的可打印字符

## 分析

可以看做是交换 `s[0]`, `s[n-1]`; `s[1]`, `s[n-2]` .... 以此类推，使用 **双指针** 进行，初始化两个指针，一个 `left=0`，一个 `right=n-1`。

> 其中 `n` 字符串长度

## 代码

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

{{< tabs tabTotal="2">}}

{{< tab tabName="Go">}}

```golang
func reverseString(s []byte)  {
    for i, j := 0, len(s)-1; i < j; {
        s[i], s[j] = s[j], s[i]
        i++
        j--
    }
}
```

{{< /tab >}}

{{< tab tabName="Python">}}

```py
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        n = len(s)
        for i in range(n // 2):
            s[i], s[n - i - 1] = s[n - i - 1], s[i]
```

{{< /tab >}}

{{< /tabs >}}
