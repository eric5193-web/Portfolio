# Portfolio Site Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single-file dark portfolio site for Poyuan (Eric) Wang and deploy it to GitHub Pages for a public URL.

**Architecture:** One `index.html` with all CSS embedded in `<style>` and all JS embedded in `<script>`. No build tools, no dependencies except a Google Fonts CDN link. Scroll-driven fade-in via IntersectionObserver. All assets (images, PDFs) are already in `assets/`.

**Tech Stack:** HTML5, CSS (custom properties, grid, flexbox), vanilla JS (IntersectionObserver). Deployed via GitHub Pages.

---

## File Map

| File | Action | Responsibility |
|---|---|---|
| `index.html` | Create | Entire site — all sections, CSS, JS |
| `assets/` | Already populated | Images, PDFs, MB landing page |

---

### Task 1: HTML Scaffold + Design System + Nav

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create the HTML shell with CSS variables and nav**

Create `/Users/wangbo/Desktop/portfolio/index.html` with this exact content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Poyuan (Eric) Wang — Portfolio</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:ital,wght@0,300;0,400;0,500;0,600;0,700;1,400&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg:           #0a0a0a;
      --surface:      #111111;
      --surface-2:    #161616;
      --border:       #1e1e1e;
      --accent:       #2B00FF;
      --accent-hover: #4d2dff;
      --text:         #f0f0f0;
      --text-muted:   #888888;
      --font:         'Inter', system-ui, sans-serif;
      --max-w:        1100px;
      --section-pad:  100px 24px;
    }
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--font);
      line-height: 1.6;
      -webkit-font-smoothing: antialiased;
    }
    a { color: inherit; text-decoration: none; }
    img { display: block; max-width: 100%; }

    /* ── Nav ───────────────────────────────────────── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 20px 40px;
      background: rgba(10,10,10,0.85);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
    }
    nav .logo {
      font-size: 14px;
      font-weight: 600;
      letter-spacing: 0.1em;
      text-transform: uppercase;
    }
    nav ul {
      list-style: none;
      display: flex;
      gap: 32px;
    }
    nav ul a {
      font-size: 13px;
      color: var(--text-muted);
      transition: color 0.2s;
      letter-spacing: 0.04em;
    }
    nav ul a:hover { color: var(--text); }

    /* ── Reveal animation ──────────────────────────── */
    .reveal {
      opacity: 0;
      transform: translateY(28px);
      transition: opacity 0.6s ease, transform 0.6s ease;
    }
    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }
  </style>
</head>
<body>

  <nav>
    <span class="logo">Eric Wang</span>
    <ul>
      <li><a href="#about">About</a></li>
      <li><a href="#internship">Internship</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#media">Media</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>

  <!-- sections go here -->

  <script>
    // Scroll reveal
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(e => {
        if (e.isIntersecting) {
          e.target.classList.add('visible');
          observer.unobserve(e.target);
        }
      });
    }, { threshold: 0.1 });
    document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
  </script>

