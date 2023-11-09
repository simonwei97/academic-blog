---
title: 快排 Quick Sort
subtitle: 快排 Quick Sort.

# Summary for listings and search engines
summary: 快排 Quick Sort.

# Link this post with a project
projects: []

# Date published
date: "2020-12-13T00:00:00Z"

# Date updated
lastmod: "2020-12-13T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

toc: true

pager: true

show_related: true

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: "Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)"
  focal_point: ""
  placement: 2
  preview_only: false

authors:
  - admin

tags:
  - Algo

categories:
  - Note
---

## 概述

快排使用分而治之的策略。

## 步骤

1. 从数组中选择一个元素，作为基准（`pivot`）。
2. 重新排列数组，所有比基准元素小的值放在基准前面，所有比基准元素大的值放在基准后面，相同的话放在任意一边均可以。此时基准位于数组的中间位置。
3. 递归地将小于基准元素的子序列和大于基准元素的子序列进行排序。

## 代码

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
func quickSort(nums []int) []int {
    low := 0
    high := len(nums) - 1

    partition(nums, low, high)
    return nums
}

func partition(nums []int, low int, high int) {
    if low >= high {
        return
    }

    l, r := low, high
    mid := (r-l)/2 + l
    pivot := nums[mid]
    for l <= r {
        for l <= r && nums[l] < pivot {
            l++
        }
        for l <= r && nums[r] > pivot {
            r--
        }

        if l <= r {
            nums[l], nums[r] = nums[r], nums[l]
            l++
            r--
        }
    }

    partition(nums, low, r)
    partition(nums, l, high)
}

```

{{< /tab >}}

{{< tab tabName="Python" >}}

```python
def quickSort(nums: List[int]) -> List[int]:
    low = 0
    high = len(nums) - 1

    partition(nums, low, high)
    return nums

def partition(nums: List[int], low: int, high: int):
    if low >= high:
        return

    l, r = low, high
    mid = (r - l) / 2 + l
    pivot = nums[mid]
    while l <= r:
        while l <= r and nums[l] < pivot:
            l += 1
        while l <= r and nums[r] > pivot:
            r -= 1

        if l <= r:
            nums[l], nums[r] = nums[r], nums[l]
            l += 1
            r -= 1

    partition(nums, low, r)
    partition(nums, l, high)
```

{{< /tab >}}

{{< tab tabName="Java" >}}

```java
/**
 * 快速排序演示
 */
public class QuickSort {
    public static void main(String[] args) {
        int[] arr = {5, 1, 7, 3, 1, 6, 9, 4};

        quickSort(arr, 0, arr.length - 1);

        for (int i : arr) {
            System.out.print(i + "\t");
        }
    }

    /**
     * @param arr        待排序列
     * @param leftIndex  待排序列起始位置
     * @param rightIndex 待排序列结束位置
     */
    private static void quickSort(int[] arr, int leftIndex, int rightIndex) {
        if (leftIndex >= rightIndex) {
            return;
        }

        int left = leftIndex;
        int right = rightIndex;
        // 待排序的第一个元素作为基准值
        int key = arr[left];

        // 从左右两边交替扫描，直到left = right
        while (left < right) {
            while (right > left && arr[right] >= key) {
                // 从右往左扫描，找到第一个比基准值小的元素
                right--;
            }

            // 找到这种元素将arr[right]放入arr[left]中
            arr[left] = arr[right];

            while (left < right && arr[left] <= key) {
                //从左往右扫描，找到第一个比基准值大的元素
                left++;
            }

            // 找到这种元素将arr[left]放入arr[right]中
            arr[right] = arr[left];
        }
        // 基准值归位
        arr[left] = key;
        // 对基准值左边的元素进行递归排序
        quickSort(arr, leftIndex, left - 1);
        // 对基准值右边的元素进行递归排序。
        quickSort(arr, right + 1, rightIndex);
    }
}
```

{{< /tab >}}

{{< tab tabName="Rust" >}}

```rust
// TODO
```

{{< /tab >}}

{{< /tabs >}}

## 参考
