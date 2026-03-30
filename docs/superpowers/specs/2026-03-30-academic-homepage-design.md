# Yi Xie Academic Homepage - Design Spec

## Overview

Build a personal academic homepage for Yi Xie (Ph.D. Student, University of Arizona) using the [acad-homepage](https://github.com/RayeRen/acad-homepage.github.io) Jekyll template, deployed on GitHub Pages at `yydc1.github.io`.

## Approach

Fork the `RayeRen/acad-homepage.github.io` template and customize content. This is the same template used by the reference site (andrewzhou924.github.io).

## Deployment

- Platform: GitHub Pages
- Repository: `yydc1/yydc1.github.io`
- URL: `https://yydc1.github.io`
- Build: Jekyll (GitHub Pages native support, auto-builds on push)

## Page Sections

### 1. Header / About (Hero)

- **Photo:** Placeholder image initially, user replaces later
- **Name:** Yi Xie
- **Title:** Ph.D. Student, Computer Science & Engineering
- **Affiliation:** University of Arizona
- **Contact links:** Email (yydc1@outlook.com), GitHub (yydc1), Google Scholar
- **Bio paragraph:** 1-2 paragraphs covering:
  - Current PhD student at UofA advised by Bo Liu
  - Research focus: multi-agent LLM reasoning & post-training, reliable reasoning evaluation, code reasoning
  - Previously MS at Fudan University, BS at BUCT

### 2. News

Timeline format, 3-5 recent items:

- [2026] SAT paper accepted at AAMAS 2026
- [2025] Paper "From Debate to Equilibrium" accepted at ICML 2025
- [2025] Started Ph.D. at University of Arizona
- [2025] Two papers accepted at AAMAS 2025

### 3. Education

Three entries in reverse chronological order:

| Institution | Degree | Period |
|---|---|---|
| University of Arizona | Ph.D., Computer Science & Engineering | Sep 2025 - Present |
| Fudan University | M.S., Mechanical & Electrical Engineering | Sep 2022 - Jun 2025 |
| Beijing University of Chemical Technology | B.S., Mechanical & Electrical Engineering; B.S., Economic Management (Dual) | Sep 2017 - Jun 2022 |

### 4. Selected Publications

Two groups, each paper with: title, authors (Yi Xie bolded), venue, and links (PDF/Code when available). Placeholder thumbnail images.

**Group A: LLM Reasoning & Multi-Agent LLMs**

1. **SAT: Sequential Agent Tuning for Coordinator-Free Plug-and-Play Multi-LLM Training with Monotonic Improvement Guarantees**
   - **Yi Xie**, Yangyang Xu, Fan Yi, Bo Liu
   - AAMAS 2026 (accepted)

2. **From Debate to Equilibrium: Belief-Driven Multi-Agent LLM Reasoning via Bayesian Nash Equilibrium**
   - **Yi Xie**, Zhanke Zhou, Chentao Cao, Qiyu Niu, Tongliang Liu, Bo Han
   - ICML 2025 (accepted)

**Group B: Multi-Agent RL & Robotics**

3. **ACORN: Acyclic Coordination with Reachability Network to Reduce Communication Redundancy in Multi-Agent Systems**
   - **Yi Xie**, Ziqing Zhou, Chun Ouyang, Siao Liu, Zhile Zhao, Zhongxue Gan
   - AAMAS 2025

4. **Heuristics-Assisted Experience Replay Strategy for Cooperative Multi-Agent Reinforcement Learning**
   - **Yi Xie**, Ziqing Zhou, Chun Ouyang, Siao Liu, Zhile Zhao, Zhongxue Gan
   - AAMAS 2025

5. **Improving Robotic Grasp Detection Under Sparse Annotations via Grasp Transformer with Pixel-Wise Contrastive Learning**
   - Siao Liu, Yang Liu, Zhaoyu Chen, Ziqing Zhou, Zhile Zhao, **Yi Xie**, Wei Li, Zhongxue Gan
   - IEEE Transactions on Industrial Electronics, 2025

6. **A Framework for Dynamical Distributed Flocking Control in Dense Environments**
   - Ziqing Zhou, Chun Ouyang, Linqiang Hu, **Yi Xie**, Yuning Chen, Zhongxue Gan
   - Expert Systems with Applications, 2023

7. **Improving Generalization in Visual Reinforcement Learning via Conflict-aware Gradient Agreement Augmentation**
   - Siao Liu, Zhaoyu Chen, Yang Liu, Yuzheng Wang, Dingkang Yang, Zhile Zhao, Ziqing Zhou, **Yi Xie**, Wei Li, Wenqiang Zhang, Zhongxue Gan
   - ICCV 2023

### 5. Academic Service

- Reviewer: NeurIPS 2024; ICLR 2025, 2026; ICML 2025, 2026; COLM 2025

### 6. Navigation Bar

Anchors: About | Publications | Service

## Configuration Details

### _config.yml changes

- `title`: Yi Xie
- `description`: Yi Xie's Academic Homepage
- `repository`: yydc1/yydc1.github.io
- `author.name`: Yi Xie
- `author.bio`: Ph.D. Student at University of Arizona
- `author.location`: Tucson, AZ
- `author.email`: yydc1@outlook.com
- `author.uri`: https://yydc1.github.io
- `author.github`: yydc1
- `author.google_scholar`: (user to provide Google Scholar ID)
- `google_scholar_stats_use_cdn`: true

### Google Scholar Citation Crawler

Configure the GitHub Actions workflow (already included in template) with the user's Google Scholar author ID. This auto-updates citation counts.

## Out of Scope

- Research Experience detailed page (covered by CV)
- Talks / Teaching sections (no data in CV)
- Dark mode
- Multi-language support
- Custom domain
- Paper thumbnail images (placeholder only)

## Implementation Steps (High Level)

1. Clone/fork the acad-homepage template repo
2. Rename to `yydc1.github.io`
3. Update `_config.yml` with personal info
4. Edit `_pages/about.md` with all section content
5. Add placeholder avatar image
6. Configure Google Scholar crawler (if Scholar ID available)
7. Push to GitHub, verify deployment
8. Test responsive layout
