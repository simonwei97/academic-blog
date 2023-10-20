---
title: 76. 最小覆盖子串 (minimum-window-substring)
linktitle: 76. 最小覆盖子串
type: book
date: "2019-05-09T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 7
---

## 描述 (Description)

给你一个字符串 `s` 、一个字符串 `t` 。返回 `s` 中涵盖 `t` 所有字符的最小子串。如果 `s` 中不存在涵盖 `t` 所有字符的子串，则返回空字符串 `""` 。

注意：

- 对于 `t` 中重复字符，我们寻找的子字符串中该字符数量必须不少于 `t` 中该字符数量。
- 如果 `s` 中存在这样的子串，我们保证它是唯一的答案。

https://leetcode.com/problems/minimum-window-substring/

**Example 1:**

> Input: s = "ADOBECODEBANC", t = "ABC"

> Output: "BANC"

**Example 2:**

> Input: s = "a", t = "a"

> Output: "a"

**Example 3:**

> Input: s = "a", t = "aa"

> Output: ""

## 提示 (Constraints)

- `m == s.length`
- `n == t.length`
- `1 <= m, n <= 105`
- `s` 和 `t` 由英文字母组成

## 分析 (Analysis)

滑动窗口

- 先遍历 `t`， 记录元素到哈希表 `need` 中；记录需要遍历的个数 `len(t)` 到 `neecCnt`。
- 初始化长度为 2 的 `ret` 数组`[0, Inf]`，作为记录目标子字符串的左右索引下标。
- 遍历字符串 `s`， 如果遍历到的元素刚好 `>0`, 说明是 t 中元素，`needCnt` 减一。将遍历到的元素 `-1` 记录到哈希表 `need` 中。
- 如果 `needCnt == 0` 说明此时左右下标范围内 `[lo,hi]` 有符合要求子字符串, 开始缩小滑动窗口。
- 左索引下标 `lo` 向前推进, 当 `need[s[lo]] == 0` 时，说明遍历到 `t` 中元素（并且因为此时 `needCntCnt==0`）， `s[lo,hi]` 为结果之一，判断是否最小。

## 代码 (Code)

- 时间复杂度：$O(n)$
- 空间复杂度：$O(k)$，`k` 为 `s` 和 `t` 中的字符集合。

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
func minWindow(s string, t string) string {
    need := make(map[byte]int)
    for i := range t {
        need[t[i]]++
    }

    needCnt := len(t)
    res := []int{0, math.MaxInt32}

    var lo int
    for hi := range s {
        if need[s[hi]] > 0 {
            needCnt--
        }
        need[s[hi]]--

        if needCnt == 0 {
            for {
                if need[s[lo]] == 0 {
                    break
                }
                need[s[lo]]++
                lo++
            }

            if hi - lo < res[1] - res[0] {
                res = []int{lo, hi}
            }
            need[s[lo]]++
            needCnt++
            lo++
        }
    }

    if res[1] > len(s) {
        return ""
    }
    return s[res[0]: res[1]+1]
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```python
class Solution:
        def minWindow(self, s: str, t: str) -> str:
        need=collections.defaultdict(int)
        for c in t:
            need[c]+=1
        needCnt=len(t)
        i=0
        res=(0,float('inf'))
        for j,c in enumerate(s):
            if need[c]>0:
                needCnt-=1
            need[c]-=1
            if needCnt==0:       #步骤一：滑动窗口包含了所有T元素
                while True:      #步骤二：增加i，排除多余元素
                    c=s[i]
                    if need[c]==0:
                        break
                    need[c]+=1
                    i+=1
                if j-i<res[1]-res[0]:   #记录结果
                    res=(i,j)
                need[s[i]]+=1  #步骤三：i增加一个位置，寻找新的满足条件滑动窗口
                needCnt+=1
                i+=1
        return '' if res[1]>len(s) else s[res[0]:res[1]+1]    #如果res始终没被更新过，代表无满足条件的结果

# 作者：Mcdull
# 链接：https://leetcode.cn/problems/minimum-window-substring/solutions/258513/tong-su-qie-xiang-xi-de-miao-shu-hua-dong-chuang-k/
```

{{< /tab >}}

{{< /tabs >}}