</body>
</html>
```

- [ ] **Step 2: Open in browser to verify**

Run: `open /Users/wangbo/Desktop/portfolio/index.html`

Expected: Black page, fixed nav bar at top with logo "Eric Wang" and nav links.

- [ ] **Step 3: Commit**

```bash
cd /Users/wangbo/Desktop/portfolio
git add index.html
git commit -m "feat: scaffold HTML, design system, nav"
```

---

### Task 2: Hero Section

**Files:**
- Modify: `index.html` — add hero HTML inside `<body>` after nav, add hero CSS inside `<style>`

- [ ] **Step 1: Add hero CSS** inside `<style>` before `</style>`:

```css
    /* ── Hero ─────────────────────────────────────── */
    #hero {
      min-height: 100vh;
      display: grid;
      grid-template-columns: 1fr 1fr;
      align-items: center;
      gap: 60px;
      max-width: var(--max-w);
      margin: 0 auto;
      padding: 120px 24px 60px;
    }
    #hero .hero-text { }
    #hero .eyebrow {
      font-size: 12px;
      font-weight: 600;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 20px;
    }
    #hero h1 {
      font-size: clamp(2.4rem, 5vw, 4rem);
      font-weight: 700;
      line-height: 1.1;
      letter-spacing: -0.02em;
      margin-bottom: 20px;
    }
    #hero .subtitle {
      font-size: 15px;
      color: var(--text-muted);
      line-height: 1.7;
      max-width: 420px;
      margin-bottom: 36px;
    }
    #hero .cta-group { display: flex; gap: 14px; flex-wrap: wrap; }
    .btn-primary {
      display: inline-block;
      padding: 12px 28px;
      background: var(--accent);
      color: #fff;
      font-size: 13px;
      font-weight: 600;
      border-radius: 6px;
      letter-spacing: 0.04em;
      transition: background 0.2s, transform 0.2s;
    }
    .btn-primary:hover { background: var(--accent-hover); transform: translateY(-2px); }
    .btn-outline {
      display: inline-block;
      padding: 12px 28px;
      border: 1px solid var(--border);
      color: var(--text-muted);
      font-size: 13px;
      font-weight: 500;
      border-radius: 6px;
      letter-spacing: 0.04em;
      transition: border-color 0.2s, color 0.2s;
    }
    .btn-outline:hover { border-color: var(--text-muted); color: var(--text); }
    #hero .hero-image {
      display: flex;
      justify-content: center;
    }
    #hero .hero-image img {
      width: 380px;
      height: 480px;
      object-fit: cover;
      object-position: top;
      border-radius: 12px;
      border: 1px solid var(--border);
      box-shadow: 0 0 60px rgba(43,0,255,0.15);
    }
```

- [ ] **Step 2: Add hero HTML** inside `<body>`, after `</nav>` and before `<!-- sections go here -->`:

```html
  <!-- HERO -->
  <section id="hero">
    <div class="hero-text">
      <p class="eyebrow reveal">NYU Integrated Marketing · silueta.ai</p>
      <h1 class="reveal" style="transition-delay:0.1s">Poyuan<br>(Eric) Wang</h1>
      <p class="subtitle reveal" style="transition-delay:0.2s">
        Marketing Analytics &amp; AI-Augmented Brand Strategy.<br>
        Compressing team workflows into single-operator pipelines.
      </p>
      <div class="cta-group reveal" style="transition-delay:0.3s">
        <a href="#internship" class="btn-primary">View Work</a>
        <a href="#contact" class="btn-outline">Get in Touch</a>
      </div>
    </div>
    <div class="hero-image reveal" style="transition-delay:0.2s">
      <img src="assets/eric-headshot.png" alt="Poyuan (Eric) Wang">
    </div>
  </section>
