---
title: 84. 柱状图中最大的矩形 (Largest Rectangle In Histogram)
linktitle: 84. 柱状图中最大的矩形
type: book
date: "2022-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
---

[LeetCode Link](https://leetcode.cn/problems/largest-rectangle-in-histogram/)

## 描述

给定 `n` 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 `1` 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

**Example 1:**

> Input: heights = [2,1,5,6,2,3]

> Output: 10

![图示](/docs/leetcode/largestRectangleArea-1.jpeg)

**Example 2:**

> Input: heights = [2,4]

> Output: 4

## 提示 (Constraints)

- `1 <= heights.length <=10^5`
- `0 <= height[i] <= 10^4`

## 分析

利用单调栈的特性，通过维护一个递增的栈来计算最大矩形面积。具体步骤如下：

1. 创建一个空栈，用于存储柱子的索引。
2. 在柱状图的末尾添加一个高度为 0 的柱子，以便将所有柱子都处理完毕。
3. 遍历所有柱子的高度：
   - 如果栈不为空且当前柱子的高度小于等于栈顶柱子的高度，则说明栈顶柱子的右边界已确定，可以计算栈顶柱子的面积。
   - 弹出栈顶柱子的索引，并计算弹出柱子后的面积。
   - 更新最大面积。
4. 将当前柱子的索引入栈。
5. 返回最大面积。

通过这种方式，可以在一次遍历中找到柱状图中最大的矩形面积。

- 时间复杂度分析：`O(n)`
  - 通过一次遍历即可计算出最大矩形面积。因此，时间复杂度为 `O(n)`，其中 `n` 是柱子的数量。
- 空间复杂度分析：`O(n)`
  - 算法使用了一个栈来存储柱子的索引，栈的最大长度为 `n`。因此，空间复杂度为 `O(n)`。

## 代码

{{< tabs tabTotal="2">}}

{{< tab tabName="Go">}}

```golang
func largestRectangleArea(heights []int) int {
    // 创建一个空栈，用于存储柱子的索引
    stack := make([]int, 0)
    // 在柱状图的末尾添加一个高度为 0 的柱子，以便将所有柱子都处理完毕
    heights = append(heights, 0)
    // 初始化最大面积为 0
    maxArea := 0
    // 遍历所有柱子的高度
    for i := 0; i < len(heights); i++ {
        // 如果栈不为空且当前柱子的高度小于等于栈顶柱子的高度
        for len(stack) > 0 && heights[i] <= heights[stack[len(stack)-1]] {
            h := heights[stack[len(stack)-1]] // 弹出栈顶柱子的索引
            stack = stack[:len(stack)-1]
            w := i
            if len(stack) > 0 {
                w = i - stack[len(stack)-1] - 1 // 计算弹出柱子后的面积
            }
            area := h * w
            if area > maxArea { // 更新最大面积
                maxArea = area
            }
        }
        stack = append(stack, i) // 将当前柱子的索引入栈
    }
    return maxArea
}
```

{{< /tab >}}

{{< tab tabName="Python">}}

```py
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        heights.insert(0, 0)
        heights.append(0)
        stack = [0]
        result = 0
        for i in range(1, len(heights)):
            while stack and heights[i] < heights[stack[-1]]:
                mid_height = heights[stack[-1]]
                stack.pop()
                if stack:
                    # area = width * height
                    area = (i - stack[-1] - 1) * mid_height
                    result = max(area, result)
            stack.append(i)
        return result
```

{{< /tab >}}

{{< /tabs >}}
