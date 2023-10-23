---
title: 28. 找出字符串中第一个匹配项的下标 (strStr())
linktitle: 28. 找出字符串中第一个匹配项的下标
type: book
date: "2022-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
---

## 描述

给你两个字符串 `haystack` 和 `needle` ，请你在 `haystack` 字符串中找出 `needle` 字符串的第一个匹配项的下标（下标从 `0` 开始）。如果 `needle` 不是 `haystack` 的一部分，则返回 `-1` 。

https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/

**Example 1:**

> Input: haystack = "sadbutsad", needle = "sad"

> Output: 0

**Example 2:**

> Input: haystack = "leetcode", needle = "leeto"

> Output: -1

## 提示 (Constraints)

- `1 <= haystack.length, needle.length <= 10^4`
- `haystack` 和 `needle` 仅由小写英文字符组成

## 分析

## 代码

### 暴力解法

Refer: https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/solutions/575568/shua-chuan-lc-shuang-bai-po-su-jie-fa-km-tb86/

- 时间复杂度：$O((n−m)∗m)$。`n` 为原串的长度，`m` 为匹配串的长度。其中枚举的复杂度为 $O(n−m)$，构造和比较字符串的复杂度为 $O(m)$。整体复杂度为 $O((n−m)∗m)$。
- 空间复杂度：$O(1)$。

{{< tabs tabTotal="2">}}

{{< tab tabName="Go">}}

```golang
func strStr(haystack string, needle string) int {
    nn := len(haystack)
    mm := len(needle)

    for i := 0; i <= nn - mm; i++ {
        a := i
        b := 0
        for b < mm && haystack[a] == needle[b] {
            a++
            b++
        }
        if b == mm {
            return i
        }
    }
    return -1
}
```

{{< /tab >}}

{{< tab tabName="Python">}}

```py
# TODO
```

{{< /tab >}}

{{< /tabs >}}

### KMP 解法

Refer: https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/solutions/732461/dai-ma-sui-xiang-lu-kmpsuan-fa-xiang-jie-mfbs/

{{< tabs tabTotal="2">}}

{{< tab tabName="Go">}}

```golang
func strStr(haystack string, needle string) int {
    if len(needle) == 0 {
        return 0
    }
    next := make([]int, len(needle))
    getNext(next, needle)
    j := -1 // 模式串的起始位置 next为-1 因此也为-1
    for i := 0; i < len(haystack); i++ {
        for j >= 0 && haystack[i] != needle[j+1] {
             = next[j] // 寻找下一个匹配点
        }
        if haystack[i] == needle[j+1] {
            j++
        }
        if j == len(needle)-1 { // j指向了模式串的末尾
            return i - len(needle) + 1
        }
    }
    return -1
}

func getNext(next []int, s string) {
    j := -1 // j表示 最长相等前后缀长度
    next[0] = j

    for i := 1; i < len(s); i++ {
        for j >= 0 && s[i] != s[j+1] {
            j = next[j] // 回退前一位
        }
        if s[i] == s[j+1] {
            j++
        }
        next[i] = j // next[i]是i（包括i）之前的最长相等前后缀长度
    }
}
```

{{< /tab >}}

{{< tab tabName="Python">}}

```py
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if not needle:
            return 0
        next = [0] * len(needle)
        self.getNext(next, needle)
        j = -1
        for i in range(len(haystack)):
            while j >= 0 and haystack[i] != needle[j+1]:
                j = next[j]
            if haystack[i] == needle[j+1]:
                j += 1
            if j == len(needle) - 1:
                return i - len(needle) + 1
        return -1

    def getNext(self, next, s):
        j = -1
        next[0] = j
        for i in range(1, len(s)):
            while j >= 0 and s[i] != s[j+1]:
                j = next[j]
            if s[i] == s[j+1]:
                j += 1
            next[i] = j
```

{{< /tab >}}

{{< /tabs >}}