```

- [ ] **Step 3: Open in browser to verify**

Run: `open /Users/wangbo/Desktop/portfolio/index.html`

Expected: Hero fills the viewport. Name on left, headshot on right. Blue accent on eyebrow text. Two buttons visible. Headshot has subtle blue glow.

- [ ] **Step 4: Commit**

```bash
cd /Users/wangbo/Desktop/portfolio
git add index.html
git commit -m "feat: add hero section"
```

---

### Task 3: About Section

**Files:**
- Modify: `index.html` — add about CSS and HTML

- [ ] **Step 1: Add about CSS** inside `<style>` before `</style>`:

```css
    /* ── Shared section styles ─────────────────────── */
    section:not(#hero) {
      padding: var(--section-pad);
    }
    .section-inner {
      max-width: var(--max-w);
      margin: 0 auto;
    }
    .section-label {
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 12px;
    }
    .section-title {
      font-size: clamp(1.6rem, 3vw, 2.4rem);
      font-weight: 700;
      letter-spacing: -0.02em;
      margin-bottom: 48px;
    }
    hr.divider {
      border: none;
      border-top: 1px solid var(--border);
      margin: 0;
    }

    /* ── About ────────────────────────────────────── */
    #about { border-top: 1px solid var(--border); }
    #about .about-grid {
      display: grid;
      grid-template-columns: 1fr 340px;
      gap: 80px;
      align-items: start;
    }
    #about blockquote {
      font-size: 18px;
      font-style: italic;
      color: var(--text-muted);
      border-left: 3px solid var(--accent);
      padding-left: 20px;
      margin-bottom: 28px;
      line-height: 1.7;
    }
    #about .bio {
      font-size: 15px;
      color: var(--text-muted);
      line-height: 1.8;
    }
    #about .stats {
      display: flex;
      flex-direction: column;
      gap: 32px;
      padding-top: 8px;
    }
    #about .stat-item { border-left: 2px solid var(--border); padding-left: 20px; }
    #about .stat-number {
      font-size: 2rem;
      font-weight: 700;
      color: var(--text);
      line-height: 1;
      margin-bottom: 6px;
    }
    #about .stat-label {
      font-size: 12px;
      color: var(--text-muted);
      letter-spacing: 0.06em;
      text-transform: uppercase;
    }
```

- [ ] **Step 2: Add about HTML** after the `<!-- HERO -->` section:

```html
  <hr class="divider">

  <!-- ABOUT -->
  <section id="about">
    <div class="section-inner">
      <p class="section-label reveal">About</p>
      <h2 class="section-title reveal">A rare mix of<br>data and stage.</h2>
      <div class="about-grid">
        <div>
          <blockquote class="reveal">
            "I believe the best marketing sits at the intersection of data and story — where analytics inform the message and creative execution makes it land. My goal is to build campaigns that don't just reach audiences but move them, using AI-augmented workflows to close the gap between insight and output."
          </blockquote>
          <p class="bio reveal">
            Poyuan (Eric) Wang is an NYU Integrated Marketing graduate student specializing in marketing analytics and AI-augmented brand strategy. Originally trained as a professional dancer — earning a full scholarship BFA in Classical Chinese Dance and performing before 1M+ live audiences annually with Shen Yun Performing Arts across five continents — Eric brings a rare combination of creative instinct and analytical precision to modern marketing.
            <br><br>
            He compresses what once required an entire team — research, targeting, creative production, automation — into a single AI-augmented workflow, delivering faster iteration and data-informed decisions without sacrificing creative quality. His work spans social media growth, direct marketing ROI modeling, competitive media planning, and creator brand strategy.
            <br><br>
            Currently interning at silueta.ai as a Creator Brand &amp; Social Media Marketing Intern, Eric is building the brand's content pipeline and creator outreach infrastructure from the ground up for a fast-paced startup launch.
          </p>
        </div>
        <div class="stats reveal">
          <div class="stat-item">
            <div class="stat-number">1M+</div>
            <div class="stat-label">Live audiences reached</div>
          </div>
          <div class="stat-item">
            <div class="stat-number">25–35</div>
            <div class="stat-label">Weekly content suggestions generated</div>
          </div>
          <div class="stat-item">
            <div class="stat-number">2</div>
            <div class="stat-label">International brand campaigns</div>
          </div>
          <div class="stat-item">
            <div class="stat-number">23%</div>
            <div class="stat-label">Enrollment growth driven</div>
          </div>
        </div>
      </div>
    </div>
  </section>
