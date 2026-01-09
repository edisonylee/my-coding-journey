# Content Structure Guide

## Three Types of Posts

Your blog has three distinct content types, each with its own purpose and category:

### 1. **Daily Log** (`categories: [log]`)
- **Purpose**: Daily journal entries documenting your overall progress
- **Location**: Listed at `/log/`
- **Naming**: `YYYY-MM-DD-day-###.md`
- **Content**: Brief summaries of what you did, with links to detailed posts
- **Template**: `_posts/_TEMPLATE.md`

**Example**: `2026-01-09-day-001.md`

```markdown
---
layout: post
title: "Day 1 — Setup + First LeetCode"
date: 2026-01-09
categories: [log]
hours: 2.5
---

## What I Did Today
- Set up blog
- Solved first LeetCode

## LeetCode
Solved **[Two Sum](/2026/01/09/two-sum/)** (LC #1)

## Python
Studied **[List Comprehensions](/2026/01/09/python-list-comprehensions/)**
```

### 2. **LeetCode Solutions** (`categories: [leetcode]`)
- **Purpose**: Detailed writeups of individual LeetCode problems
- **Location**: Listed at `/leetcode/`
- **Naming**: `YYYY-MM-DD-problem-name.md`
- **Content**: Problem statement, approach, solution code, complexity analysis
- **Template**: `_posts/_TEMPLATE_LEETCODE.md`

**Example**: `2026-01-09-two-sum.md`

```markdown
---
layout: post
title: "LC 001 — Two Sum"
date: 2026-01-09
categories: [leetcode]
tags: [array, hash-map]
difficulty: easy
leetcode_url: "https://leetcode.com/problems/two-sum/"
---

## Problem
[Two Sum]({{ page.leetcode_url }}) - **Easy**

## Approach
Hash map for O(n) lookup...

## Solution
```python
def twoSum(nums, target):
    # implementation
```

## Key Takeaways
- Trading space for time
- Complement pattern
```

### 3. **Python Notes** (`categories: [python]`)
- **Purpose**: Deep dives into specific Python concepts, patterns, or techniques
- **Location**: Listed at `/python/`
- **Naming**: `YYYY-MM-DD-python-concept-name.md`
- **Content**: Explanation, syntax, examples, best practices, gotchas
- **Template**: `_posts/_TEMPLATE_PYTHON.md`

**Example**: `2026-01-09-python-list-comprehensions.md`

```markdown
---
layout: post
title: "Python: List Comprehensions"
date: 2026-01-09
categories: [python]
tags: [fundamentals, syntax]
---

## Overview
Concise way to create lists...

## Basic Syntax
```python
squares = [i**2 for i in range(10)]
```

## Common Use Cases
...
```

### 4. **Diary** (`categories: [diary]`)
- **Purpose**: Daily personal reflections and notes, separate from technical logs
- **Location**: Listed at `/diary/`
- **Naming**: `YYYY-MM-DD-day-###.md`
- **Content**: Personal thoughts, feelings, observations, and daily experiences
- **Template**: `_posts/_TEMPLATE_DIARY.md`

**Example**: `2026-01-09-day-001.md`

```markdown
---
layout: post
title: "Day 1 — Starting Fresh"
date: 2026-01-09
categories: [diary]
tags: []
---

Today I'm starting this journey...

## Today's Reflections
Feeling excited but also a bit nervous...

## Notes
- Remember to stay consistent
- Don't be too hard on yourself
```

### 5. **Projects** (`categories: [projects]`)
- **Purpose**: Document projects you're building
- **Location**: Listed at `/projects/`
- **Naming**: `YYYY-MM-DD-project-name.md`
- **Content**: Project description, progress updates, what you learned

---

## How They Work Together

### Daily Log References Detailed Posts

Your daily log acts as an **index** that links to your detailed content:

```
Day 1 (Log Post)
  ├─→ Two Sum (LeetCode Post)
  └─→ List Comprehensions (Python Post)
```

This way:
- **Log** gives the high-level view of your day
- **LeetCode/Python pages** show all your detailed work in those areas
- Users can navigate from daily summaries to deep dives

---

## Creating New Content

### Daily Log Entry
```bash
cp _posts/_TEMPLATE.md _posts/2026-01-10-day-002.md
# Edit: Add brief summaries + links to detailed posts
```

### LeetCode Solution
```bash
cp _posts/_TEMPLATE_LEETCODE.md _posts/2026-01-10-reverse-linked-list.md
# Edit: Add problem details, solution, analysis
```

### Python Note
```bash
cp _posts/_TEMPLATE_PYTHON.md _posts/2026-01-10-python-decorators.md
# Edit: Add concept explanation, examples
```

---

## Category System

Posts are organized by **categories** (not tags):

| Category | Description | Index Page |
|----------|-------------|------------|
| `log` | Daily journal entries | `/log/` |
| `leetcode` | LeetCode solutions | `/leetcode/` |
| `python` | Python concept notes | `/python/` |
| `diary` | Personal reflections | `/diary/` |
| `projects` | Project documentation | `/projects/` |

**Important**: Use `categories: [leetcode]` not `tags: [leetcode]` for the post to appear on the correct index page.

---

## Workflow Example

### Day 2: Solve "Reverse Linked List" and learn about Python Decorators

1. **Create LeetCode post**:
```bash
cp _posts/_TEMPLATE_LEETCODE.md _posts/2026-01-10-reverse-linked-list.md
```
Edit with problem details, solution, analysis.

2. **Create Python post**:
```bash
cp _posts/_TEMPLATE_PYTHON.md _posts/2026-01-10-python-decorators.md
```
Edit with decorator explanation, examples.

3. **Create daily log**:
```bash
cp _posts/_TEMPLATE.md _posts/2026-01-10-day-002.md
```
Edit with:
```markdown
## LeetCode
Solved **[Reverse Linked List](/2026/01/10/reverse-linked-list/)** (LC #206)

## Python
Studied **[Decorators](/2026/01/10/python-decorators/)** - Functions that modify other functions
```

4. **Result**:
- Home page shows "Day 2" in Recent Updates
- `/log/` lists all daily entries including Day 2
- `/leetcode/` shows "Reverse Linked List" post
- `/python/` shows "Decorators" post
- Day 2 post links to the detailed posts

---

## Benefits of This Structure

1. **Separation of concerns**: Daily logs stay brief, detailed posts stay focused
2. **Better organization**: Easy to find all LeetCode solutions or Python notes
3. **Reusability**: Can reference the same LeetCode solution from multiple daily logs
4. **Scalability**: Hundreds of posts remain manageable
5. **Navigation**: Multiple pathways to find content (by date, by topic, by type)

---

## Quick Reference

| Task | Command |
|------|---------|
| New daily log | `cp _posts/_TEMPLATE.md _posts/YYYY-MM-DD-day-XXX.md` |
| New LeetCode | `cp _posts/_TEMPLATE_LEETCODE.md _posts/YYYY-MM-DD-problem.md` |
| New Python | `cp _posts/_TEMPLATE_PYTHON.md _posts/YYYY-MM-DD-python-topic.md` |
| New diary | `cp _posts/_TEMPLATE_DIARY.md _posts/YYYY-MM-DD-day-XXX.md` |

| Category | Use For | Appears At |
|----------|---------|------------|
| `log` | Daily journals | `/log/` and Home |
| `leetcode` | Problem solutions | `/leetcode/` |
| `python` | Concept deep-dives | `/python/` |
| `diary` | Personal reflections | `/diary/` |
| `projects` | Project docs | `/projects/` |
