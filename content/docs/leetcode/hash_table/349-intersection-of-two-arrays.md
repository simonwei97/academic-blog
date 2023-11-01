---
title: 349. 两个数组的交集 (Intersection Of Two Arrays)
linktitle: 349. 两个数组的交集
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
---

## 描述 (Description)

给定两个数组 `nums1` 和 `nums2` ，返回*它们的交集*。输出结果中的每个元素一定是**唯一**的。我们可以 **不考虑输出结果的顺序** 。

https://leetcode.cn/problems/intersection-of-two-arrays/

**Example 1:**

> Input: nums1 = [1,2,2,1], nums2 = [2,2]

> Output: [2]

**Example 2:**

> Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]

> Output: [9,4]

## 提示 (Constraints)

- `1 <= nums1.length, nums2.length <= 1000`
- `0 <= nums1[i], nums2[i] <= 1000`

## 分析 (Analysis)

使用哈希表记录字符串 `s` 中字符出现的频次，然后再遍历字符串 `t`，如果字符出现在字符串 `t` 中则添加至结果数组。

## 代码 (Code)

`m` 和 `n` 分别代表两个数组的长度。

- 时间复杂度：$O(m+n)$,
- 空间复杂度：$O(max(m+n))$

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
func intersection(nums1 []int, nums2 []int) []int {
    m := make(map[int]int)
    for _, v := range nums1 {
        m[v] = 1
    }

    var res []int
    for _, v := range nums2 {
        if cnt, ok := m[v]; ok && cnt > 0 {
            res = append(res, v)
            m[v]--
        }
    }
    return res
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        htable = {}
        for num in nums1:
            htable[num] = htable.get(num, 0) + 1

        res = []
        for num in nums2:
            if htable.get(num):
                res.append(num)
                htable[num] = 0

        return res

    # 使用set()
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        table = {}
        for num in nums1:
            table[num] = table.get(num, 0) + 1

        # 使用集合存储结果
        res = set()
        for num in nums2:
            if num in table:
                res.add(num)
                del table[num]

        return list(res)
```

{{< /tab >}}

{{< /tabs >}}
