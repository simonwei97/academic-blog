---
title: 151. 反转字符串中的单词 (Reverse String)
linktitle: 151. 反转字符串中的单词
type: book
date: "2022-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## 描述

给你一个字符串 `s` ，请你反转字符串中 **单词** 的顺序。

**单词** 是由非空格字符组成的字符串。`s` 中使用至少一个空格将字符串中的 **单词** 分隔开。

返回 **单词** 顺序颠倒且 **单词** 之间用单个空格连接的结果字符串。

注意：输入字符串 `s` 中可能会存在前导空格、尾随空格或者单词间的多个空格。返回的结果字符串中，单词间应当仅用单个空格分隔，且不包含任何额外的空格。

https://leetcode.com/problems/reverse-words-in-a-string/

**Example 1:**

> Input: s = "the sky is blue"

> Output: "blue is sky the"

**Example 2:**

> Input: s = " hello world "

> Output: "world hello"

**Example 3:**

> Input: s = "a good example"

> Output: "example good a"

## 提示 (Constraints)

- `1 <= s.length <= 10^4`
- `s` 包含英文大小写字母、数字和空格 `' '`
- `s` 中 **至少存在一个** 单词

## 分析

## 代码

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

{{< tabs tabTotal="2">}}

{{< tab tabName="Go">}}

```golang
func reverseWords(s string) string {
    slow, fast := 0, 0
    b := []byte(s)

    // 删除前导空格
    for len(b) > 0 && fast < len(b) && b[fast] == ' ' {
        fast++
    }

    for ; fast < len(b); fast++ {
        if fast-1 > 0 && b[fast-1] == b[fast] && b[fast] == ' ' {
            continue
        }
        b[slow] = b[fast]
        slow++
    }

    // 删除尾部空格
    if slow - 1 > 0 && b[slow-1] == ' ' {
        b = b[:slow-1]
    } else {
        b = b[:slow]
    }

    // 翻转整个字符串
    reverse(&b, 0, len(b)-1)
    i := 0
    for i < len(b) {
        j := i
        for ; j < len(b) && b[j] != ' '; j++ {
        }
        reverse(&b, i, j-1)
        i = j
        i++
    }
    return string(b)
}

func reverse(b *[]byte, left, right int) {
    for left < right {
        (*b)[left], (*b)[right] = (*b)[right], (*b)[left]
        left++
        right--
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
