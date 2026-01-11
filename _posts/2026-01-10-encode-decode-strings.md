---
layout: post
title: "LC 271 — Encode and Decode Strings"
date: 2026-01-10
categories: [leetcode]
tags: [string, design, encoding]
difficulty: medium
leetcode_url: "https://leetcode.com/problems/encode-and-decode-strings/"
---

## Problem

[Encode and Decode Strings]({{ page.leetcode_url }}) - **{{ page.difficulty | capitalize }}**

Design an algorithm to encode a list of strings to a single string. The encoded string is then decoded back to the original list of strings.

Please implement `encode` and `decode`.

**Example 1:**
- Input: `["Hello","World"]`
- Output: `["Hello","World"]`
- Explanation: One possible encode method is: `"Hello" + "World"` → encode → `"HelloWorld"` → decode → `["Hello","World"]`

**Example 2:**
- Input: `[""]`
- Output: `[""]`

**Constraints:**
- 0 ≤ strs.length < 200
- 0 ≤ strs[i].length < 200
- strs[i] contains any possible characters out of 256 valid ASCII characters

**Note:** The string may contain any possible characters including special characters. Your algorithm must be able to handle strings containing any character.

## Approach

The challenge is that strings can contain ANY characters, including delimiters we might want to use. A simple delimiter like `#` won't work because the string itself might contain `#`.

**Solution: Length-Prefix Encoding**

We encode each string with its length followed by a delimiter, then the actual string:
- Format: `"<length>#<string>"`
- Example: `["hi", "world"]` → `"2#hi5#world"`

**Why this works:**
- We know exactly how many characters to read for each string
- Strings can contain ANY characters (including `#`) without breaking the encoding
- The `#` delimiter separates the length from the content, not string from string

**Encoding Algorithm:**
1. For each string in the list:
   - Get its length
   - Append `<length>#<string>` to the result
2. Return the concatenated result

**Decoding Algorithm:**
1. Initialize pointer `i = 0` and empty result list
2. While `i < len(encoded_string)`:
   - Find the `#` delimiter (using pointer `j`)
   - Extract the length: `int(s[i:j])`
   - Extract the string: `s[j+1 : j+1+length]`
   - Add to result list
   - Move `i` to the next length prefix
3. Return the result list

**Example walkthrough:**

Encode `["hi", "world"]`:
- "hi" has length 2 → `"2#hi"`
- "world" has length 5 → `"5#world"`
- Result: `"2#hi5#world"`

Decode `"2#hi5#world"`:
- i=0: Read "2", find '#' at j=1, length=2, extract "hi" (positions 2-3), i→4
- i=4: Read "5", find '#' at j=5, length=5, extract "world" (positions 6-10), i→11
- Result: `["hi", "world"]`

**Time Complexity:** O(n) where n is the total length of all strings combined

**Space Complexity:** O(n) for the encoded string (output space)

## Solution

```python
from typing import List

class Codec:
    def encode(self, strs: List[str]) -> str:
        """
        Encode a list of strings into one string using length-prefixing.

        Format per string: "<length>#<string>"
        Example: ["hi", "world"] -> "2#hi5#world"

        Why this works:
        - We store the length first, so strings can contain ANY characters (including '#')
          without breaking decoding.
        """
        encoded = ""
        for s in strs:
            # Prefix each string with its length and a delimiter '#'
            # so decoding knows exactly how many chars to read next.
            encoded += str(len(s)) + "#" + s
        return encoded

    def decode(self, s: str) -> List[str]:
        """
        Decode a single encoded string back into the original list of strings.

        We scan left-to-right:
        1) Read digits until '#': that's the length L
        2) Read the next L characters: that's the string
        3) Repeat until we reach the end
        """
        decoded = []
        i = 0  # pointer to where the next length starts

        while i < len(s):
            j = i  # pointer used to find the '#'

            # Move j until we hit the delimiter '#'
            # Everything from s[i:j] is the length (as text).
            while s[j] != "#":
                j += 1

            length = int(s[i:j])  # convert length substring to an integer
            start = j + 1         # first character of the actual string
            end = start + length  # end boundary (exclusive)

            # Extract the string of known length and store it
            decoded.append(s[start:end])

            # Jump i to the next length prefix (right after the extracted string)
            i = end

        return decoded
```

## Key Takeaways

- **Length-prefix encoding**: Solves the delimiter problem by storing the length before each string
- **Two-pointer technique**: Use one pointer for length start (`i`) and one to find delimiter (`j`)
- **Handle any characters**: This approach works even if strings contain special characters, newlines, or delimiters
- **String slicing**: `s[i:j]` extracts length, `s[start:end]` extracts the actual string content
- **State machine pattern**: The decoder works as a simple state machine (read length → read string → repeat)

## Related Problems

- [Design Compressed String Iterator](https://leetcode.com/problems/design-compressed-string-iterator/) - Run-length encoding
- [String Compression](https://leetcode.com/problems/string-compression/) - In-place compression
- [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/) - Similar encoding/decoding pattern
