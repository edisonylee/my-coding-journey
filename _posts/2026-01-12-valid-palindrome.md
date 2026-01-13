---
layout: post
title: "LC 125 — Valid Palindrome"
date: 2026-01-12
categories: [leetcode]
tags: [two-pointers, string]
difficulty: easy
leetcode_url: "https://leetcode.com/problems/valid-palindrome/"
---

## Problem

[Valid Palindrome]({{ page.leetcode_url }}) - **{{ page.difficulty | capitalize }}**

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.

**Example 1:**
```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

**Example 2:**
```
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

**Example 3:**
```
Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
```

**Constraints:**
- 1 ≤ s.length ≤ 2 * 10⁵
- s consists only of printable ASCII characters

## Approach

The key insight is to use **two pointers** starting from both ends and move inward, skipping non-alphanumeric characters and comparing characters case-insensitively.

**Algorithm:**
1. **Initialize two pointers**: `i` at the start (0) and `j` at the end (len(s) - 1)
2. **Move pointers inward**: While `i < j`:
   - **Skip non-alphanumeric from left**: While `i < j` and `s[i]` is not alphanumeric, increment `i`
   - **Skip non-alphanumeric from right**: While `i < j` and `s[j]` is not alphanumeric, decrement `j`
   - **Compare characters**: If `s[i].lower() != s[j].lower()`, return False
   - **Move both pointers**: Increment `i`, decrement `j`
3. **Return True**: If we complete the loop without finding mismatches, it's a palindrome

**Why this works:**
- **Two-pointer pattern**: By comparing characters from both ends moving inward, we can verify palindrome property in one pass
- **isalnum() method**: Python's built-in method checks if a character is alphanumeric (letter or digit)
- **Case-insensitive comparison**: Using `.lower()` handles uppercase/lowercase differences
- **In-place validation**: No need to create a cleaned string, saving space
- **Early termination**: Return False immediately when a mismatch is found

**Edge cases handled:**
- Empty string or single character (vacuously true)
- Strings with only non-alphanumeric characters
- Mixed case characters
- Numbers in the string

**Time Complexity:** O(n) where n is the length of the string - each character is checked at most once

**Space Complexity:** O(1) - only using two pointer variables, no additional data structures

## Solution

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        i = 0
        j = len(s) - 1

        while i < j:
            # Skip non-alphanumeric characters from the left
            while i < j and not s[i].isalnum():
                i += 1

            # Skip non-alphanumeric characters from the right
            while i < j and not s[j].isalnum():
                j -= 1

            # Compare characters (case-insensitive)
            if s[i].lower() != s[j].lower():
                return False

            # Move both pointers inward
            i += 1
            j -= 1

        return True
```

## Key Takeaways

- **Two-pointer technique**: Moving from both ends toward the center is efficient for palindrome validation
- **String methods**: `isalnum()` and `lower()` are powerful Python built-in methods for string manipulation
- **Nested while loops**: The inner while loops skip invalid characters without breaking the outer loop structure
- **Condition ordering**: Always check `i < j` first in the inner loops to prevent index out of bounds
- **In-place vs preprocessing**: This approach is more space-efficient than creating a cleaned string first
- **Pattern recognition**: This two-pointer pattern applies to many string and array problems

## Related Problems

- [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/) - Allow one character deletion
- [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) - Palindrome check on linked list
- [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) - Find longest palindromic substring
