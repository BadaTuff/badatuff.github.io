# Content Guide for BTuff Security

Quick reference for adding new weekly letters and Off the Clock posts.

## Adding a New Weekly Letter

1. **Create a new file** in `docs/_letters/` following this naming pattern:
   ```
   docs/_letters/week-02.md
   docs/_letters/week-03.md
   ```

2. **Use this frontmatter** (copy and adjust nav_order):
   ```yaml
   ---
   layout: default
   title: "Week XX - Your Title Here"
   parent: Weekly Letters
   nav_order: X  # Use sequential numbers: 1, 2, 3, etc. (newest = highest number)
   ---
   ```

3. **Add header image** (optional):
   ```markdown
   <img src="/BTuff-Security/assets/images/your-image.jpg" alt="Description" style="width: 100%; max-width: 800px; display: block; margin: 20px auto;">
   ```

4. **Write your content** following the Week 01 structure as a template

5. **Save images** to `docs/assets/images/` first

## Adding a New "Off the Clock" Post

1. **Create a new file** in `docs/_offclock/` with sequential numbering:
   ```
   docs/_offclock/003-your-post-title.md
   docs/_offclock/004-another-post.md
   ```

2. **Use this frontmatter**:
   ```yaml
   ---
   layout: default
   title: "Your Post Title"
   parent: Off the Clock
   nav_order: X  # Use sequential numbers (newest = highest)
   ---
   ```

3. **Write your content** - these are unstructured, authentic posts

## Navigation Order

- **nav_order** determines sidebar position
- Higher numbers = newer posts (appear first due to reverse sorting in _config.yml)
- Week 01 = nav_order: 1, Week 02 = nav_order: 2, etc.

## Important Rules

### DO:
✅ Always set `parent: Weekly Letters` or `parent: Off the Clock`
✅ Use unique `nav_order` numbers
✅ Save images to `docs/assets/images/` before referencing them
✅ Use `/BTuff-Security/` prefix for all image paths
✅ Test locally before pushing (optional but recommended)

### DON'T:
❌ Don't add `permalink` to child posts (Just the Docs handles this)
❌ Don't skip `parent` field (breaks sidebar navigation)
❌ Don't use duplicate `nav_order` numbers
❌ Don't reference images that don't exist yet

## Quick Template - Weekly Letter

```markdown
---
layout: default
title: "Week XX - Title"
parent: Weekly Letters
nav_order: X
---

# Week XX: Title

<img src="/BTuff-Security/assets/images/image-name.jpg" alt="Alt text" style="width: 100%; max-width: 800px; display: block; margin: 20px auto;">

[Your intro paragraph]

---

## 🔵 BLUE TEAM

[Content]

---

## 🔴 RED TEAM

[Content]

---

## WRAP-UP

[Content]
```

## Quick Template - Off the Clock

```markdown
---
layout: default
title: "Your Post Title"
parent: Off the Clock
nav_order: X
---

# Your Post Title

<img src="/BTuff-Security/assets/images/image.jpg" alt="Description" style="width: 100%; max-width: 800px; display: block; margin: 20px auto;">

[Your authentic, unstructured content]

---

[Closing thoughts]
```

## Testing Locally (Optional)

```bash
cd docs
bundle install
bundle exec jekyll serve
# Visit http://localhost:4000/BTuff-Security/
```

## Committing Changes

```bash
git add .
git commit -m "Add Week XX letter"
git push
```

GitHub Pages will rebuild automatically (takes ~2-3 minutes).

---

**Need help?** Check the existing posts in `docs/_letters/` and `docs/_offclock/` for examples.
