---
title: 42. 接雨水 (Trapping Rain Water)
linktitle: 42. 接雨水
type: book
date: "2022-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 4
---

## 描述

给定 `n` 个非负整数表示每个宽度为 `1` 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

**Example 1:**

> Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]

> Output: 6

![图示](/docs/leetcode/trap_water.png)

**Example 2:**

> Input: height = [4,2,0,3,2,5]

> Output: 9

## 提示 (Constraints)

- `n == height.length`
- `1 <= n <= 2 * 10^4`
- `0 <= height[i] <= 10^5`

## 分析

### 双指针

### 单调栈

## 代码

### 双指针

- 时间复杂度：`O(n)`
- 空间复杂度：`O(1)`

{{< tabs tabTotal="2">}}

{{< tab tabName="Go">}}

```golang
func trap(height []int) int {
    left, right := 0, len(height)-1
    leftMax, rightMax := 0, 0
    var res int
    for left < right {
        leftMax = max(leftMax, height[left])
        rightMax = max(rightMax, height[right])
        if height[left] < height[right] {
            res += leftMax - height[left]
            left++
        } else {
            res += rightMax - height[right]
            right--
        }
    }
    return res
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```

{{< /tab >}}

{{< tab tabName="Python">}}

```py
class Solution:
    def trap(self, height: List[int]) -> int:
        leftheight, rightheight = [0]*len(height), [0]*len(height)

        leftheight[0]=height[0]
        for i in range(1,len(height)):
            leftheight[i]=max(leftheight[i-1],height[i])
        rightheight[-1]=height[-1]
        for i in range(len(height)-2,-1,-1):
            rightheight[i]=max(rightheight[i+1],height[i])

        result = 0
        for i in range(0,len(height)):
            summ = min(leftheight[i],rightheight[i])-height[i]
            result += summ
        return result
```

{{< /tab >}}

{{< /tabs >}}

### 单调栈

TODO
