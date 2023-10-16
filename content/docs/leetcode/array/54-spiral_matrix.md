---
title: 54. 螺旋矩阵 (Spiral Matrix)
linktitle: 54. 螺旋矩阵
type: book
date: "2019-05-09T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
---

## 描述 (Description)

给你一个 `m` 行 `n` 列的矩阵 `matrix` ，请按照 **顺时针螺旋顺序** ，返回矩阵中的所有元素。

https://leetcode.com/problems/spiral-matrix/

**Example 1:**

> Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]

> Output: [1,2,3,6,9,8,7,4,5]

![](/docs/leetcode/spiral1.jpeg)

**Example 2:**

> Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]

> Output: [1,2,3,4,8,12,11,10,9,5,6,7]

![](/docs/leetcode/spiral2.jpeg)

## 提示 (Constraints)

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 10`
- `-100 <= matrix[i][j] <= 100`

## 分析 (Analysis)

使用模拟方法，按层进行模拟输出。

- 从上至下
- 从左至右

遍历

- 上: `(top, left) --> (top, right)`
- 右: `(top+1, right) --> (bottom, right)`
- 下: `(bottom, right-1) --> (bottom, left+1)`
- 左: `(bottom, left) --> (top+1, left)`

## 代码 (Code)

- 时间复杂度：$O(mn)$
- 空间复杂度：$O(1)$

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
func spiralOrder(matrix [][]int) []int {
    if len(matrix) == 0 || len(matrix[0]) == 0 {
        return []int{}
    }
    var (
        rows, columns = len(matrix), len(matrix[0])
        order = make([]int, rows * columns)
        index = 0
        left, right, top, bottom = 0, columns - 1, 0, rows - 1
    )

    for left <= right && top <= bottom {
        for column := left; column <= right; column++ {
            order[index] = matrix[top][column]
            index++
        }
        for row := top + 1; row <= bottom; row++ {
            order[index] = matrix[row][right]
            index++
        }
        if left < right && top < bottom {
            for column := right - 1; column > left; column-- {
                order[index] = matrix[bottom][column]
                index++
            }
            for row := bottom; row > top; row-- {
                order[index] = matrix[row][left]
                index++
            }
        }
        left++
        right--
        top++
        bottom--
    }
    return order
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```python

```

{{< /tab >}}

{{< /tabs >}}
