---
title: 242.有效的字母异位词 (Valid Anagram)
linktitle: 242.有效的字母异位词
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

## 描述 (Description)

给定两个字符串 `s` 和 `t` ，编写一个函数来判断 `t` 是否是 `s` 的字母异位词。

注意：若 `s` 和 `t` 中每个字符出现的次数都相同，则称 `s` 和 `t` 互为字母异位词。

https://leetcode.com/problems/valid-anagram/

**Example 1:**

> Input: s = "anagram", t = "nagaram"

> Output: true

**Example 2:**

> Input: s = "rat", t = "car"

> Output: false

## 提示 (Constraints)

- `1 <= s.length, t.length <= 5 * 10^4`
- `s` 和 `t` 仅包含小写字母

## 分析 (Analysis)

使用哈希表记录字符串 `s` 中字符出现的频次，然后再遍历字符串 `t`，减去哈希表中对应的频次，最后判断哈希表中是否有元素不为 `0`。为 `0` 才表示为异位词。

## 代码 (Code)

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
func isAnagram(s string, t string) bool {
    record := [26]int{}
    for _, v := range t {
        record[v-rune('a')]++
    }

    for _, v := range s {
        record[v-rune('a')]--
    }

    return record == [26]int{}
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        record = [0] * 26
        for i in s:
            record[ord(i) - ord('a')] += 1

        for j in t:
            record[ord(j) - ord('a')] -= 1

        for i in range(26):
            if record[i] != 0:
                return False
        return True
```

{{< /tab >}}

{{< /tabs >}}