```

- [ ] **Step 3: Open in browser and verify**

Run: `open /Users/wangbo/Desktop/portfolio/index.html`

Expected: About section below hero. Pull-quote in italic with blue left border. Bio text in muted color. Stats column on right with large numbers.

- [ ] **Step 4: Commit**

```bash
cd /Users/wangbo/Desktop/portfolio
git add index.html
git commit -m "feat: add about section with bio and stats"
```

---

### Task 4: Skills Section

**Files:**
- Modify: `index.html` — add skills CSS and HTML

- [ ] **Step 1: Add skills CSS** inside `<style>` before `</style>`:

```css
    /* ── Skills ───────────────────────────────────── */
    #skills { background: var(--surface); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
    #skills .skills-grid {
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
    }
    .skill-tag {
      display: inline-block;
      padding: 8px 18px;
      border: 1px solid var(--border);
      border-radius: 100px;
      font-size: 13px;
      font-weight: 500;
      color: var(--text-muted);
      transition: border-color 0.2s, color 0.2s, background 0.2s;
      cursor: default;
    }
    .skill-tag:hover {
      border-color: var(--accent);
      color: var(--text);
      background: rgba(43,0,255,0.08);
    }
```

- [ ] **Step 2: Add skills HTML** after the about section:

```html
  <!-- SKILLS -->
  <section id="skills">
    <div class="section-inner">
      <p class="section-label reveal">Skills &amp; Tools</p>
      <h2 class="section-title reveal">What I work with.</h2>
      <div class="skills-grid">
        <span class="skill-tag reveal">SQL</span>
        <span class="skill-tag reveal">Google Ads</span>
        <span class="skill-tag reveal">Meta Ads Manager</span>
        <span class="skill-tag reveal">GA4</span>
        <span class="skill-tag reveal">Tableau</span>
        <span class="skill-tag reveal">Canva</span>
        <span class="skill-tag reveal">CapCut</span>
        <span class="skill-tag reveal">Excel / MegaStat</span>
        <span class="skill-tag reveal">Chinese (Native)</span>
        <span class="skill-tag reveal">English (Fluent)</span>
      </div>
    </div>
  </section>
```

- [ ] **Step 3: Open in browser and verify**

Run: `open /Users/wangbo/Desktop/portfolio/index.html`

Expected: Skills section on dark surface background. Pill-shaped tags. Hover turns border blue.

- [ ] **Step 4: Commit**

```bash
cd /Users/wangbo/Desktop/portfolio
git add index.html
git commit -m "feat: add skills section"
```

---

### Task 5: silueta.ai Internship Section

**Files:**
- Modify: `index.html` — add internship CSS and HTML

- [ ] **Step 1: Add internship CSS** inside `<style>` before `</style>`:

```css
    /* ── Internship ────────────────────────────────── */
    #internship { border-top: 1px solid var(--border); }
    #internship .internship-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 80px;
      align-items: start;
    }
    #internship .company-badge {
      display: inline-flex;
      align-items: center;
      gap: 10px;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 8px 16px;
      margin-bottom: 24px;
      font-size: 13px;
      font-weight: 600;
    }
    #internship .company-badge .dot {
      width: 8px; height: 8px;
      border-radius: 50%;
      background: var(--accent);
    }
    #internship .role-title {
      font-size: 13px;
      color: var(--text-muted);
      margin-bottom: 20px;
      letter-spacing: 0.04em;
    }
    #internship .internship-desc {
      font-size: 15px;
      color: var(--text-muted);
      line-height: 1.8;
      margin-bottom: 28px;
    }
    #internship ul {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 14px;
    }
    #internship ul li {
      font-size: 14px;
      color: var(--text-muted);
      padding-left: 20px;
      position: relative;
      line-height: 1.6;
    }
    #internship ul li::before {
      content: '';
      position: absolute;
      left: 0; top: 9px;
      width: 6px; height: 6px;
      border-radius: 50%;
      background: var(--accent);
    }
    #internship .ig-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
    }
    #internship .ig-grid img {
      width: 100%;
      aspect-ratio: 1 / 1;
      object-fit: cover;
      border-radius: 8px;
      border: 1px solid var(--border);
      transition: transform 0.3s, border-color 0.3s;
    }
    #internship .ig-grid img:hover {
      transform: scale(1.02);
      border-color: var(--accent);
    }
