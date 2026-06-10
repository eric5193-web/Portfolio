# Portfolio Site Design — Poyuan (Eric) Wang
**Date:** 2026-06-10
**Purpose:** NYU Integrated Marketing internship final portfolio submission

---

## Overview

A single-page, scroll-based personal portfolio site built in pure HTML/CSS/JS. Deployed to GitHub Pages for a public URL to submit to NYU. Dark & modern aesthetic with electric blue (#2B00FF) accent pulled from silueta.ai's brand identity.

---

## Requirements Coverage

**Part A (5/5):** Personal statement · Short bio · Skills · Accomplishments · Contact
**Part B (5–6/8):** Internship work samples · Past job/media work · Course projects · Visual presentations · Art/Media

---

## Site Sections

### 1. Hero
- Full-viewport dark panel
- Professional headshot (right), name + title (left)
- Name: POYUAN (ERIC) WANG
- Title: Marketing Analytics & Brand Strategy | NYU Integrated Marketing | silueta.ai
- Subtle fade-in on load

### 2. About
- Third-person bio (155 words, approved):
  > Poyuan (Eric) Wang is an NYU Integrated Marketing graduate student specializing in marketing analytics and AI-augmented brand strategy. Originally trained as a professional dancer — earning a full scholarship BFA in Classical Chinese Dance and performing before 1M+ live audiences annually with Shen Yun Performing Arts across five continents — Eric brings a rare combination of creative instinct and analytical precision to modern marketing.
  >
  > He compresses what once required an entire team — research, targeting, creative production, automation — into a single AI-augmented workflow, delivering faster iteration and data-informed decisions without sacrificing creative quality. His work spans social media growth, direct marketing ROI modeling, competitive media planning, and creator brand strategy.
  >
  > Currently interning at silueta.ai as a Creator Brand & Social Media Marketing Intern, Eric is building the brand's content pipeline and creator outreach infrastructure from the ground up for a fast-paced startup launch.
- Right side: stat strip — `1M+ live audiences · 2 brand campaigns · 2 course projects`

### 3. Skills
Tag grid (in order):
SQL · Google Ads · Meta Ads Manager · GA4 · Tableau · Canva · CapCut · Excel/MegaStat · Chinese (Native) · English (Fluent)

### 4. Internship: silueta.ai *(Part B — primary work samples)*
- Left column: role title, company description, bullet points of work done (AI content pipeline, creator research/outreach)
- Right column: 2×2 grid of Instagram post screenshots from the silueta_ai account
- Source images: user-provided screenshots

### 5. Course Projects *(Part B — project work + visual presentations)*
Two cards side by side:
- **Mercedes-Benz GLC Campaign**
  - Opens vibe-coded landing page: `/Users/wangbo/Desktop/NYU/Second semaster/Campaign 2/MB Final Presentation/Landing page_dark.html`
  - Links to PDF deck: `MercedesBenz_Campaign_Final.pdf`
- **Applebee's RFM Analysis**
  - Description: RFM segmentation, data visualization, 6-KPI dashboard
  - Links to PDF deck: `Applebees_Finalppt_EricWang.pptx.pdf`

### 6. Media & Campaigns *(Part B — Art/Media)*
Two embedded YouTube players:
- Volkswagen Commercial Vehicles Campaign: https://youtu.be/06l52ERbgaE?si=wzY_70_k2Qn7kWcg
- Chang Hwa Commercial Bank Visual Campaign: https://youtu.be/qjB16vRecDs?si=bhvs0YNfFqGTOzkm

### 7. Contact
- Email: pw2591@nyu.edu
- LinkedIn: linkedin.com/in/poyuan-wang-393751360

---

## Design System

| Token | Value |
|---|---|
| Background | #0a0a0a |
| Surface | #111111 |
| Border | #1e1e1e |
| Accent | #2B00FF |
| Accent hover | #4422FF |
| Text primary | #f0f0f0 |
| Text secondary | #888888 |
| Font | Inter, system-ui, sans-serif |

- Smooth scroll behavior
- Fade-in on scroll (IntersectionObserver)
- Hover lift effect on cards
- Responsive: mobile-first, single column on small screens

---

## Tech Stack

- **Build:** Pure HTML/CSS/JS — single `index.html`
- **Assets:** PDF files and images copied into `/assets/` folder
- **Deploy:** GitHub Pages — public URL format: `https://<username>.github.io/portfolio`

---

## File Structure

```
portfolio/
├── index.html
├── assets/
│   ├── eric-headshot.jpg
│   ├── silueta-post-1.jpg
│   ├── silueta-post-2.jpg
│   ├── silueta-post-3.jpg
│   ├── silueta-post-4.jpg
│   ├── mb-deck.pdf
│   └── applebees-deck.pdf
└── docs/
    └── superpowers/
        └── specs/
            └── 2026-06-10-portfolio-design.md
```
