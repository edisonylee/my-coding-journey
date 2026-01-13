---
layout: post
title: "LC 128 — Longest Consecutive Sequence"
date: 2026-01-11
categories: [leetcode]
tags: [array, hash-set, union-find]
difficulty: medium
leetcode_url: "https://leetcode.com/problems/longest-consecutive-sequence/"
---

## Problem

[Longest Consecutive Sequence]({{ page.leetcode_url }}) - **{{ page.difficulty | capitalize }}**

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.

**Example 1:**
```
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

**Example 2:**
```
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```

**Constraints:**
- 0 ≤ nums.length ≤ 10⁵
- -10⁹ ≤ nums[i] ≤ 10⁹

## Approach

The key insight is to use a **set for O(1) lookups** and only start counting from the **beginning of each sequence**. This avoids redundant work and achieves O(n) time complexity.

**Naive approach (why it doesn't work):**
- Sorting would be O(n log n), which violates the time constraint
- Checking every number as a potential sequence start would lead to O(n²) in worst case

**Optimal approach:**
1. **Convert to set**: Create a set from the array for O(1) average-time lookups and to remove duplicates
2. **Identify sequence starts**: For each number `n`, check if `n - 1` exists in the set
   - If `n - 1` does NOT exist, then `n` is the start of a sequence
   - If `n - 1` exists, skip `n` (it will be counted as part of another sequence)
3. **Count forward**: Once we identify a sequence start, count how many consecutive numbers exist
   - Initialize `length = 0`
   - While `n + length` exists in the set, increment `length`
4. **Track maximum**: Keep track of the longest sequence found

**Why this works:**
- **No redundant counting**: Each number is only checked once as a potential sequence start
- **O(1) lookups**: Set membership checks are O(1) average time
- **Smart filtering**: By only starting from sequence beginnings (where `n - 1` not in set), we ensure each sequence is counted exactly once
- **Example walkthrough** with `[100, 4, 200, 1, 3, 2]`:
  - Set: {100, 4, 200, 1, 3, 2}
  - Check 100: 99 not in set → sequence start → only 100 → length 1
  - Check 4: 3 in set → skip (will be counted from 1)
  - Check 200: 199 not in set → sequence start → only 200 → length 1
  - Check 1: 0 not in set → sequence start → 1, 2, 3, 4 all exist → length 4
  - Check 3: 2 in set → skip
  - Check 2: 1 in set → skip
  - Maximum length: 4

**Time Complexity:** O(n) - Despite the nested while loop, each number is visited at most twice (once in the outer loop, once as part of a sequence)

**Space Complexity:** O(n) - For storing the set

## Solution

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        # Convert list to set for O(1) average-time lookups
        # This also removes duplicates, which don't affect consecutive sequences
        num_set = set(nums)

        # Tracks the length of the longest consecutive sequence found
        longest = 0

        # Iterate through each unique number
        for n in num_set:
            # Only start counting if `n` is the BEGINNING of a sequence
            # (i.e., there is no number immediately before it)
            if n - 1 not in num_set:
                length = 0  # Length of the current consecutive sequence

                # Count forward while consecutive numbers exist
                while n + length in num_set:
                    length += 1

                # Update global maximum if this sequence is longer
                longest = max(longest, length)

        # Return the length of the longest consecutive sequence
        return longest
```

## Key Takeaways

- **Set for O(1) lookups**: Converting to a set is crucial for achieving O(n) time complexity
- **Sequence start detection**: Checking if `n - 1` exists is an elegant way to identify sequence beginnings
- **Avoiding redundant work**: Only starting from sequence beginnings ensures each number is processed once
- **Why it's O(n) not O(n²)**: The inner while loop only executes for sequence starts, and each number is added to a sequence exactly once
- **Duplicates don't matter**: Sets automatically handle duplicates, simplifying the logic
- **Amortized analysis**: Even though there's a nested loop, the total number of operations across all iterations is bounded by 2n

## Related Problems

- [Binary Tree Longest Consecutive Sequence](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence/) - Tree variation of consecutive sequence
- [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/) - Similar but subsequence doesn't need to be consecutive
- [Consecutive Numbers Sum](https://leetcode.com/problems/consecutive-numbers-sum/) - Different take on consecutive numbers
