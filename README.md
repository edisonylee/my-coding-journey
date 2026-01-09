# My Coding Journey

A minimal, typewriter-inspired Jekyll blog for tracking daily coding progress, LeetCode problems, Python learning, and project work.

## Features

- **Daily Log**: Chronicle your coding journey day by day
- **LeetCode Tracker**: Document problems solved with approaches and solutions
- **Python Notes**: Track concepts and techniques learned
- **Projects**: Showcase work-in-progress and completed projects
- **Minimal Design**: Clean, developer-focused aesthetic with monospace fonts
- **GitHub Pages Ready**: Zero-config deployment

## Local Development

### Prerequisites

- Ruby 2.7+ (check with `ruby -v`)
- Bundler (`gem install bundler`)

### Setup

1. Clone this repository:
```bash
git clone https://github.com/yourusername/blog.git
cd blog
```

2. Install dependencies:
```bash
bundle install
```

3. Run the local server:
```bash
bundle exec jekyll serve
```

4. Open your browser to `http://localhost:4000`

The site will auto-reload when you make changes to files.

## Deployment to GitHub Pages

1. Create a new repository on GitHub named `yourusername.github.io` (or any name for a project site)

2. Push your code:
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/yourusername/blog.git
git push -u origin main
```

3. Enable GitHub Pages:
   - Go to repository **Settings** → **Pages**
   - Under "Source", select **main** branch
   - Click **Save**

4. Your site will be live at `https://yourusername.github.io/` (or `https://yourusername.github.io/blog/` for project sites)

### Configuration

Edit `_config.yml` to customize:
- `title`: Your blog title
- `author`: Your name
- `url`: Your GitHub Pages URL

## Creating Posts

### Daily Log Entry

Create a new file in `_posts/` following this naming convention:
```
_posts/YYYY-MM-DD-day-###.md
```

Example: `_posts/2026-01-10-day-002.md`

**Template**:
```markdown
---
layout: post
title: "Day 2 — [Brief Description]"
date: 2026-01-10
categories: [log]
tags: [leetcode, python, projects]
hours: 3.0
---

## What I Did Today

- Bullet point summary
- Key achievements
- What you learned

## LeetCode

[Problem Name](https://leetcode.com/problems/problem-slug/)

**Approach**: Describe your solution approach

```python
# Your code here
```

**Key insight**: What you learned from this problem

## Python

Notes on Python concepts covered today:
- List important takeaways
- Include code examples

## Projects

(Optional) What you built or worked on

---

*Total coding time: 3.0 hours*
```

### Tagging Guide

Include tags in the frontmatter to organize your posts:

- **Always include**: `categories: [log]` for daily entries
- **Add tags based on content**:
  - `leetcode`: Include when you solve LeetCode problems
  - `python`: Include when you learn Python concepts
  - `projects`: Include when you work on projects

Posts will automatically appear in the corresponding index pages (`/leetcode/`, `/python/`, `/projects/`) based on their tags.

## File Structure

```
blog/
├── _config.yml           # Site configuration
├── _layouts/             # Page templates
│   ├── default.html      # Base layout with navigation
│   ├── page.html         # Static page layout
│   └── post.html         # Blog post layout
├── _posts/               # Blog posts (daily entries)
│   └── 2026-01-09-day-001.md
├── assets/
│   └── css/
│       └── style.css     # All styling
├── index.html            # Home page
├── log.html              # Daily log index
├── leetcode.html         # LeetCode index
├── python.html           # Python index
├── projects.html         # Projects index
├── about.md              # About page
├── Gemfile               # Ruby dependencies
└── README.md             # This file
```

## Customization

### Colors & Typography

Edit CSS variables in `assets/css/style.css`:

```css
:root {
  --color-bg: #fafafa;
  --color-text: #2a2a2a;
  --color-accent: #0066cc;
  --font-mono: 'SF Mono', Monaco, Courier, monospace;
  --font-sans: -apple-system, BlinkMacSystemFont, sans-serif;
}
```

### Navigation

Add or remove navigation items in `_layouts/default.html` (`.nav-links` section).

### About Page

Edit `about.md` to add your personal information, bio, and contact details.

## Tips

- Write posts consistently to build momentum
- Use descriptive titles for easy scanning
- Include hours to track time investment
- Link to LeetCode problems for future reference
- Tag posts accurately for proper categorization
- Keep the style minimal and focused on content

## License

MIT License - feel free to use this as a template for your own coding journey!

---

Built with Jekyll • Hosted on GitHub Pages • Inspired by Daktilo
