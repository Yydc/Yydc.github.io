# Yi Xie Academic Homepage Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build and deploy Yi Xie's personal academic homepage at yydc1.github.io using the acad-homepage Jekyll template.

**Architecture:** Clone the RayeRen/acad-homepage.github.io template into the local working directory (`/Users/apple/Downloads/homepage`), customize configuration and content files, then push to a new GitHub repo `yydc1/yydc1.github.io` for GitHub Pages deployment.

**Tech Stack:** Jekyll, GitHub Pages, HTML/Markdown, YAML, GitHub Actions (for Google Scholar citation crawler)

---

## File Structure

All work happens inside `/Users/apple/Downloads/homepage`. After cloning the template, these are the files we create or modify:

| Action | File | Responsibility |
|--------|------|----------------|
| Modify | `_config.yml` | Site metadata, author info, social links |
| Modify | `_pages/about.md` | All page content (bio, news, publications, education, service) |
| Modify | `_data/navigation.yml` | Navigation bar links |
| Add | `images/avatar.png` | Placeholder avatar image |
| Modify | `google_scholar_crawler/main.py` | Google Scholar author ID (deferred until user provides ID) |

---

### Task 1: Clone Template and Initialize Git Repo

**Files:**
- All files from `RayeRen/acad-homepage.github.io` cloned into `/Users/apple/Downloads/homepage`

- [ ] **Step 1: Clone the acad-homepage template into the working directory**

```bash
cd /Users/apple/Downloads/homepage
# Clone into a temp dir then move contents (directory already has docs/)
git clone https://github.com/RayeRen/acad-homepage.github.io.git _template
# Move all template files (including hidden .git would be replaced)
shopt -s dotglob
mv _template/* . 2>/dev/null || true
mv _template/.gitignore . 2>/dev/null || true
rm -rf _template
```

- [ ] **Step 2: Re-initialize as a fresh git repo for the user's site**

```bash
cd /Users/apple/Downloads/homepage
rm -rf .git
git init
git add -A
git commit -m "chore: initialize from acad-homepage template"
```

- [ ] **Step 3: Verify template files are in place**

```bash
ls _config.yml _pages/about.md _data/navigation.yml images/
```

Expected: All four paths exist.

---

### Task 2: Configure `_config.yml` with Personal Info

**Files:**
- Modify: `_config.yml`

- [ ] **Step 1: Update site settings**

Replace in `_config.yml`:

```yaml
# Site Settings
title                    : "Yi Xie"
description              : "Yi Xie's Academic Homepage - Ph.D. Student at University of Arizona"
repository               : "yydc1/yydc1.github.io"
google_scholar_stats_use_cdn : true
```

- [ ] **Step 2: Update author section**

Replace the entire `author:` block in `_config.yml`:

```yaml
# Site Author
author:
  name             : "Yi Xie"
  avatar           : "images/avatar.png"
  bio              : "Ph.D. Student at University of Arizona"
  location         : "Tucson, AZ"
  employer         :
  pubmed           :
  googlescholar    : "https://scholar.google.com/citations?user=PLACEHOLDER_ID"
  email            : "yydc1@outlook.com"
  researchgate     :
  uri              : "https://yydc1.github.io"
  bitbucket        :
  codepen          :
  dribbble         :
  flickr           :
  facebook         :
  foursquare       :
  github           : "yydc1"
  google_plus      :
  keybase          :
  instagram        :
  impactstory      :
  lastfm           :
  linkedin         :
  dblp             :
  orcid            :
  pinterest        :
  soundcloud       :
  stackoverflow    :
  steam            :
  tumblr           :
  twitter          :
  vine             :
  weibo            :
  xing             :
  youtube          :
  wikipedia        :
```

- [ ] **Step 3: Update timezone**

Replace timezone line:

```yaml
timezone: America/Phoenix
```

- [ ] **Step 4: Commit**

```bash
cd /Users/apple/Downloads/homepage
git add _config.yml
git commit -m "feat: configure site with Yi Xie's personal info"
```

---

### Task 3: Update Navigation Bar

**Files:**
- Modify: `_data/navigation.yml`

- [ ] **Step 1: Replace navigation.yml contents**

Write the following to `_data/navigation.yml`:

```yaml
# main links
main:
  - title: "About Me"
    url: "/#about-me"

  - title: "News"
    url: "/#-news"

  - title: "Publications"
    url: "/#-publications"

  - title: "Education"
    url: "/#-education"

  - title: "Service"
    url: "/#-service"
```

- [ ] **Step 2: Commit**

```bash
cd /Users/apple/Downloads/homepage
git add _data/navigation.yml
git commit -m "feat: update navigation bar to match site sections"
```

---

### Task 4: Add Placeholder Avatar Image

**Files:**
- Add: `images/avatar.png`

- [ ] **Step 1: Generate a simple placeholder avatar**

