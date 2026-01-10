---
layout: post
title: "LC 242 — Valid Anagram"
date: 2026-01-09
categories: [leetcode]
tags: [hash-map, string, sorting]
difficulty: easy
leetcode_url: "https://leetcode.com/problems/valid-anagram/"
---

## Problem

[Valid Anagram]({{ page.leetcode_url }}) - **{{ page.difficulty | capitalize }}**

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

An anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example:**
- Input: `s = "anagram"`, `t = "nagaram"` → Output: `true`
- Input: `s = "rat"`, `t = "car"` → Output: `false`

**Constraints:**
- 1 ≤ s.length, t.length ≤ 5 * 10⁴
- `s` and `t` consist of lowercase English letters

## Approach

The key insight is that two strings are anagrams if they contain the exact same characters with the same frequencies.

**Algorithm (Hash Map):**
1. If the strings have different lengths, they can't be anagrams
2. Count the frequency of each character in the first string
3. Decrement counts for each character in the second string
4. If all counts are zero, the strings are anagrams

**Alternative (Sorting):**
Sort both strings and compare them directly. This is simpler but less efficient.

**Time Complexity:** O(n) - single pass through both strings (hash map approach)
**Space Complexity:** O(1) - at most 26 characters (English lowercase letters)

## Solution

### Hash Map Approach (Optimal)
```python
def isAnagram(s, t):
    if len(s) != len(t):
        return False

    char_count = {}

    # Count characters in s
    for char in s:
        char_count[char] = char_count.get(char, 0) + 1

    # Decrement counts for characters in t
    for char in t:
        if char not in char_count:
            return False
        char_count[char] -= 1
        if char_count[char] < 0:
            return False

    return True
```

### Sorting Approach (Simpler)
```python
def isAnagram(s, t):
    return sorted(s) == sorted(t)
```

**Time Complexity:** O(n log n) - due to sorting
**Space Complexity:** O(n) - for sorted strings

## Key Takeaways

- **Character frequency counting**: Core pattern for many string problems
- **Hash maps for O(1) operations**: Essential for optimization
- **Trade-offs**: Sorting is simpler code but slower; hash map is faster but more code
- **Early exit optimization**: Check lengths first to avoid unnecessary work
- **Python's Counter**: Could also use `from collections import Counter` and compare `Counter(s) == Counter(t)`

## Related Problems

- [Group Anagrams](https://leetcode.com/problems/group-anagrams/) - Grouping multiple anagrams
- [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/) - Sliding window variant
- [Permutation in String](https://leetcode.com/problems/permutation-in-string/) - Similar frequency counting pattern