```

- [ ] **Step 2: Add internship HTML** after the skills section:

```html
  <!-- INTERNSHIP -->
  <section id="internship">
    <div class="section-inner">
      <p class="section-label reveal">Current Internship</p>
      <h2 class="section-title reveal">Creator Brand &amp; Social Media<br>@ silueta.ai</h2>
      <div class="internship-grid">
        <div>
          <div class="company-badge reveal">
            <span class="dot"></span>
            silueta.ai — Active 2025
          </div>
          <p class="role-title reveal">Creator Brand &amp; Social Media Marketing Intern</p>
          <p class="internship-desc reveal">
            Silueta is a creator-commerce startup building infrastructure for creator-led brands — where tastemakers curate, audiences validate, and the platform produces. As one of the first marketing hires, I work directly with the founding team to build the brand's social presence and creator partner pipeline from the ground up.
          </p>
          <ul>
            <li class="reveal">Built an AI-augmented content pipeline — researching competitor accounts, analyzing traffic sources, and auto-generating 25–35 weekly IG/TikTok content suggestions to accelerate creative output for a fast-paced startup launch.</li>
            <li class="reveal">Conducted competitive research and prospected creator partner accounts via social platforms — qualifying fit, analyzing traffic sources, and producing a weekly outreach target list to support the founding team's BD pipeline.</li>
            <li class="reveal">Grew the official @silueta_ai Instagram account from zero, establishing brand voice and editorial aesthetic across all posts.</li>
          </ul>
        </div>
        <div class="ig-grid reveal">
          <img src="assets/silueta-post-2.png" alt="silueta.ai Instagram profile">
          <img src="assets/silueta-post-1.png" alt="silueta.ai content feed">
          <img src="assets/silueta-post-3.png" alt="silueta.ai post — skin campaign">
          <img src="assets/silueta-post-4.png" alt="silueta.ai post — brand campaign">
        </div>
      </div>
    </div>
  </section>
```

- [ ] **Step 3: Open in browser and verify**

Run: `open /Users/wangbo/Desktop/portfolio/index.html`

Expected: Two-column layout. Left: company badge with blue dot, role title, description, bullet list. Right: 2×2 Instagram grid. Images load from assets/.

- [ ] **Step 4: Commit**

```bash
cd /Users/wangbo/Desktop/portfolio
git add index.html
git commit -m "feat: add silueta.ai internship section"
```

---

### Task 6: Course Projects Section

**Files:**
- Modify: `index.html` — add projects CSS and HTML

- [ ] **Step 1: Add projects CSS** inside `<style>` before `</style>`:

```css
    /* ── Projects ──────────────────────────────────── */
    #projects { background: var(--surface); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
    #projects .projects-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 24px;
    }
    .project-card {
      background: var(--surface-2);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 36px;
      display: flex;
      flex-direction: column;
      gap: 16px;
      transition: border-color 0.25s, transform 0.25s;
    }
    .project-card:hover {
      border-color: var(--accent);
      transform: translateY(-4px);
    }
    .project-card .card-tag {
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--accent);
    }
    .project-card h3 {
      font-size: 20px;
      font-weight: 700;
      line-height: 1.3;
      letter-spacing: -0.01em;
    }
    .project-card p {
      font-size: 14px;
      color: var(--text-muted);
      line-height: 1.7;
      flex: 1;
    }
    .project-card .card-links {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      margin-top: 8px;
    }
    .card-links .btn-primary,
    .card-links .btn-outline {
      font-size: 12px;
      padding: 9px 18px;
    }
