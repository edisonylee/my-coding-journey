---
layout: post
title: "LC 238 — Product of Array Except Self"
date: 2026-01-10
categories: [leetcode]
tags: [array, prefix-sum, math]
difficulty: medium
leetcode_url: "https://leetcode.com/problems/product-of-array-except-self/"
---

## Problem

[Product of Array Except Self]({{ page.leetcode_url }}) - **{{ page.difficulty | capitalize }}**

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

The product of any prefix or suffix of `nums` is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operator.

**Example 1:**
- Input: `nums = [1,2,3,4]`
- Output: `[24,12,8,6]`

**Example 2:**
- Input: `nums = [-1,1,0,-3,3]`
- Output: `[0,0,9,0,0]`

**Constraints:**
- 2 ≤ nums.length ≤ 10⁵
- -30 ≤ nums[i] ≤ 30
- The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer

**Follow up:** Can you solve the problem in O(1) extra space complexity? (The output array does not count as extra space for space complexity analysis.)

## Approach

The key insight is that for each index `i`, the result is the product of all numbers **before** `i` (prefix) multiplied by all numbers **after** `i` (suffix).

**Two-Pass Solution:**
1. **First pass (prefix)**: Calculate prefix products from left to right
   - For each position, store the product of all elements to its left
   - Start with `postfix = 1` and multiply as we go
2. **Second pass (suffix)**: Calculate suffix products from right to left
   - For each position, multiply its current value by the product of all elements to its right
   - Start with `suffix = 1` and multiply as we go

**Example walkthrough with `nums = [1,2,3,4]`:**

After prefix pass: `res = [1, 1, 2, 6]`
- res[0] = 1 (no elements before index 0)
- res[1] = 1 (product of elements before: 1)
- res[2] = 2 (product of elements before: 1×2)
- res[3] = 6 (product of elements before: 1×2×3)

After suffix pass: `res = [24, 12, 8, 6]`
- res[3] = 6×4 = 24 (6 × product of elements after: 4)
- res[2] = 2×(4×3) = 24 (2 × product of elements after: 3×4)
- res[1] = 1×(4×3×2) = 24 (1 × product of elements after: 2×3×4)
- res[0] = 1×(4×3×2×1) = 24 (1 × product of elements after: 1×2×3×4)

Wait, let me recalculate:
- res[0] = 1 × (2×3×4) = 24 ✓
- res[1] = 1 × (3×4) = 12 ✓
- res[2] = 2 × 4 = 8 ✓
- res[3] = 6 × 1 = 6 ✓

**Time Complexity:** O(n) - two passes through the array

**Space Complexity:** O(1) - only using the output array (which doesn't count) and two variables

## Solution

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        res = [1] * len(nums)
        postfix = 1
        for i in range(len(nums)):
            res[i] = postfix
            postfix *= nums[i]
        suffix = 1
        for i in range(len(nums) -1, -1, -1):
            res[i] *= suffix
            suffix *= nums[i]
        return res
```

## Key Takeaways

- **Prefix and suffix products**: Breaking down the problem into products before and after each element
- **Two-pass technique**: First pass builds prefix, second pass applies suffix
- **Space optimization**: Use the output array to store intermediate results instead of creating separate arrays
- **No division needed**: This approach naturally avoids division, handling edge cases like zeros
- **Running product pattern**: Maintain a running product variable that accumulates as we iterate

## Related Problems

- [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/) - Finding max product in contiguous subarray
- [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/) - Similar prefix/suffix approach
- [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) - Single pass optimization pattern
