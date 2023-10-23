---
title: 5. 最长回文子串 (Longest Palindrome)
linktitle: 5. 最长回文子串
type: book
date: "2022-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
---

## 描述

给你一个字符串 `s`，找到 `s` 中最长的回文子串。

如果字符串的反序与原始字符串相同，则该字符串称为回文字符串。

https://leetcode.com/problems/longest-palindromic-substring/

**Example 1:**

> Input: s = "babad"

> Output: "bab"

**Example 2:**

> Input: s = "cbbd"

> Output: "bb"

## 提示 (Constraints)

- `1 <= s.length <= 1000`
- `s` 仅由数字和英文字母组成

## 分析

## 代码

### 中心扩散法

遍历每一个下标，以这个下标为中心，利用 **回文串** 的中心对称的特性，从中心向两边扩散查找，看最多能扩散到什么位置。

- 时间复杂度：$O(n)$ 。其中 $n$ 是字符串的长度。长度为 $1$ 和 $2$ 的回文中心分别有 $n-1$ 和 $n-2$ 个，每个回文中心最多会向外扩展 $O(n)$ 次。
- 空间复杂度：$O(1)$ 。

{{< tabs tabTotal="2">}}

{{< tab tabName="Go">}}

```golang
func longestPalindrome(s string) string {
    res := ""
    for i := 0; i < len(s); i++ {
        res = maxPalindrome(s, i, i, res)     // odd
        res = maxPalindrome(s, i, i + 1, res) // even
    }
    return res
}

func maxPalindrome(s string, i, j int, res string) string {
    sub := ""
    for i >= 0 && j < len(s) && s[i] == s[j] {
        sub = s[i:j+1]
        i--
        j++
    }
    if len(res) < len(sub) {
        return sub
    }
    return res
}
```

{{< /tab >}}

{{< tab tabName="Python">}}

```py

```

{{< /tab >}}

{{< /tabs >}}

### Manacher's algorithm

Refer: https://books.halfrost.com/leetcode/ChapterFour/0001~0099/0005.Longest-Palindromic-Substring/

- 时间复杂度：$O(n)$ 。
- 空间复杂度：$O(n)$ 。

{{< tabs tabTotal="2">}}

{{< tab tabName="Go">}}

```golang
func longestPalindrome(s string) string {
    if len(s) < 2 {
        return s
    }

    newS := make([]rune, 0)
    newS = append(newS, '#')
    for _, c := range s {
        newS = append(newS, c)
        newS = append(newS, '#')
    }

    // dp[i]:    以预处理字符串下标 i 为中心的回文半径(奇数长度时不包括中心)
	// maxRight: 通过中心扩散的方式能够扩散的最右边的下标
	// center:   与 maxRight 对应的中心字符的下标
	// maxLen:   记录最长回文串的半径
	// begin:    记录最长回文串在起始串 s 中的起始下标
    dp := make([]int, len(newS))
    maxRight, center, maxLen, begin := 0, 0, 1, 0
    for i := 0; i < len(newS); i++ {
        if i < maxRight {
            dp[i] = min(maxRight - i, dp[2 * center - i])
        }

        // 中心扩散
        left, right := i - (1 + dp[i]), i + (1 + dp[i])
        for left >= 0 && right < len(newS) && newS[left] == newS[right] {
            dp[i]++
            left--
            right++
        }

        // 更新maxRight
        if i + dp[i] < maxRight {
            maxRight = i + dp[i]
            center = i
        }

        // 记录最长回文串的起始点
        if dp[i] > maxLen {
            maxLen = dp[i]
            begin = (i - maxLen) / 2
        }
    }
    return s[begin:begin+maxLen]
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
```

{{< /tab >}}

{{< tab tabName="Python">}}

```py

```

{{< /tab >}}

{{< /tabs >}}
