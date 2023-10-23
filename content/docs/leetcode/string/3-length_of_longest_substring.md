---
title: 3. 无重复字符的最长子串 (Length Of Longest Substring)
linktitle: 3. 无重复字符的最长子串
type: book
date: "2022-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 4
---

## 描述

给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。

https://leetcode.com/problems/longest-substring-without-repeating-characters/

**Example 1:**

> Input: s = "abcabcbb"

> Output: 3

**Example 2:**

> Input: s = "bbbbb"

> Output: 1

**Example 3:**

> Input: s = "pwwkew"

> Output: 3

## 提示 (Constraints)

- `0 <= s.length <= 5 * 10^4`
- `s` 由英文字母、数字、符号和空格组成

## 分析

滑动窗口

## 代码

- 时间复杂度：$O(n)$ 。其中 $n$ 是字符串的长度。长度为 $1$ 和 $2$ 的回文中心分别有 $n-1$ 和 $n-2$ 个，每个回文中心最多会向外扩展 $O(n)$ 次。
- 空间复杂度：$O(|\Sigma|)$ 。其中 $\Sigma$ 表示字符集。

{{< tabs tabTotal="2">}}

{{< tab tabName="Go">}}

```golang
func lengthOfLongestSubstring(s string) int {
    window := make(map[byte]int)
    res := 0
    for i, j := 0, 0; i < len(s); i++ {
        window[s[i]]++
        for window[s[i]] > 1 {
            window[s[j]]--
            j++
        }
        res = max(res, i - j + 1)
    }
    return res
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```

{{< /tab >}}

{{< tab tabName="Python">}}

```py
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        occur = set()
        n = len(s)
        # rk表示还没有开始移动，位于字符串的左侧。
        rk, ans = -1, 0
        for i in range(n):
            if i != 0:
                # 左指针向右移动一格，移除一个字符
                occur.remove(s[i-1])
            while rk + 1 < n and s[rk + 1] not in occur:
                 # 不断地移动右指针
                occur.add(s[rk + 1])
                rk += 1
            ans = max(ans, rk - i + 1)

        return ans
```

{{< /tab >}}

{{< /tabs >}}
