---
title: 27. 移除元素 (Remove Element)
linktitle: 27. 移除元素
type: book
date: "2019-05-09T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

## 描述 (Description)

给你一个数组 `nums` 和一个值 `val`，你需要 **原地** 移除所有数值等于 `val` 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 $O(1)$ 额外空间并 **原地** 修改输入数组。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

https://leetcode.com/problems/remove-element/

**Example 1:**

> Input: nums = [3,2,2,3], val = 3

> Output: 2, nums = [2,2]

**Example 2:**

> Input: nums = [0,1,2,2,3,0,4,2], val = 2

> Output: 5, nums = [0,1,4,0,3]

## 提示 (Constraints)

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`

## 分析 (Analysis)

使用双指针方法，定义快慢指针

- 快指针：原数组的下标指引，持续遍历
- 慢指针：最终新数组的位置，只有满足条件，才+1

## 代码 (Code)

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
func removeElement(nums []int, val int) int {
    i := 0
    for _, v := range nums {
        if v == val {
            continue
        }
        nums[i] = v
        i++
    }
    nums = nums[:i]
    return i
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i = 0
        for j in range(len(nums)):
            if nums[j] != val:
                nums[i] = nums[j]
                i+=1
        nums = nums[:i]
        return i
```

{{< /tab >}}

{{< /tabs >}}