```

- [ ] **Step 2: Add projects HTML** after the internship section:

```html
  <!-- PROJECTS -->
  <section id="projects">
    <div class="section-inner">
      <p class="section-label reveal">Course Projects</p>
      <h2 class="section-title reveal">Academic work, real results.</h2>
      <div class="projects-grid">

        <div class="project-card reveal">
          <span class="card-tag">Campaign Strategy · Media Planning</span>
          <h3>Mercedes-Benz GLC — Competitive Market Research &amp; Media Strategy</h3>
          <p>
            Identified CA's 20–25% EV share as GLC's primary threat using DMA research (Mintel 2025, Cox Automotive). Repositioned GLC against Tesla — from performance specs to premium passenger experience. Built a $25M, 296M-impression media plan across SF/LA/SD with 4 audience moments. Produced 3 AI-assisted creatives commended by professor (active tech CMO).
          </p>
          <div class="card-links">
            <a href="assets/mb-landing/Landing page_dark.html" target="_blank" class="btn-primary">View Landing Page</a>
            <a href="assets/mb-deck-updated.pdf" target="_blank" class="btn-outline">View Deck</a>
          </div>
        </div>

        <div class="project-card reveal">
          <span class="card-tag">Data Analytics · Direct Marketing</span>
          <h3>Applebee's eClub — Customer Segmentation &amp; Direct Marketing ROI Analysis</h3>
          <p>
            Applied RFM segmentation to 400 eClub records — surfacing VIP ($391 avg spend, 18 visits/yr) and Loyal ($232, 11 visits/yr) segments as primary targets. Designed a 3-wave DM + email campaign reaching 100K recipients within a $250K budget. Modeled $205K spend projecting $252K revenue at 22.9% ROI. Built a 6-KPI dashboard targeting ≥17.2% redemption rate and ≥35% 90-day repeat visit rate.
          </p>
          <div class="card-links">
            <a href="assets/applebees-deck.pdf" target="_blank" class="btn-primary">View Analysis</a>
          </div>
        </div>

      </div>
    </div>
  </section>
```

- [ ] **Step 3: Open in browser and verify**

Run: `open /Users/wangbo/Desktop/portfolio/index.html`

Expected: Two project cards on dark surface. Hover lifts card and turns border blue. "View Landing Page" button opens MB landing page in new tab. "View Deck" opens PDF in new tab.

- [ ] **Step 4: Commit**

```bash
cd /Users/wangbo/Desktop/portfolio
git add index.html
git commit -m "feat: add course projects section"
```

---

### Task 7: Media & Campaigns Section

**Files:**
- Modify: `index.html` — add media CSS and HTML

- [ ] **Step 1: Add media CSS** inside `<style>` before `</style>`:

```css
    /* ── Media ─────────────────────────────────────── */
    #media { border-top: 1px solid var(--border); }
    #media .media-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 40px;
    }
    .media-item { display: flex; flex-direction: column; gap: 16px; }
    .media-item .video-wrap {
      position: relative;
      padding-bottom: 56.25%;
      height: 0;
      overflow: hidden;
      border-radius: 10px;
      border: 1px solid var(--border);
    }
    .media-item .video-wrap iframe {
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 100%;
      border: none;
    }
    .media-item .media-meta { }
    .media-item .media-brand {
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 6px;
    }
    .media-item .media-title {
      font-size: 16px;
      font-weight: 600;
      margin-bottom: 6px;
    }
    .media-item .media-desc {
      font-size: 13px;
      color: var(--text-muted);
      line-height: 1.6;
    }
