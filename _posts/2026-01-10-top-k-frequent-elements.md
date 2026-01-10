---
layout: post
title: "LC 347 — Top K Frequent Elements"
date: 2026-01-10
categories: [leetcode]
tags: [hash-map, array, bucket-sort, heap]
difficulty: medium
leetcode_url: "https://leetcode.com/problems/top-k-frequent-elements/"
---

## Problem

[Top K Frequent Elements]({{ page.leetcode_url }}) - **{{ page.difficulty | capitalize }}**

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements. You may return the answer in any order.

**Example 1:**
- Input: `nums = [1,1,1,2,2,3], k = 2`
- Output: `[1,2]`

**Example 2:**
- Input: `nums = [1], k = 1`
- Output: `[1]`

**Constraints:**
- 1 ≤ nums.length ≤ 10⁵
- -10⁴ ≤ nums[i] ≤ 10⁴
- k is in the range [1, the number of unique elements in the array]
- It is guaranteed that the answer is unique

## Approach

The key insight is to use **bucket sort** to organize numbers by their frequency. Instead of sorting (which would be O(n log n)), we can achieve O(n) time by using the frequency as an array index.

**Algorithm:**
1. **Count frequencies**: Create a hash map to count how many times each number appears
2. **Create frequency buckets**: Create an array of lists where `freq[i]` contains all numbers that appear exactly `i` times
   - The array needs `len(nums) + 1` buckets because the maximum possible frequency is `len(nums)`
3. **Fill the buckets**: For each number and its frequency, place the number into the bucket at index `frequency`
4. **Collect results**: Iterate from the highest frequency bucket down to lowest, collecting numbers until we have `k` elements

**Why this works:**
- By using frequency as the array index, we automatically have numbers sorted by frequency
- We can iterate from high to low frequency without actually sorting
- We can stop early once we've collected `k` elements

**Time Complexity:** O(n) where n is the length of nums - we iterate through the array a constant number of times

**Space Complexity:** O(n) for the hash map and frequency buckets

## Solution

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # Step 1: Count how many times each number appears
        # count[num] = frequency of num
        count = {}
        for n in nums:
            count[n] = count.get(n, 0) + 1

        # Step 2: Create buckets where index = frequency
        # freq[i] will store all numbers that appear exactly i times
        # We need len(nums) + 1 buckets because the maximum possible
        # frequency of any number is len(nums)
        freq = []
        for _ in range(len(nums) + 1):
            freq.append([])

        # Step 3: Place each number into the bucket
        # corresponding to its frequency
        for num, frequency in count.items():
            freq[frequency].append(num)

        # Step 4: Collect the k most frequent elements
        # Iterate from highest frequency to lowest
        res = []
        for i in range(len(freq) - 1, 0, -1):
            for num in freq[i]: # For each list at freq[i], go thru the values
                res.append(num) # append the element or elements at freq[i]
                # Once we have k elements, we can stop early
                if len(res) == k:
                    return res
```

## Key Takeaways

- **Bucket sort pattern**: Using frequency as an index is a powerful O(n) sorting technique when the range is limited
- **Frequency buckets**: Creating `len(nums) + 1` buckets ensures we can handle the maximum possible frequency
- **Early termination**: We can stop collecting elements once we reach `k`, making this efficient
- **Alternative approaches**: Could use a heap (O(n log k)) or sorting (O(n log n)), but bucket sort is optimal at O(n)
- **Space-time tradeoff**: We use O(n) extra space to achieve O(n) time complexity

## Related Problems

- [Top K Frequent Words](https://leetcode.com/problems/top-k-frequent-words/) - Similar problem with strings
- [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) - Similar k-th element pattern
- [Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/) - Frequency sorting pattern
