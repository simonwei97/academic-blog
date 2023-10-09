---
title: 496. 下一个更大元素 I (Next Greater Element I)
linktitle: 496. 下一个更大元素 I
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## 描述

`nums1` 中数字 `x` 的 **下一个更大元素** 是指 `x` 在 `nums2` 中对应位置 **右侧** 的 **第一个** 比 `x` 大的元素。

给你两个 **没有重复元素** 的数组 `nums1` 和 `nums2` ，下标从 `0` 开始计数，其中 `nums1` 是 `nums2` 的子集。

对于每个 `0 <= i < nums1.length` ，找出满足 `nums1[i] == nums2[j]` 的下标 `j` ，并且在 `nums2` 确定 `nums2[j]` 的 **下一个更大元素** 。如果不存在下一个更大元素，那么本次查询的答案是 `-1` 。

返回一个长度为 `nums1.length` 的数组 `ans` 作为答案，满足 `ans[i]` 是如上所述的 **下一个更大元素** 。

**Example 1:**

> Input: nums1 = [4,1,2], nums2 = [1,3,4,2].

> Output: [-1,3,-1]

**Example 2:**

> Input: nums1 = [2,4], nums2 = [1,2,3,4].

> Output: [3,-1]

## 提示 (Constraints)

- `1 <= nums1.length <= nums2.length <= 1000`
- `0 <= nums1[i], nums2[i] <= 10^4`
- `nums1` 和 `nums2` 中所有整数 互不相同
- `nums1` 中的所有整数同样出现在 `nums2` 中

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
func nextGreaterElement(nums1 []int, nums2 []int) []int {
    res := make([]int, len(nums1))
    for i := range res {
        res[i] = -1
    }

    mapR := make(map[int]int, 0)
    for i, v := range nums1 {
        mapR[v] = i
    }

    stack := []int{0}

    for i := 1; i < len(nums2); i++ {
        for len(stack) > 0 && nums2[i] > nums2[stack[len(stack)-1]] {
            top := stack[len(stack)-1]         // top index
            if v, ok := mapR[nums2[top]]; ok { // check if exist
                res[v] = nums2[i]
            }
            stack = stack[:len(stack)-1]
        }
        stack = append(stack, i)
    }
    return res
}
```

{{< /tab >}}

{{< tab tabName="Python">}}

```py
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        result = [-1]*len(nums1)
        stack = [0]
        for i in range(1, len(nums2)):
            # 情况一和情况二
            if nums2[i] <= nums2[stack[-1]]:
                stack.append(i)
            # 情况三
            else:
                while len(stack) != 0 and nums2[i] > nums2[stack[-1]]:
                    if nums2[stack[-1]] in nums1:
                        index = nums1.index(nums2[stack[-1]])
                        result[index] = nums2[i]
                    stack.pop()
                stack.append(i)
        return result
```

{{< /tab >}}

{{< /tabs >}}
