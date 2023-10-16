---
title: 209. 长度最小的子数组 (Minimum Size Subarray Sum)
linktitle: 209. 长度最小的子数组
type: book
date: "2019-05-09T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 4
---

## 描述 (Description)

给定一个含有 `n` 个正整数的数组和一个正整数 `target` 。

找出该数组中满足其总和大于等于 `target` 的长度最小的 连续子数组 `[numsl, numsl+1, ..., numsr-1, numsr]` ，并返回其长度。如果不存在符合条件的子数组，返回 `0` 。

https://leetcode.com/problems/minimum-size-subarray-sum/

**Example 1:**

> Input: target = 7, nums = [2,3,1,2,4,3]

> Output: 2

**Example 2:**

> Input: target = 4, nums = [1,4,4]

> Output: 1

**Example 3:**

> Input: target = 11, nums = [1,1,1,1,1,1,1,1]

> Output: 0

## 提示 (Constraints)

- `1 <= target <= 10^9`
- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^5`

## 分析 (Analysis)

**滑动窗口**，动态调整窗口的大小，窗口内就是子序列的长度。

## 代码 (Code)

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
func minSubArrayLen(target int, nums []int) int {
    i := 0
    l := len(nums)
    res := l+1
    sum := 0
    for j := 0; j < l; j++ {
        sum += nums[j]
        for sum >= target {
            subL := j - i + 1
            if subL < res {
                res = subL
            }
            sum -= nums[i]
            i++
        }
    }

    if res == l + 1 {
        return 0
    }
    return res
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```python
class Solution:
    def minSubArrayLen(self, s: int, nums: List[int]) -> int:
        l = len(nums)
        left = 0
        right = 0
        min_len = l+1
        cur_sum = 0 #当前的累加值

        while right < l:
            cur_sum += nums[right]
            while cur_sum >= s:
                min_len = min(min_len, right - left + 1)
                cur_sum -= nums[left]
                left += 1

            right += 1

        return 0 if min_len == l+1 else min_len
```

{{< /tab >}}

{{< /tabs >}}
