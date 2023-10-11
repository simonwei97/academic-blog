---
title: 503. 下一个更大元素 II (Next Greater Element II)
linktitle: 503. 下一个更大元素 II
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
---

## 描述

给定一个循环数组 `nums` （ `nums[nums.length - 1]` 的下一个元素是 `nums[0]` ），返回 `nums` 中每个元素的 **下一个更大元素** 。

数字 `x` 的 **下一个更大的元素** 是按数组遍历顺序，这个数字之后的第一个比它更大的数，这意味着你应该循环地搜索它的下一个更大的数。如果不存在，则输出 `-1` 。

**Example 1:**

> Input: nums = [1,2,1]

> Output: [2,-1,2]

**Example 2:**

> Input: nums = [1,2,3,4,3]

> Output: [2,3,4,-1,4]

## 提示 (Constraints)

- `1 <= nums.length <= 10^4`
- `-10^9 <= nums[i] <= 10^9`

## 分析

假设定义参数如下

- 当前遍历元素 `T[i]`
- 栈顶元素 `T[st.top()]`

使用单调栈的三种情况（保持单调递增栈）:

1. `T[i] < T[st.top()]`：直接放入栈中，
2. `T[i] = T[st.top()]`：直接放入栈中（同上）
3. `T[i] > T[st.top()]`：将栈顶元素弹出 `T[st.top()]`，加入当前遍历元素 `T[i]`。这里需要循环判断，即弹出后再次比对当前元素和栈顶元素。

## 代码

{{< tabs tabTotal="2">}}

{{< tab tabName="Go">}}

```golang
func nextGreaterElements(nums []int) []int {
    res := make([]int, len(nums))
    for i := range res {
        res[i] = -1
    }
    if len(nums) == 0 {
        return res
    }
    stack := []int{}
    for i := 0; i < len(nums)*2; i++ {
        for len(stack) > 0 && nums[i % len(nums)] > nums[stack[len(stack)-1]] {
            index := stack[len(stack)-1]
            res[index] = nums[i % len(nums)]
            stack = stack[:len(stack)-1]       // pop
        }
        stack = append(stack, i % len(nums))
    }
    return res
}
```

{{< /tab >}}

{{< tab tabName="Python">}}

```py
class Solution:
    def nextGreaterElements(self, nums: List[int]) -> List[int]:
        n = len(nums)
        ret = [-1] * n
        stk = list()

        for i in range(n * 2 - 1):
            while stk and nums[stk[-1]] < nums[i % n]:
                ret[stk.pop()] = nums[i % n]
            stk.append(i % n)

        return ret
```

{{< /tab >}}

{{< /tabs >}}