```

- [ ] **Step 2: Add media HTML** after the projects section:

```html
  <!-- MEDIA -->
  <section id="media">
    <div class="section-inner">
      <p class="section-label reveal">Media &amp; Campaigns</p>
      <h2 class="section-title reveal">On-camera brand work.</h2>
      <div class="media-grid">

        <div class="media-item reveal">
          <div class="video-wrap">
            <iframe
              src="https://www.youtube.com/embed/06l52ERbgaE"
              title="Volkswagen Commercial Vehicles Campaign"
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
              allowfullscreen>
            </iframe>
          </div>
          <div class="media-meta">
            <p class="media-brand">Volkswagen</p>
            <p class="media-title">Commercial Vehicles Campaign</p>
            <p class="media-desc">Selected as campaign-facing talent for an integrated Volkswagen Commercial Vehicles launch across TV, social, and digital platforms — contributing to 2.4M+ YouTube impressions.</p>
          </div>
        </div>

        <div class="media-item reveal">
          <div class="video-wrap">
            <iframe
              src="https://www.youtube.com/embed/qjB16vRecDs"
              title="Chang Hwa Commercial Bank Visual Campaign"
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
              allowfullscreen>
            </iframe>
          </div>
          <div class="media-meta">
            <p class="media-brand">Chang Hwa Commercial Bank</p>
            <p class="media-title">Visual Campaign Ambassador</p>
            <p class="media-desc">Selected as campaign visual ambassador for a two-year multi-platform brand campaign across Instagram, YouTube, TV, and digital media.</p>
          </div>
        </div>

      </div>
    </div>
  </section>
```

- [ ] **Step 3: Open in browser and verify**

Run: `open /Users/wangbo/Desktop/portfolio/index.html`

Expected: Two YouTube embeds side by side, each with brand label, title, and description below. Videos are playable.

- [ ] **Step 4: Commit**

```bash
cd /Users/wangbo/Desktop/portfolio
git add index.html
git commit -m "feat: add media and campaigns section with YouTube embeds"
```

---

### Task 8: Contact Section + Footer

**Files:**
- Modify: `index.html` — add contact CSS and HTML

- [ ] **Step 1: Add contact CSS** inside `<style>` before `</style>`:

```css
    /* ── Contact ───────────────────────────────────── */
    #contact {
      background: var(--surface);
      border-top: 1px solid var(--border);
      text-align: center;
    }
    #contact .contact-inner { max-width: 600px; margin: 0 auto; }
    #contact .contact-tagline {
      font-size: clamp(1.4rem, 3vw, 2rem);
      font-weight: 700;
      line-height: 1.3;
      margin-bottom: 16px;
      letter-spacing: -0.02em;
    }
    #contact .contact-sub {
      font-size: 15px;
      color: var(--text-muted);
      margin-bottom: 40px;
    }
    #contact .contact-links {
      display: flex;
      justify-content: center;
      gap: 16px;
      flex-wrap: wrap;
    }
    footer {
      padding: 24px;
      text-align: center;
      font-size: 12px;
      color: var(--text-muted);
      border-top: 1px solid var(--border);
    }
```

- [ ] **Step 2: Add contact HTML** after the media section:

```html
  <!-- CONTACT -->
  <section id="contact">
    <div class="section-inner">
      <div class="contact-inner">
        <p class="section-label reveal">Contact</p>
        <h2 class="contact-tagline reveal">Let's work together.</h2>
        <p class="contact-sub reveal">Open to marketing roles, brand collaborations, and internship opportunities.</p>
        <div class="contact-links reveal">
          <a href="mailto:pw2591@nyu.edu" class="btn-primary">pw2591@nyu.edu</a>
          <a href="https://linkedin.com/in/poyuan-wang-393751360" target="_blank" class="btn-outline">LinkedIn</a>
        </div>
      </div>
    </div>
  </section>

  <footer>
    <p>© 2026 Poyuan (Eric) Wang · NYU Integrated Marketing</p>
  </footer>
