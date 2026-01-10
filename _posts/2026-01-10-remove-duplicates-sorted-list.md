---
layout: post
title: "LC 083 — Remove Duplicates from Sorted List"
date: 2026-01-10
categories: [leetcode]
tags: [linked-list, two-pointers]
difficulty: easy
leetcode_url: "https://leetcode.com/problems/remove-duplicates-from-sorted-list/"
---

## Problem

[Remove Duplicates from Sorted List]({{ page.leetcode_url }}) - **{{ page.difficulty | capitalize }}**

Given the `head` of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

**Example 1:**
- Input: `head = [1,1,2]`
- Output: `[1,2]`

**Example 2:**
- Input: `head = [1,1,2,3,3]`
- Output: `[1,2,3]`

**Constraints:**
- The number of nodes in the list is in the range [0, 300]
- -100 ≤ Node.val ≤ 100
- The list is guaranteed to be sorted in ascending order

## Approach

Since the linked list is already **sorted**, all duplicate values will be adjacent to each other. We can use a single pointer to traverse the list and skip over duplicates.

**Algorithm:**
1. Start with `curr` pointing to the head of the list
2. While `curr` and `curr.next` both exist:
   - If `curr.val == curr.next.val`:
     - Skip the duplicate by setting `curr.next = curr.next.next`
     - Don't move `curr` forward (there might be more duplicates)
   - Else:
     - Move to the next node: `curr = curr.next`
3. Return the original head

**Why this works:**
- The list is sorted, so duplicates are consecutive
- By comparing only adjacent nodes, we catch all duplicates
- We skip duplicates by bypassing nodes, not physically deleting them
- We don't move `curr` forward when we find a duplicate because there could be multiple duplicates in a row

**Time Complexity:** O(n) where n is the number of nodes - we visit each node once

**Space Complexity:** O(1) - we only use a single pointer, no extra space needed

## Solution

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        curr = head # temp head
        while curr and curr.next: # while curr and curr.next are true
            if curr.val == curr.next.val: # if the values are equal
                curr.next = curr.next.next # set the next pointer to the next node
            else:
                curr = curr.next # if not equal, move to the next
        return head
```

## Key Takeaways

- **Sorted list advantage**: When a list is sorted, duplicates are always adjacent, simplifying the logic
- **Pointer manipulation**: Removing nodes by reassigning `next` pointers is more efficient than creating new nodes
- **Don't move on duplicates**: When we find a duplicate, we stay at the current node to check for more duplicates
- **No dummy node needed**: Since we're never removing the head, we don't need a dummy node
- **Two-pointer check**: Always check both `curr` and `curr.next` exist before accessing `curr.next.val`

## Related Problems

- [Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/) - Remove all nodes that have duplicates
- [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) - Array version of this problem
- [Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/) - Remove nodes by value