```bash
cd /Users/apple/Downloads/homepage
# Create a simple 512x512 placeholder PNG using Python
python3 -c "
from PIL import Image, ImageDraw, ImageFont
img = Image.new('RGB', (512, 512), color=(200, 200, 200))
draw = ImageDraw.Draw(img)
# Draw initials
try:
    font = ImageFont.truetype('/System/Library/Fonts/Helvetica.ttc', 120)
except:
    font = ImageFont.load_default()
text = 'YX'
bbox = draw.textbbox((0, 0), text, font=font)
w = bbox[2] - bbox[0]
h = bbox[3] - bbox[1]
draw.text(((512-w)/2, (512-h)/2 - 20), text, fill=(100, 100, 100), font=font)
img.save('images/avatar.png')
print('avatar.png created')
"
```

If PIL is not available, fall back to copying the existing template placeholder:

```bash
# The template already has images/android-chrome-512x512.png
# If PIL fails, just use that as the avatar
cp images/android-chrome-512x512.png images/avatar.png 2>/dev/null || echo "Using template default"
```

- [ ] **Step 2: Commit**

```bash
cd /Users/apple/Downloads/homepage
git add images/avatar.png
git commit -m "feat: add placeholder avatar image"
```

---

### Task 5: Write Main Page Content (`_pages/about.md`)

**Files:**
- Modify: `_pages/about.md`

This is the core task. Replace the entire content of `_pages/about.md` with all sections.

- [ ] **Step 1: Write the complete about.md**

Replace the entire contents of `_pages/about.md` with:

```markdown
---
permalink: /
title: ""
excerpt: ""
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

{% if site.google_scholar_stats_use_cdn %}
{% assign gsDataBaseUrl = "https://cdn.jsdelivr.net/gh/" | append: site.repository | append: "@" %}
{% else %}
{% assign gsDataBaseUrl = "https://raw.githubusercontent.com/" | append: site.repository | append: "/" %}
{% endif %}
{% assign url = gsDataBaseUrl | append: "google-scholar-stats/gs_data_shieldsio.json" %}

<span class='anchor' id='about-me'></span>

I am Yi Xie, a Ph.D. student in Computer Science & Engineering at the [University of Arizona](https://www.arizona.edu/), advised by [Prof. Bo Liu](https://liubo-lab.github.io/). Previously, I received my M.S. from [Fudan University](https://www.fudan.edu.cn/en/) (advised by Prof. Zhongxue Gan) and dual B.S. degrees from [Beijing University of Chemical Technology](https://www.buct.edu.cn/).

My research focuses on:
- **Multi-agent LLM reasoning and post-training** (RL, trust regions, theoretical guarantees)
- **Reliable reasoning evaluation:** math / planning / active reasoning benchmarks
- **Code reasoning:** traceable multi-turn debugging and decoding control


# 🔥 News
- *2026.01*: &nbsp;🎉 Our paper "SAT: Sequential Agent Tuning" is accepted at **AAMAS 2026**!
- *2025.09*: &nbsp;🎉 Started my Ph.D. at the University of Arizona!
- *2025.05*: &nbsp;🎉 Our paper "From Debate to Equilibrium" is accepted at **ICML 2025**!
- *2025.01*: &nbsp;🎉 Two papers accepted at **AAMAS 2025**!


# 📝 Publications

## LLM Reasoning & Multi-Agent LLMs

<div class='paper-box'><div class='paper-box-image'><div><div class="badge">AAMAS 2026</div><img src='images/500x300.png' alt="sym" width="100%"></div></div>
<div class='paper-box-text' markdown="1">

**SAT: Sequential Agent Tuning for Coordinator-Free Plug-and-Play Multi-LLM Training with Monotonic Improvement Guarantees**

**Yi Xie**, Yangyang Xu, Fan Yi, Bo Liu

AAMAS 2026 (accepted)

</div>
</div>

<div class='paper-box'><div class='paper-box-image'><div><div class="badge">ICML 2025</div><img src='images/500x300.png' alt="sym" width="100%"></div></div>
<div class='paper-box-text' markdown="1">

**From Debate to Equilibrium: Belief-Driven Multi-Agent LLM Reasoning via Bayesian Nash Equilibrium**

**Yi Xie**, Zhanke Zhou, Chentao Cao, Qiyu Niu, Tongliang Liu, Bo Han

ICML 2025 (accepted)

</div>
</div>

## Multi-Agent RL & Robotics

<div class='paper-box'><div class='paper-box-image'><div><div class="badge">AAMAS 2025</div><img src='images/500x300.png' alt="sym" width="100%"></div></div>
<div class='paper-box-text' markdown="1">

**ACORN: Acyclic Coordination with Reachability Network to Reduce Communication Redundancy in Multi-Agent Systems**

**Yi Xie**, Ziqing Zhou, Chun Ouyang, Siao Liu, Zhile Zhao, Zhongxue Gan

AAMAS 2025

</div>
</div>

<div class='paper-box'><div class='paper-box-image'><div><div class="badge">AAMAS 2025</div><img src='images/500x300.png' alt="sym" width="100%"></div></div>
<div class='paper-box-text' markdown="1">

**Heuristics-Assisted Experience Replay Strategy for Cooperative Multi-Agent Reinforcement Learning**

**Yi Xie**, Ziqing Zhou, Chun Ouyang, Siao Liu, Zhile Zhao, Zhongxue Gan

AAMAS 2025

</div>
</div>

- **Improving Robotic Grasp Detection Under Sparse Annotations via Grasp Transformer with Pixel-Wise Contrastive Learning**, Siao Liu, Yang Liu, Zhaoyu Chen, Ziqing Zhou, Zhile Zhao, **Yi Xie**, Wei Li, Zhongxue Gan. *IEEE Transactions on Industrial Electronics, 2025*

- **A Framework for Dynamical Distributed Flocking Control in Dense Environments**, Ziqing Zhou, Chun Ouyang, Linqiang Hu, **Yi Xie**, Yuning Chen, Zhongxue Gan. *Expert Systems with Applications, 2023*

- **Improving Generalization in Visual Reinforcement Learning via Conflict-aware Gradient Agreement Augmentation**, Siao Liu, Zhaoyu Chen, Yang Liu, Yuzheng Wang, Dingkang Yang, Zhile Zhao, Ziqing Zhou, **Yi Xie**, Wei Li, Wenqiang Zhang, Zhongxue Gan. *ICCV 2023*


# 📖 Education
- *2025.09 - present*, Ph.D. Student in Computer Science & Engineering, University of Arizona. Advisor: [Bo Liu](https://liubo-lab.github.io/).
- *2022.09 - 2025.06*, M.S. in Mechanical & Electrical Engineering, Fudan University. Advisor: Zhongxue Gan.
- *2017.09 - 2022.06*, B.S. in Mechanical & Electrical Engineering & B.S. in Economic Management (Dual Degree), Beijing University of Chemical Technology.


# 💻 Service
- **Reviewer:** NeurIPS 2024; ICLR 2025, 2026; ICML 2025, 2026; COLM 2025
```

