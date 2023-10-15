---
title: 704. 二分查找 (Binary Search)
linktitle: 704. 二分查找
type: book
date: "2019-05-09T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## 描述 (Description)

给定一个 `n` 个元素有序的（升序）整型数组 `nums` 和一个目标值 `target` ，写一个函数搜索 `nums` 中的 `target`，如果目标值存在返回下标，否则返回 `-1`。

https://leetcode.cn/problems/binary-search/

**Example 1:**

> Input: nums = [-1,0,3,5,9,12], target = 9

> Output: 4

**Example 2:**

> Input: nums = [-1,0,3,5,9,12], target = 2

> Output: -1

## 提示 (Constraints)

- `n` 将在 `[1, 10000]` 之间。
- `nums` 的每个元素都将在 `[-9999, 9999]` 之间。

## 分析 (Analysis)

在一个**左闭右闭**的区间里，`[left, right]`。

## 代码 (Code)

- 时间复杂度：`O(log n)`
- 空间复杂度：`O(1)`

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
func search(nums []int, target int) int {
    high := len(nums)-1
    low := 0
    for low <= high {
        mid := low + (high-low)/2
        if nums[mid] == target {
            return mid
        } else if nums[mid] > target {
            high = mid-1
        } else {
            low = mid+1
        }
    }
    return -1
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums)-1
        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] > target:
                right = mid - 1
            elif nums[mid] < target:
                left = mid + 1
            else:
                return mid
        return -1
```

{{< /tab >}}

{{< tab tabName="Rust" >}}

```rust
impl Solution {
    pub fn search(nums: Vec<i32>, target: i32) -> i32 {
        let mut left:usize = 0;
        let mut right:usize = nums.len() - 1;
        while left as i32 <= right as i32{
            let mid = (left + right) / 2;
            if nums[mid] < target {
                left = mid + 1;
            } else if nums[mid] > target {
                right = mid - 1;
            } else {
                return mid as i32;
            }
        }
        -1
    }
}

```

{{< /tab >}}

{{< /tabs >}}