```

- [ ] **Step 3: Open in browser and verify**

Run: `open /Users/wangbo/Desktop/portfolio/index.html`

Expected: Centered contact section. Email button (blue), LinkedIn button (outline). Footer with copyright.

- [ ] **Step 4: Commit**

```bash
cd /Users/wangbo/Desktop/portfolio
git add index.html
git commit -m "feat: add contact section and footer"
```

---

### Task 9: Mobile Responsive Pass

**Files:**
- Modify: `index.html` — add responsive CSS

- [ ] **Step 1: Add responsive CSS** inside `<style>` before `</style>`:

```css
    /* ── Responsive ────────────────────────────────── */
    @media (max-width: 768px) {
      nav { padding: 16px 20px; }
      nav ul { gap: 18px; }
      nav ul a { font-size: 12px; }

      #hero {
        grid-template-columns: 1fr;
        padding: 100px 24px 60px;
        text-align: center;
      }
      #hero .subtitle { max-width: 100%; }
      #hero .cta-group { justify-content: center; }
      #hero .hero-image { order: -1; }
      #hero .hero-image img { width: 240px; height: 300px; }

      #about .about-grid { grid-template-columns: 1fr; gap: 48px; }
      #about .stats { flex-direction: row; flex-wrap: wrap; }
      #about .stat-item { flex: 1; min-width: 120px; }

      #internship .internship-grid { grid-template-columns: 1fr; gap: 48px; }
      #projects .projects-grid { grid-template-columns: 1fr; }
      #media .media-grid { grid-template-columns: 1fr; }
    }

    @media (max-width: 480px) {
      nav ul { display: none; }
      #hero h1 { font-size: 2.2rem; }
    }
```

- [ ] **Step 2: Open in browser and verify at mobile width**

Run: `open /Users/wangbo/Desktop/portfolio/index.html`

In browser DevTools (F12 → Toggle device toolbar), set width to 390px (iPhone 14).

Expected: Single-column layout. Headshot above text in hero. All sections stack vertically. No horizontal overflow.

- [ ] **Step 3: Commit**

```bash
cd /Users/wangbo/Desktop/portfolio
git add index.html
git commit -m "feat: add mobile responsive styles"
```

---

### Task 10: Deploy to GitHub Pages

**Files:**
- No code changes — git push + GitHub Pages config

- [ ] **Step 1: Create a GitHub repository**

Go to https://github.com/new and create a new **public** repo named `portfolio`. Do NOT initialize with README (we already have one).

- [ ] **Step 2: Connect local repo to GitHub and push**

```bash
cd /Users/wangbo/Desktop/portfolio
git remote add origin https://github.com/<your-username>/portfolio.git
git branch -M main
git push -u origin main
```

Replace `<your-username>` with your actual GitHub username.

Expected: Push succeeds, all files appear on GitHub.

- [ ] **Step 3: Enable GitHub Pages**

1. Go to your repo on GitHub
2. Click **Settings** → **Pages** (left sidebar)
3. Under **Source**, select **Deploy from a branch**
4. Branch: `main`, folder: `/ (root)`
5. Click **Save**

Expected: GitHub shows "Your site is being published" — takes ~1 minute.

- [ ] **Step 4: Copy the public URL**

GitHub Pages URL format: `https://<your-username>.github.io/portfolio`

Open that URL in a browser and verify the full site loads correctly.

- [ ] **Step 5: Update README with live URL**

In `README.md`, replace `_to be added after GitHub Pages deployment_` with the actual URL.

```bash
cd /Users/wangbo/Desktop/portfolio
git add README.md
git commit -m "docs: add live GitHub Pages URL"
git push
```

---

## Self-Review Checklist

- [x] **Spec coverage:** Hero · About (personal statement + bio) · Skills · silueta.ai internship · Course projects (MB + Applebee's) · Media (VW + Chang Hwa) · Contact — all sections accounted for
- [x] **Part A:** Personal statement (blockquote in About) · Bio · Skills · Accomplishments (stats strip + project descriptions) · Contact ✓
- [x] **Part B:** Internship work samples · Art/Media (YouTube) · Course project work · Visual presentations (PDF decks) · Past campaign work ✓
- [x] **No placeholders:** All code is complete and exact
- [x] **Asset paths consistent:** All `assets/` references match files present in the repo
- [x] **YouTube embed URLs:** Converted from `youtu.be/` short links to `youtube.com/embed/` format ✓
- [x] **MB landing page:** References copied MP4 and PNG — both in `assets/mb-landing/` ✓
