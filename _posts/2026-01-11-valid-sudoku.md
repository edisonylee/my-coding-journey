---
layout: post
title: "LC 036 — Valid Sudoku"
date: 2026-01-11
categories: [leetcode]
tags: [array, hash-map, matrix]
difficulty: medium
leetcode_url: "https://leetcode.com/problems/valid-sudoku/"
---

## Problem

[Valid Sudoku]({{ page.leetcode_url }}) - **{{ page.difficulty | capitalize }}**

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits 1-9 without repetition
2. Each column must contain the digits 1-9 without repetition
3. Each of the nine 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition

**Note:**
- A Sudoku board (partially filled) could be valid but is not necessarily solvable
- Only the filled cells need to be validated according to the mentioned rules

**Example 1:**
```
Input: board =
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]

Output: true
```

**Example 2:**
```
Input: board =
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]

Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

**Constraints:**
- board.length == 9
- board[i].length == 9
- board[i][j] is a digit 1-9 or '.'

## Approach

The key insight is to track seen numbers separately for rows, columns, and 3x3 boxes using hash sets. This allows us to validate all three rules in a single pass through the board.

**Algorithm:**
1. **Initialize storage**: Create three separate data structures to track seen numbers:
   - `rows[r]`: Set of numbers seen in row r
   - `cols[c]`: Set of numbers seen in column c
   - `boxes[(r // 3, c // 3)]`: Set of numbers seen in the 3x3 box
2. **Iterate through the board**: Check every cell (r, c) from 0 to 8
3. **Skip empty cells**: If the cell contains '.', continue to the next cell
4. **Check for duplicates**: If the current value already exists in:
   - The current row (`rows[r]`), OR
   - The current column (`cols[c]`), OR
   - The current 3x3 box (`boxes[(r // 3, c // 3)]`)

   Then return False (invalid board)
5. **Add to trackers**: If no duplicate found, add the value to all three trackers
6. **Return True**: If we complete the loops without finding duplicates, the board is valid

**Why this works:**
- **Box index calculation**: `(r // 3, c // 3)` maps each cell to its 3x3 box
  - Top-left box: rows 0-2, cols 0-2 → (0, 0)
  - Top-middle box: rows 0-2, cols 3-5 → (0, 1)
  - Center box: rows 3-5, cols 3-5 → (1, 1)
  - And so on...
- **Single pass efficiency**: We validate all three rules simultaneously as we iterate
- **defaultdict with sets**: Automatically creates empty sets for new keys, simplifying initialization

**Time Complexity:** O(81) = O(1) - We always check exactly 81 cells regardless of input

**Space Complexity:** O(81) = O(1) - Maximum of 9 numbers per row/col/box, with 9 rows, 9 cols, and 9 boxes

## Solution

```python
from collections import defaultdict

class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        # 1. Initialize storage for seen numbers
        rows = defaultdict(set)
        cols = defaultdict(set)
        boxes = defaultdict(set)

        # 2. Iterate through every cell in the 9x9 grid
        for r in range(9):
            for c in range(9):
                val = board[r][c]

                # 3. Skip empty cells
                if val == ".":
                    continue

                # 4. Check if the value already exists in the current Row, Col, or Box
                # Box index is (r // 3, c // 3)
                if (val in rows[r] or
                    val in cols[c] or
                    val in boxes[(r // 3, c // 3)]):
                    return False

                # 5. Add the value to our trackers
                rows[r].add(val)
                cols[c].add(val)
                boxes[(r // 3, c // 3)].add(val)

        # 6. If we finish the loops without returning False, the board is valid
        return True
```

## Key Takeaways

- **Clever indexing with floor division**: `(r // 3, c // 3)` elegantly maps cells to their 3x3 boxes
- **Triple tracking pattern**: Maintaining separate data structures (rows, cols, boxes) enables simultaneous validation of multiple constraints
- **defaultdict convenience**: Using `defaultdict(set)` eliminates the need for explicit initialization checks
- **Early termination**: Return False immediately upon finding a duplicate, avoiding unnecessary checks
- **Constant time/space**: Despite nested loops, both complexity measures are O(1) since the board size is fixed at 9x9
- **Set membership**: O(1) average-time lookup makes this approach very efficient

## Related Problems

- [Sudoku Solver](https://leetcode.com/problems/sudoku-solver/) - Solve the entire Sudoku board using backtracking
- [Valid Tic-Tac-Toe State](https://leetcode.com/problems/valid-tic-tac-toe-state/) - Similar board validation logic
- [Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/) - Another matrix manipulation problem
