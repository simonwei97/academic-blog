---
title: 1. 两数之和 (2Sum)
linktitle: 1. 两数之和
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## 描述 (Description)

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** `target` 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

**Example 1:**

> Input: nums = [2,7,11,15], target = 9

> Output: [0,1]

**Example 2:**

> Input: nums = [3,2,4], target = 6

> Output: [1,2]

**Example 3:**

> Input: nums = [3,3], target = 6

> Output: [0,1]

## 提示 (Constraints)

- `2 <= nums.length <= 10^4`
- `−10^9 <= nums[i] <= 10^9`
- `−10^9 <= target <= 10^9`
- 只会存在一个有效答案.

## 分析 (Analysis)

- :x: 方法 1：暴力，复杂度 `O(n^2)`，会超时。
- :white_check_mark: 方法 2：`hash`。用一个哈希表，存储每个数对应的下标，复杂度 `O(n)`.
- :x: 方法 3：先排序，然后左右夹逼，排序 `O(nlogn)`，左右夹逼 `O(n)`，最终 `O(nlogn)`。但是注意，这题需要返回的是下标，而不是数字本身，因此这个方法行不通。

## 代码 (Code)

- 时间复杂度：`O(n)`
- 空间复杂度：`O(n)`

{{< tabs tabTotal="4">}}
{{< tab tabName="Go">}}

```golang
func twoSum(nums []int, target int) []int {
    hashMap := make(map[int]int)
    for index, val := range nums {
        res := target - val
        if _, ok := hashMap[res]; ok {
            return []int{hashMap[res], index}
        }
        hashMap[val] = index
    }
    return nil
}
```

{{< /tab >}}
{{< tab tabName="Python" >}}

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        m = {num: i for i, num in enumerate(nums)}

        for i, num in enumerate(nums):
            complement = m.get(target - num)
            if complement is not None and complement > i:
                return [i, complement]

        return None
```

{{< /tab >}}
{{< tab tabName="Java" >}}

```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> m = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            m.put(nums[i], i);
        }
        for (int i = 0; i < nums.length; i++) {
            final Integer complement = m.get(target-nums[i]);
            if (complement != null && complement > i) {
                return new int[]{i, complement};
            }
        }
        return null;
    }
};
```

{{< /tab >}}
{{< tab tabName="C++">}}

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> m;
        for (int i = 0; i < nums.size(); i++) {
            m[nums[i]] = i;
        }
        for (int i = 0; i < nums.size(); i++) {
            auto complement = m.find(target - nums[i]);
            if (complement != m.end() && complement->second > i) {
                return {i, complement->second};
            }
        }
        return {-1, -1};
    }
};
```

{{< /tab >}}
{{< /tabs >}}