- [ ] **Step 2: Verify the file was written correctly**

```bash
head -5 /Users/apple/Downloads/homepage/_pages/about.md
wc -l /Users/apple/Downloads/homepage/_pages/about.md
```

Expected: First line is `---`, file is approximately 100-120 lines.

- [ ] **Step 3: Commit**

```bash
cd /Users/apple/Downloads/homepage
git add _pages/about.md
git commit -m "feat: add Yi Xie's academic content to homepage"
```

---

### Task 6: Create GitHub Repo and Push

**Files:**
- No file changes, git operations only

- [ ] **Step 1: Create the GitHub repository**

```bash
cd /Users/apple/Downloads/homepage
gh repo create yydc1/yydc1.github.io --public --source=. --description "Yi Xie's Academic Homepage"
```

If `gh` is not authenticated or available, do it manually:

```bash
cd /Users/apple/Downloads/homepage
git remote add origin https://github.com/yydc1/yydc1.github.io.git
git branch -M main
git push -u origin main
```

Note: The user will need to authenticate with GitHub. The user previously shared a PAT (which should be revoked). They will need a fresh token or SSH key.

- [ ] **Step 2: Push all commits**

```bash
cd /Users/apple/Downloads/homepage
git push -u origin main
```

- [ ] **Step 3: Verify GitHub Pages is enabled**

After push, GitHub Pages should auto-detect the Jekyll site. Verify by:

```bash
gh repo view yydc1/yydc1.github.io --web
```

Or navigate to `https://yydc1.github.io` in a browser (may take 1-2 minutes for first build).

---

### Task 7: Verify Deployment and Test

**Files:**
- No file changes

- [ ] **Step 1: Wait for GitHub Pages build**

```bash
# Check GitHub Actions build status
gh run list --repo yydc1/yydc1.github.io --limit 3
```

Expected: A "pages build and deployment" workflow run in progress or completed.

- [ ] **Step 2: Verify the live site**

Open `https://yydc1.github.io` in a browser and verify:
- Avatar and name display correctly in sidebar
- Bio text renders properly
- News section shows 4 items
- Publications section shows both groups with paper boxes
- Education section shows 3 entries
- Service section shows reviewer list
- Navigation bar links scroll to correct sections

- [ ] **Step 3: Check responsive layout**

Test the site at mobile width (375px) to verify it's responsive. The acad-homepage template handles this by default.

---

## Deferred Tasks (User Action Required)

These tasks cannot be completed now and require user input later:

1. **Replace avatar image:** User provides a personal photo, save as `images/avatar.png` (square, at least 512x512px recommended), commit and push.

2. **Google Scholar integration:** User provides their Google Scholar author ID. Update `_config.yml` field `author.googlescholar` with the real URL, and update `google_scholar_crawler/main.py` with the author ID. The GitHub Actions workflow will auto-update citation counts.

3. **Add paper links:** As paper PDFs and code repos become available, add `[[paper]](url)` and `[[code]](url)` links to each publication entry in `_pages/about.md`.

4. **Add paper thumbnail images:** Replace `images/500x300.png` placeholders with actual paper figure thumbnails saved to `images/` directory.
