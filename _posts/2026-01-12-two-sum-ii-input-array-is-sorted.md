---
layout: post
title: "LC 167 — Two Sum II - Input Array Is Sorted"
date: 2026-01-12
categories: [leetcode]
tags: [two-pointers, array, binary-search]
difficulty: medium
leetcode_url: "https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/"
---

## Problem

[Two Sum II - Input Array Is Sorted]({{ page.leetcode_url }}) - **{{ page.difficulty | capitalize }}**

Given a **1-indexed** array of integers `numbers` that is already sorted in **non-decreasing order**, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

Return the indices of the two numbers, `index1` and `index2`, **added by one** as an integer array `[index1, index2]` of length 2.

The tests are generated such that there is **exactly one solution**. You **may not** use the same element twice.

Your solution must use only constant extra space.

**Example 1:**
```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].
```

**Example 2:**
```
Input: numbers = [2,3,4], target = 6
Output: [1,3]
Explanation: The sum of 2 and 4 is 6. Therefore, index1 = 1, index2 = 3. We return [1, 3].
```

**Example 3:**
```
Input: numbers = [-1,0], target = -1
Output: [1,2]
Explanation: The sum of -1 and 0 is -1. Therefore, index1 = 1, index2 = 2. We return [1, 2].
```

**Constraints:**
- 2 ≤ numbers.length ≤ 3 * 10⁴
- -1000 ≤ numbers[i] ≤ 1000
- numbers is sorted in non-decreasing order
- -1000 ≤ target ≤ 1000
- The tests are generated such that there is exactly one solution

## Approach

The key insight is to leverage the **sorted property** of the array using a **two-pointer technique**. By comparing the sum to the target, we can decide which pointer to move.

**Why not hash map?**
- The original Two Sum (LC #1) uses a hash map because the array is unsorted
- Here, the array is sorted, so we can use a more space-efficient two-pointer approach
- Hash map would use O(n) space, but two pointers only use O(1) space

**Algorithm:**
1. **Initialize two pointers**: `i` at the start (0) and `j` at the end (len(numbers) - 1)
2. **Calculate sum**: While `i < j`, compute `sum = numbers[i] + numbers[j]`
3. **Compare and adjust**:
   - If `sum == target`: We found the answer! Return `[i + 1, j + 1]` (1-indexed)
   - If `sum < target`: The sum is too small, so increment `i` to get a larger value
   - If `sum > target`: The sum is too large, so decrement `j` to get a smaller value
4. **Guaranteed solution**: The problem states there's exactly one solution, so we'll always find it

**Why this works:**
- **Sorted array property**: Moving left pointer increases sum, moving right pointer decreases sum
- **Convergence**: The pointers always move toward the solution
- **Example walkthrough** with `[2, 7, 11, 15]`, target = 9:
  - Initial: i=0 (val=2), j=3 (val=15), sum=17 > 9 → decrease j
  - Next: i=0 (val=2), j=2 (val=11), sum=13 > 9 → decrease j
  - Next: i=0 (val=2), j=1 (val=7), sum=9 == 9 → found! Return [1, 2]

**Time Complexity:** O(n) where n is the length of the array - each pointer moves at most n times

**Space Complexity:** O(1) - only using two pointer variables

## Solution

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        # Given a 1-indexed array of integers numbers that is already sorted
        # in non-decreasing order, find 2 numbers such that they add up to a specific target number

        i = 0
        j = len(numbers) - 1

        while i < j:
            sum = numbers[i] + numbers[j]

            if sum == target:
                return [i + 1, j + 1]
            elif sum < target:  # Need a larger sum, move left pointer right
                i += 1
            elif sum > target:  # Need a smaller sum, move right pointer left
                j -= 1

        return []
```

## Key Takeaways

- **Leveraging sorted property**: The sorted array enables the two-pointer approach, which is more space-efficient than hash map
- **Pointer movement logic**: Smaller sum → move left pointer right; larger sum → move right pointer left
- **1-indexed return**: Remember to add 1 to both indices when returning the result
- **Guaranteed solution**: The problem guarantees exactly one solution, so no need to handle edge cases
- **Two-pointer vs hash map tradeoff**: Two pointers trade O(n) space for O(n) time, both linear but different constants
- **Pattern recognition**: This two-pointer pattern works for many sorted array problems

## Related Problems

- [Two Sum](https://leetcode.com/problems/two-sum/) - Original unsorted version using hash map
- [3Sum](https://leetcode.com/problems/3sum/) - Extension to finding three numbers that sum to target
- [Container With Most Water](https://leetcode.com/problems/container-with-most-water/) - Another two-pointer problem
