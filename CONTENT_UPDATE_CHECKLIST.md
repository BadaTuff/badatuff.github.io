# Content Update Checklist

This checklist ensures all necessary files are updated when publishing new content.

---

## 📘 Publishing a New Weekly Letter (Week XX)

### 1. Create New Letter File
- [ ] Create `docs/letters/week-XX.md`
  - [ ] Add YAML front matter:
    ```yaml
    layout: default
    title: "Week XX - [Title]"
    parent: Weekly Letters
    nav_order: XX
    ```
  - [ ] Write content following the established format
  - [ ] Add hero image if needed: `<img src="/assets/images/filename.png" alt="..." style="width: 100%; max-width: 800px; display: block; margin: 20px auto;">`
  - [ ] Include wrap-up section
  - [ ] Add YouTube video embed OR "Video coming soon!" note

### 2. Add Required Images
- [ ] Upload any new images to `docs/assets/images/`
- [ ] Reference them correctly in the markdown with proper paths

### 3. Update Letters Index Page
- [ ] Edit `docs/letters/index.md`
  - [ ] Update "Latest Letter" section (lines ~26-40):
    - Update title to Week XX
    - Update description
    - Update topics covered list
    - Update link to new week
  - [ ] Move previous "Latest Letter" to "Previous Letters" section
  - [ ] Add horizontal divider (`---`) between entries in Previous Letters

### 4. Update Home Page
- [ ] Edit `docs/index.md`
  - [ ] Update "Latest Weekly Letter" section (lines ~26-38):
    - Update title to Week XX
    - Update description
    - Update topics covered list
    - Update link to new week
  - [ ] Update bottom CTA link (line ~115):
    - Change from previous week to new Week XX

### 5. Commit and Push
- [ ] Run `git add` for all changed files
- [ ] Commit with message: `"Add Week XX letter on [topic]"`
- [ ] Commit update to home page: `"Update home page to feature Week XX as latest letter"`
- [ ] Push to GitHub: `git push origin main`

---

## 🌱 Publishing a New Off the Clock Post

### 1. Create New Post File
- [ ] Create `docs/offclock/XXX-title.md` (use 3-digit number, e.g., 003-topic.md)
  - [ ] Add YAML front matter:
    ```yaml
    layout: default
    title: "[Post Title]"
    parent: Off the Clock
    nav_order: XXX
    ```
  - [ ] Write content in authentic, conversational style
  - [ ] No required format - write what feels right

### 2. Create Mirror File (if needed)
- [ ] Create identical file in `docs/_offclock/XXX-title.md`
  - [ ] Same content and front matter as main file

### 3. Add Required Images
- [ ] Upload any images to `docs/assets/images/`
- [ ] Reference them correctly in markdown

### 4. Update Home Page
- [ ] Edit `docs/index.md`
  - [ ] Update "Latest Off the Clock" section (lines ~44-50):
    - Update post title
    - Update description/excerpt
    - Update link to new post
  - [ ] Previous post is automatically archived (no manual movement needed)

### 5. Verify Auto-Update
- [ ] Confirm `docs/offclock/index.md` auto-updates via Jekyll (it should - uses dynamic sorting)
- [ ] No manual changes needed to offclock/index.md

### 6. Commit and Push
- [ ] Run `git add` for all changed files
- [ ] Commit with message: `"Add off the clock post: [title]"`
- [ ] Commit home page update: `"Update home page with latest off the clock post"`
- [ ] Push to GitHub: `git push origin main`

---

## 📋 Quick Reference: Files to Update

### Weekly Letter Publication:
1. ✅ `docs/letters/week-XX.md` (create)
2. ✅ `docs/assets/images/` (add images if needed)
3. ✅ `docs/letters/index.md` (update latest + previous)
4. ✅ `docs/index.md` (update latest weekly letter + bottom CTA)

### Off the Clock Publication:
1. ✅ `docs/offclock/XXX-title.md` (create)
2. ✅ `docs/_offclock/XXX-title.md` (create mirror)
3. ✅ `docs/assets/images/` (add images if needed)
4. ✅ `docs/index.md` (update latest off the clock)

---

## 🔍 Verification Steps

Before pushing, verify:
- [ ] All links work (use correct Jekyll syntax: `{{ site.baseurl }}{% link path/to/file.md %}`)
- [ ] Images load correctly
- [ ] YAML front matter is formatted correctly
- [ ] nav_order increments properly
- [ ] No typos in titles or descriptions
- [ ] Git status shows only intended changes
- [ ] Commit messages follow existing style

---

## 💡 Pro Tips

- **Weekly Letters**: Follow the established structure from previous weeks
- **Off the Clock**: No strict format - be authentic
- **Images**: Use descriptive filenames (e.g., `week03-phishing.png` not `image1.png`)
- **Commits**: Make separate commits for content creation vs. index updates
- **Testing**: Check the live site after pushing to confirm everything renders correctly

---

*Last updated: Week 03 - December 2024*
