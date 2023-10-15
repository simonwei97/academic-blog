---
title: 977. 有序数组的平方 (Squares of a Sorted Array)
linktitle: 977. 有序数组的平方
type: book
date: "2019-05-09T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
---

## 描述 (Description)

给你一个按 **非递减顺序** 排序的整数数组` nums`，返回 **每个数字的平方** 组成的新数组，要求也按 **非递减顺序** 排序。

- https://leetcode.cn/problems/squares-of-a-sorted-array/
- https://leetcode.com/problems/squares-of-a-sorted-array/

**Example 1:**

> Input: nums = [-4,-1,0,3,10]

> Output: [0,1,9,16,100]

**Example 2:**

> Input: nums = [-7,-3,2,3,11]

> Output: [4,9,9,49,121]

## 提示 (Constraints)

- `1 <= nums.length <= 10^4`
- `-10^4 <= nums[i] <= 10^4`
- `nums` 已按 **非递减顺序** 排序

## 分析 (Analysis)

使用双指针方法，定义快慢指针

- 快指针：原数组的下标指引，持续遍历
- 慢指针：最终新数组的位置，只有满足条件，才+1

## 代码 (Code)

- 时间复杂度：`O(n)`
- 空间复杂度：`O(1)`

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
func sortedSquares(nums []int) []int {
    n := len(nums)
    i, j, k := 0, n-1, n-1
    res := make([]int, n)
    for i <= j {
        lm, rm := nums[i]*nums[i], nums[j]*nums[j]
        if lm > rm {
            res[k] = lm
            i++
        } else {
            res[k] = rm
            j--
        }
        k--
    }
    return res
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        n = len(nums)
        i, j, k = 0, n-1, n-1
        res = [-1] * len(nums)
        while i <= j:
            lm, rm = nums[i]*nums[i], nums[j]*nums[j]
            if lm > rm:
                res[k] = lm
                i += 1
            else:
                res[k] = rm
                j -= 1
            k -= 1
        return res
```

{{< /tab >}}

{{< /tabs >}}
