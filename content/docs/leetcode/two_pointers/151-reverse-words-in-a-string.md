---
title: 151. 反转字符串中的单词 (Reverse String)
linktitle: 151. 反转字符串中的单词
type: book
date: "2022-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
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
- 空间复杂度：$O(1)$ ，不同语言不同。如 Python 中字符串为不可变类型，复杂度为 $O(n)$。

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
    def reverseWords(self, s: str) -> str:
        s = s.strip() # 删除首尾空格
        i = j = len(s) - 1
        res = []
        while i >= 0:
            while i >= 0 and s[i] != ' ': i -= 1 # 搜索首个空格
            res.append(s[i + 1: j + 1]) # 添加单词
            while s[i] == ' ': i -= 1 # 跳过单词间空格
            j = i # j 指向下个单词的尾字符
        return ' '.join(res) # 拼接并返回

# author: Krahets
# https://leetcode.cn/problems/reverse-words-in-a-string/solutions/195397/151-fan-zhuan-zi-fu-chuan-li-de-dan-ci-shuang-zh-2/
```

{{< /tab >}}

{{< /tabs >}}

## Refer:

- [ACM 解题](https://leetcode.cn/problems/reverse-words-in-a-string/solutions/1167554/acm-xuan-shou-tu-jie-leetcode-fan-zhuan-moi5x/)
