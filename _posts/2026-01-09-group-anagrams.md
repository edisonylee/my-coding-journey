---
layout: post
title: "LC 049 — Group Anagrams"
date: 2026-01-09
categories: [leetcode]
tags: [hash-map, string, array, sorting]
difficulty: medium
leetcode_url: "https://leetcode.com/problems/group-anagrams/"
---

## Problem

[Group Anagrams]({{ page.leetcode_url }}) - **{{ page.difficulty | capitalize }}**

Given an array of strings `strs`, group the anagrams together. You can return the answer in any order.

An anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**
- Input: `strs = ["eat","tea","tan","ate","nat","bat"]`
- Output: `[["bat"],["nat","tan"],["ate","eat","tea"]]`

**Example 2:**
- Input: `strs = [""]`
- Output: `[[""]]`

**Example 3:**
- Input: `strs = ["a"]`
- Output: `[["a"]]`

**Constraints:**
- 1 ≤ strs.length ≤ 10⁴
- 0 ≤ strs[i].length ≤ 100
- strs[i] consists of lowercase English letters

## Approach

The key insight is finding a **commonality** between anagrams. Words that are anagrams will have the same characters when sorted. We can use this sorted string as a key in a hash map to group anagrams together.

**Algorithm:**
1. Initialize an empty dictionary `dic = {}`
2. Loop through all words in the input array
3. For each word:
   - Sort the word and convert it back to a string: `key = "".join(sorted(word))`
   - This sorted string becomes our dictionary key
   - If the key doesn't exist in the dictionary, initialize it with an empty list: `dic[key] = []`
   - Append the current word to the list at `dic[key]`
4. Return all the values from the dictionary as a list: `list(dic.values())`

**Why this works:**
- All anagrams will produce the same sorted string
- Example: "eat", "tea", "ate" all sort to "aet"
- By using sorted strings as keys, we automatically group anagrams together

**Time Complexity:** O(n * k log k) where n is the number of strings and k is the maximum length of a string (due to sorting each word)

**Space Complexity:** O(n * k) to store all strings in the dictionary

## Solution

### Handwritten Walkthrough

![Group Anagrams Solution]({{ '/assets/images/lc49.png' | relative_url }})

### Code Implementation

```python
def groupAnagrams(strs):
    # Initialize the dictionary
    dic = {}

    # Loop through all the words in the list
    for word in strs:
        # Create key by sorting the word
        key = "".join(sorted(word))  # stores the sorted string

        # If key not in dic, going to append current word
        if key not in dic:
            dic[key] = []  # init w/an empty list

        # Append current word
        dic[key].append(word)  # append current word

    # Return a list of the values
    return list(dic.values())
```

## Key Takeaways

- **Sorted strings as keys**: Using sorted characters as hash map keys is a powerful pattern for grouping anagrams
- **Dictionary grouping pattern**: Initialize empty list if key doesn't exist, then append - this is a common pattern for grouping items
- **`"".join(sorted(word))`**: Combines sorting and string conversion in one line
- **`dic.values()`**: Returns all grouped lists, which is exactly what we need
- **Trading space for time**: Using a hash map provides O(1) lookup at the cost of O(n*k) space

## Related Problems

- [Valid Anagram](https://leetcode.com/problems/valid-anagram/) - Check if two strings are anagrams
- [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/) - Sliding window variant
- [Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/) - Similar frequency pattern