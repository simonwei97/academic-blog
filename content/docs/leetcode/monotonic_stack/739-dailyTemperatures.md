---
title: 739. 每日温度 (Daily Temperatures)
linktitle: 739. 每日温度
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## 描述

给定一个整数数组 `temperatures` ，表示每天的温度，返回一个数组 `answer` ，其中 `answer[i]` 是指对于第 `i` 天，下一个更高温度出现在几天后。如果气温在这之后都不会升高，请在该位置用 `0` 来代替。

**Example 1:**

> Input: temperatures = [73,74,75,71,69,72,76,73]

> Output: [1,1,4,2,1,1,0,0]

**Example 2:**

> Input: temperatures = [30,40,50,60]

> Output: [1,1,1,0]

**Example 3:**

> Input: temperatures = [30,60,90]

> Output: [1,1,0]

## 提示 (Constraints)

- `1 <= temperatures.length <= 10^5`
- `30 <= temperatures[i] <= 100`

## 分析

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
func dailyTemperatures(temperatures []int) []int {
    res := make([]int, len(temperatures))
    stack := make([]int, 0)
    for index, val := range temperatures {
        // 栈非空, 保证栈里面的元素的单调性
        for len(stack) != 0 && val > temperatures[stack[len(stack)-1]] {
            top := stack[len(stack)-1]
            stack = stack[:len(stack)-1] // pop
            res[top] = index - top
        }
        stack = append(stack, index)
    }
    return res
}
```

{{< /tab >}}
{{< tab tabName="Python">}}

```py
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        answer = [0]*len(temperatures)
        stack = []
        for i in range(len(temperatures)):
            while len(stack) > 0 and temperatures[i] > temperatures[stack[-1]]:
                answer[stack[-1]] = i - stack[-1]
                stack.pop()
            stack.append(i)
        return answer
```

{{< /tab >}}
{{< /tabs >}}
