---
title: 541. 反转字符串II (Reverse String II)
linktitle: 541. 反转字符串II
type: book
date: "2022-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

## 描述

给定一个字符串 `s` 和一个整数 `k`，从字符串开头算起，每计数至 `2k` 个字符，就反转这 `2k` 字符中的前 `k` 个字符。

- 如果剩余字符少于 `k` 个，则将剩余字符全部反转。
- 如果剩余字符小于 `2k` 但大于或等于 `k` 个，则反转前 `k` 个字符，其余字符保持原样。

https://leetcode.com/problems/reverse-string-ii/

**Example 1:**

> Input: s = "abcdefg", k = 2

> Output: "bacdfeg"

**Example 2:**

> Input: s = "abcd", k = 2

> Output: "bacd"

## 提示 (Constraints)

- `1 <= s.length <= 10^4`
- `s` 仅由小写英文组成
- `1 <= k <= 104`

## 分析

可以看做是交换 `s[0]`, `s[n-1]`; `s[1]`, `s[n-2]` .... 以此类推，使用 **双指针** 进行，初始化两个指针，一个 `left=0`，一个 `right=n-1`。

> 其中 `n` 字符串长度

## 代码

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

{{< tabs tabTotal="2">}}

{{< tab tabName="Go">}}

```golang
func reverseStr(s string, k int) string {
    ss := []byte(s)
    for i := 0; i < len(s); i += 2*k {
        if i + k < len(s) {
            // 1. 每隔 2k 个字符的前 k 个字符进行反转
            reverse(ss[i:i+k])
        } else {
            // 2. 剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符
            reverse(ss[i:len(s)])
        }
    }
    return string(ss)
}

func reverse(s []byte)  {
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
    def reverseStr(self, s: str, k: int) -> str:
        res, flag = "", True
        for i in range(0, len(s), k):
            res += s[i:i + k][::-1] if flag else s[i:i+k]
            flag = not flag
        return res

# https://leetcode.com/problems/reverse-string-ii/solutions/292728/jian-duan-yi-li-jie-by-powcai/
```

{{< /tab >}}

{{< /tabs >}}
