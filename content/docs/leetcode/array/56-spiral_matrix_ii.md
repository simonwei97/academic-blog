---
title: 56. 螺旋矩阵 II (Spiral Matrix II)
linktitle: 56. 螺旋矩阵 II
type: book
date: "2019-05-09T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 6
---

## 描述 (Description)

给你一个正整数 n ，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 。

https://leetcode.com/problems/spiral-matrix-ii/

**Example 1:**

> Input: n = 3

> Output: [[1,2,3],[8,9,4],[7,6,5]]

![](/docs/leetcode/spiraln3.jpeg)

**Example 2:**

> Input: n = 1

> Output: [[1]]

## 提示 (Constraints)

- `1 <= n <= 20`

## 分析 (Analysis)

在一个**左闭右闭**的区间里，`[left, right]`。

## 代码 (Code)

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
func generateMatrix(n int) [][]int {
    top, bottom := 0, n-1
    left, right := 0, n-1

    matrix := make([][]int, n)
    for i := 0; i < n; i++ {
        matrix[i] = make([]int, n)
    }

    num := 1
    for num <= n*n {
        // left to right
        for i := left; i <= right; i++ {
            matrix[top][i] = num
            num++
        }
        top++
        // top to bottom
        for i := top; i <= bottom; i++ {
            matrix[i][right] = num
            num++
        }
        right--
        // right to left
        for i := right; i >= left; i-- {
            matrix[bottom][i] = num
            num++
        }
        bottom--
        // bottom to top
        for i := bottom; i >= top; i-- {
            matrix[i][left] = num
            num++
        }
        left++
    }
    return matrix
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        top, bottom = 0, n-1
        left, right = 0, n-1

        matrix = [[0 for _ in range(n)] for _ in range(n)]

        num = 1
        while num <= n*n:
            # left to right
            for i in range(left, right+1):
                matrix[top][i] = num
                num += 1
            top += 1
            # top to bottom
            for i in range(top, bottom+1):
                matrix[i][right] = num
                num += 1
            right -= 1
            # right to left
            for i in range(right, left-1, -1):
                matrix[bottom][i] = num
                num += 1
            bottom -= 1
            # bottom to top
            for i in range(bottom, top-1, -1):
                matrix[i][left] = num
                num += 1
            left += 1
        return matrix
```

{{< /tab >}}

{{< /tabs >}}
