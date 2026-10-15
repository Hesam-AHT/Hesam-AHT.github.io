# Build plan: Amirhesam Torkashvand's portfolio site

**Live address:** https://hesam-aht.github.io
**Repository:** `Hesam-AHT/Hesam-AHT.github.io` (public, branch `main`)
**Hosting:** GitHub Pages, served from the repository root
**Approved design:** artboard **E · Tabbed** on the "Portfolio Style Options" canvas (light theme)
**Planned with:** Claude Opus · **To be built with:** Claude Sonnet

---

## 0. What we are building

A one-page, tabbed personal portfolio for a master's student who is applying for a six-month thesis position in a European research group, and later a PhD. The main readers are professors and research-group leads, who skim. The site must load fast, read clearly, and every fact on it must match the CV.

The layout is a left **profile card** (photo, name, title, contacts) and a right **content panel** with four tabs: **About · Resume · Research · Projects**. Only one tab is visible at a time. The Projects tab has category filter buttons.

The site starts from the free, MIT-licensed **vCard** template by codewithsadee (https://github.com/codewithsadee/vcard-personal-portfolio). That template is dark; this site uses a **light theme** (section 5).

---

## 1. Rules for the builder

1. **Follow this plan, don't redesign.** If something here is unclear or impossible, stop and ask Amirhesam instead of guessing.
2. **Use only the content in this file.** Don't invent numbers, skills, dates, percentages, testimonials or projects. All the text is in sections 7 to 12.
3. **Never put the phone number on the site**, in any file.
4. **Keep it plain:** HTML, CSS and vanilla JavaScript only. No frameworks, no build step, no npm.
5. **Keep the template's `LICENSE` file unchanged.** MIT requires keeping the copyright notice.
6. **Don't fork the template.** Copy its files into this repository, so the repo has its own clean history and name.
7. Wherever a value is still missing, keep the marked placeholder (`TODO:`) and list it in your final summary. Section 15 lists what's missing.

---

## 2. Stack and hosting

- Static files served by **GitHub Pages** from `main`, at the root folder `/`.
- Add an empty `.nojekyll` file at the root, so GitHub serves the files as they are, without running Jekyll.
- External resources: Google Fonts (Poppins 300/400/500/600, already linked by the template) and Ionicons 5.5.2 from unpkg (already linked by the template). Add nothing else.

---

## 3. Final repository layout

```
Hesam-AHT.github.io/
├── index.html
├── .nojekyll
├── LICENSE                     ← from the template, unchanged
├── README.md                   ← rewritten (section 18)
├── PLAN.md                     ← this file
├── CLAUDE.md                   ← rules for future edits (section 19)
└── assets/
    ├── css/style.css           ← template CSS + light theme + new components
    ├── js/script.js            ← template JS, trimmed (section 13)
    ├── files/
    │   └── Amirhesam_Torkashvand_CV.pdf   ← TODO: supplied by Amirhesam
    └── images/
        ├── avatar.jpg          ← supplied (600×600 portrait)
        └── favicon.svg         ← new, simple "AT" monogram
```

Delete from the template: every demo image (`avatar-1..4.png`, `blog-*.jpg`, `project-*`, `logo-*-color.png`, `icon-*.svg`, `my-avatar.png`, `logo.ico`, `logo.svg`), `index.txt`, the `website-demo-image/` folder, and `.github/FUNDING.yml` (that's the template author's funding link).

---

## 4. Setup steps

1. Clone the template into a temporary folder **outside** the repository: `git clone --depth 1 https://github.com/codewithsadee/vcard-personal-portfolio.git`. Its default branch is `master`.
2. Copy `index.html`, `LICENSE` and `assets/` into the repository root. Don't copy the template's `.git`.
3. Delete the files listed in section 3.
4. Add `assets/images/avatar.jpg` (provided with this plan), and add the CV PDF when Amirhesam supplies it.
5. Add `.nojekyll`.
6. Make the changes in sections 5 to 14, then run the checks in section 16.

---

## 5. Light theme

### 5.1 Replace the colour variables in `:root` of `style.css`

The template's variable names are dark-theme names (for example `--smoky-black`), so keep the names and change only the values. That way every rule that uses them switches automatically.

```css
/* light theme — replaces the template's colour values */
--bg-gradient-onyx: #eef0f3;          /* avatar box, icon tiles */
--bg-gradient-jet: #f8f9fb;           /* inner fill of cards and buttons */
--bg-gradient-yellow-1: #9a6700;      /* focus ring of the "Show contacts" button */
--bg-gradient-yellow-2: #fbf6ea;      /* focus fill of the "Show contacts" button */
--border-gradient-onyx: #e3e5e9;      /* 1px card borders */
--text-gradient-yellow: linear-gradient(to right, #9a6700, #b7791f); /* title underline, timeline dots */

--jet: #e3e5e9;                       /* borders, separators, timeline line */
--onyx: #eef0f3;                      /* title badge, scrollbar track */
--eerie-black-1: #f8f9fb;
--eerie-black-2: #ffffff;             /* sidebar and article cards */
--smoky-black: #f4f5f7;               /* page background */
--white-1: #16181d;                   /* text that was white */
--white-2: #16181d;                   /* headings, names, contact links */
--orange-yellow-crayola: #9a6700;     /* accent: active tab, links, labels */
--vegas-gold: #7a5200;                /* accent hover */
--light-gray: #3f444b;                /* body text */
--light-gray-70: #5d636b;             /* muted labels, dates */
--bittersweet-shimmer: #b42318;

--shadow-1: 0 4px 16px rgba(16, 24, 40, 0.06);
--shadow-2: 0 1px 2px rgba(16, 24, 40, 0.04), 0 10px 30px rgba(16, 24, 40, 0.06);
--shadow-3: 0 1px 2px rgba(16, 24, 40, 0.04), 0 12px 32px rgba(16, 24, 40, 0.07);
--shadow-4: 0 16px 40px rgba(16, 24, 40, 0.08);
--shadow-5: 0 20px 60px rgba(16, 24, 40, 0.10);
```

Also replace the lighter shadow overrides inside `@media (min-width: 768px)`, which use `hsla(0, 0%, 0%, 0.125)`, with the same light values.

### 5.2 Fix the colours that are hard-coded outside `:root`

Search `style.css` for literal `hsl(`, `hsla(`, `rgb(` and `#…` values outside `:root` and switch each to a light equivalent:

- `.navbar` background `hsla(240, 1%, 17%, 0.75)` → `rgba(255, 255, 255, 0.85)` (keep the blur).
- `::selection`: background `#9a6700`, text `#ffffff`.
- The scrollbar thumb colours (`hsla(0, 0%, 100%, …)` in the 1024px media query) → `rgba(16, 24, 40, 0.15)`, and `0.25` on hover.
- Remove any rule that only styles deleted elements (testimonials, modal, clients, blog, contact form, project images), together with those elements.

### 5.3 Colour rules

- Body text `#3f444b` on white; headings `#16181d`; muted text `#5d636b`. All of these pass WCAG AA contrast.
- The accent `#9a6700` is the only accent colour. Use it for the active tab, the title underline, dates in the timeline, category labels, links and the status dot.
- The accent passes AA (about 4.9:1) on white. Don't use a lighter gold for text.

---

## 6. Page head

```html
<title>Amirhesam Torkashvand · Computer Vision &amp; Trustworthy AI</title>
<meta name="description" content="M.Sc. student in AI &amp; Data Analytics at Politecnico di Torino working on computational pathology, visual foundation models and trustworthy AI. Looking for a master's thesis position from early 2027.">
<meta name="author" content="Amirhesam Torkashvand">
<link rel="icon" href="./assets/images/favicon.svg" type="image/svg+xml">

<meta property="og:type" content="website">
<meta property="og:title" content="Amirhesam Torkashvand · Computer Vision &amp; Trustworthy AI">
<meta property="og:description" content="M.Sc. student at Politecnico di Torino. Looking for a master's thesis position from early 2027.">
<meta property="og:url" content="https://hesam-aht.github.io/">
<meta property="og:image" content="https://hesam-aht.github.io/assets/images/avatar.jpg">
```

**Favicon:** `favicon.svg` is a 64×64 rounded square filled `#9a6700`, with the white letters "AT" in Poppins 600 (system sans-serif as the fallback).

---

## 7. Sidebar (profile card)

This keeps the template's structure (`.sidebar`, `.sidebar-info`, `.sidebar-info_more`) and its "Show Contacts" toggle on small screens.

- **Photo:** `./assets/images/avatar.jpg`, alt text `Portrait of Amirhesam Torkashvand`, with `width` and `height` attributes set. Keep the template's rounded `.avatar-box`.
- **Name** (`h1.name`, with `title` set to the name): `Amirhesam Torkashvand`
- **Title badge** (`p.title`): `M.Sc. Student in AI & Data Analytics`
- **Status line** (new, below the badge): an 8px accent dot followed by `Open to thesis positions · early 2027, late 2026`, at 12px, weight 500, in the accent colour.
- **Contacts** (replace all four template items; **remove Phone and Birthday**):

| Icon (ionicons) | Label | Value | Link |
|---|---|---|---|
| `mail-outline` | Email | ht.torkashvand210@gmail.com | `mailto:ht.torkashvand210@gmail.com` |
| `location-outline` | Location | Turin, Italy | (plain `<address>`, no link) |
| `logo-github` | GitHub | github.com/Hesam-AHT | `https://github.com/Hesam-AHT` |
| `logo-linkedin` | LinkedIn | in/amirhesam-torkashvand | `https://www.linkedin.com/in/amirhesam-torkashvand` |

  The email is long: add `word-break: break-all` to `.contact-link` so it wraps inside the card.

- **Social list:** GitHub (`logo-github`) and LinkedIn (`logo-linkedin`) only, each with an `aria-label` and `target="_blank" rel="noopener"`. Delete Facebook, Twitter and Instagram.

---

## 8. Navigation

Four buttons in this order:

```html
<button class="navbar-link active" data-nav-link>About</button>
<button class="navbar-link" data-nav-link>Resume</button>
<button class="navbar-link" data-nav-link>Research</button>
<button class="navbar-link" data-nav-link>Projects</button>
```

**Important:** the template's JavaScript switches tabs by comparing each button's `innerHTML`, lower-cased, with each article's `data-page`. It also assumes button number *i* belongs to article number *i*. So:

- The button text must be exactly `About`, `Resume`, `Research`, `Projects`, with no icons or extra whitespace inside.
- The articles must appear in the same order, with `data-page="about"`, `"resume"`, `"research"`, `"projects"`.
- Delete the Blog, Portfolio and Contact buttons and the Contact article. The Portfolio article becomes Projects and the Blog article becomes Research, as below.
- Add `type="button"` to every button.

Each article keeps the template's header: `<header><h2 class="h2 article-title">…</h2></header>`, which draws the accent underline. The titles are **About me**, **Resume**, **Research** and **Projects**.

---

## 9. About tab (`data-page="about"`, active by default)

### 9.1 Bio (`section.about-text`)

> I'm a master's student in Computer Engineering (Artificial Intelligence & Data Analytics) at Politecnico di Torino, graduating in July 2027. My work spans computational pathology, visual foundation models (DINOv2/v3, SAM), explainable and fair machine learning, and agentic LLM systems. I enjoy the whole research cycle, from curating data and building baselines to running ablations and releasing reproducible open-source code.

> I'm looking for a six-month external master's thesis from early 2027, in a European research group working on computer vision, medical image analysis or trustworthy AI, and I'm strongly motivated to continue towards a PhD.

### 9.2 News & updates (new section; `h3` "News & updates")

A simple list. The date is in the accent colour, weight 500, followed by ` · ` and the text:

- **Oct 2026** · Started work on three SemEval-2027 shared tasks with MALTO.
- **Jul 2026** · Defended my Machine Learning in Applications project on glomeruli segmentation and unsupervised necrotization profiling in kidney biopsies.
- **Apr 2026** · Built a multi-agent fraud detector at the Reply AI-Agent Hackathon.
- **Feb 2026** · Joined MALTO, Politecnico di Torino's ML student team, after placing 3rd of 43 in its recruitment hackathon.
- **Feb 2026** · Completed the Reply × Politecnico di Torino industry challenge with an agentic research assistant.

### 9.3 In a nutshell: what I work on (reuse the template's `.service` section)

Change the heading from "What i'm doing" to **In a nutshell: what I work on**. Use four `.service-item`s, replacing each icon `<img>` with `<ion-icon name="…" aria-hidden="true">` (36px, accent colour):

| Icon | Title | Text |
|---|---|---|
| `medkit-outline` | Computational pathology | Segmenting glomeruli in whole-slide kidney biopsies and profiling necrotization with foundation-model embeddings. |
| `layers-outline` | Visual foundation models | Using DINOv2, DINOv3 and SAM as dense feature extractors, and fine-tuning them for semantic correspondence. |
| `shield-checkmark-outline` | Trustworthy & explainable AI | Measuring whether SHAP and LIME explanations are equally faithful across demographic subgroups. |
| `git-network-outline` | Agentic AI | Multi-agent LLM systems for answering questions over scientific papers and for detecting financial fraud. |

### 9.4 Affiliations (replaces the template's `.clients` section)

Heading: **Affiliations**. Show text chips, not logos: a white background, a 1px `--jet` border, 12px radius, 12px × 18px padding, and heading-coloured text.

- Politecnico di Torino
- MALTO ML Student Team
- Reply (industry challenge)

(Islamic Azad University is deliberately **not** in this list.)

### 9.5 Delete

Delete the testimonials section, the testimonials modal, the overlay and the clients logo list.

---

## 10. Resume tab (`data-page="resume"`)

Put a **Download CV (PDF)** button at the top: a link to `./assets/files/Amirhesam_Torkashvand_CV.pdf` with the `download` attribute, an accent background, white text, 12px radius and 12px × 20px padding. TODO: the PDF comes from Amirhesam.

Then three timelines using the template's `.timeline` markup (title-wrapper with an icon box, then `ol.timeline-list`, then `li.timeline-item` holding an `h4.timeline-item-title`, a date `span` and a `p.timeline-text`):

### Education (icon `book-outline`)
1. **M.Sc. Computer Engineering – AI & Data Analytics** · *Politecnico di Torino · Sep 2024 – Jul 2027 (expected)* · Coursework: Advanced Machine Learning; Machine Learning in Applications.
2. **M.Sc. Artificial Intelligence (not completed)** · *Islamic Azad University, Central Tehran Branch · Sep 2023 – Jul 2024* · Withdrew to enrol at Politecnico di Torino.
3. **B.Sc. Electrical Engineering – Electronics** · *Islamic Azad University, Central Tehran Branch · Sep 2018 – Jun 2023* · (no text line)

### Experience (icon `briefcase-outline`)
1. **Member, MALTO ML Student Team** · *Politecnico di Torino · Feb 2026 – present* · 3rd of 43 in the recruitment hackathon (Qwen 2.5 + QLoRA, 0.979 macro-F1). Now working on three SemEval-2027 shared tasks.
2. **Industry Challenge: Agentic Research Assistant** · *Reply × Politecnico di Torino · Sep 2025 – Feb 2026* · Designed and built a multi-agent assistant for question answering over scientific papers, mentored by Reply and Politecnico di Torino.
3. **Research Assistant** · *Islamic Azad University, Tehran · Feb 2023 – Jun 2024* · Personality recognition from text with Transformer encoders and hybrid CNN/LSTM architectures.
4. **Research Intern** · *MECO – MAPNA Electric & Control · Jul – Aug 2022* · LoRaWAN protocol design and deployment for low-power IoT devices.

### Teaching (icon `school-outline`)
1. **Teaching Assistant** · *Islamic Azad University · Sep 2022 – Jun 2023* · Linear Algebra; Electric Machines I.
2. **Laboratory Assistant** · *Islamic Azad University · Feb – Jul 2022* · Telecommunication Circuits Laboratory.

Put the date `span` in the accent colour.

### Skills & languages (replaces the template's skill progress bars)

**Delete the percentage progress bars entirely**; they would be invented numbers. Use the heading **Skills & languages**, a chip list (`#eef0f3` background, heading-coloured text, 13px, pill radius, 6px × 14px padding) and a languages line underneath:

Chips: PyTorch · Hugging Face · LoRA / QLoRA · YOLOv8-seg · DINOv2/v3 · SAM · SHAP · LIME · LangGraph · RAG · Python · TypeScript

Languages line: `Persian (native) · English C1 (IELTS 7.0) · Italian A2`

---

## 11. Research tab (`data-page="research"`, replaces the Blog article)

Delete all the blog markup. Build this instead, using new classes (section 14.2):

### 11.1 Seeking box
A card (`#f8f9fb` background, 1px `--jet` border, 16px radius, 20px × 22px padding):
- Label: `SEEKING` (12px, uppercase, letter-spacing 0.08em, accent, weight 600)
- Text (heading colour): A six-month external master's thesis from early 2027 in computer vision, medical image analysis or trustworthy AI, on site with co-supervision from Politecnico di Torino.

### 11.2 Research interests (`h3`, then a chip list styled like the skills chips in section 10)
Medical image analysis & computational pathology · Visual foundation models & self-supervised learning · Explainable & trustworthy AI · Vision–language learning · Video understanding · Agentic AI & RAG

### 11.3 Research projects (`h3`, then four cards)
Each card has the same style as the Seeking box, with 22px padding. Inside: a title (17px, weight 500, heading colour), a context line (13px, accent, weight 500), a bulleted list (14px), and an optional `Code ↗` link (14px, accent, weight 500, `target="_blank" rel="noopener"`).

**1. Glomeruli Segmentation & Unsupervised Necrotization Profiling in Kidney Biopsies**
Context: Machine Learning in Applications · Politecnico di Torino · team of 4
- Three-phase pipeline on 9 whole-slide images (677 annotated glomeruli), with Macenko stain normalisation and hard-negative tiles against batch effects and false positives.
- Fine-tuned YOLOv8x-seg: mask mAP@50 0.993 (mAP@50–95 0.757), mean Dice 0.83 on 170 held-out patches.
- Slide-corrected DINOv2 embeddings show necrotization is one continuous healthy-to-sclerotic axis, robust across 8 backbone and masking setups including UNI and H0-mini.
- No code link.

**2. Semantic Correspondence with Visual Foundation Models**
Context: Advanced Machine Learning · Politecnico di Torino · team of 3
- Zero-shot on SPair-71k, DINOv2 led with 51.9% PCK@0.10 against 20.4% for SAM.
- Fine-tuning DINOv2 with an InfoNCE patch-matching loss raised it to 67.4%, and windowed soft-argmax decoding to 69.1%.
- Ablations of LoRA, mutual-nearest-neighbour verification and ensembling; transfer to AP-10K animals reached 68.1%.
- `Code ↗` → TODO: repo URL (placeholder `https://github.com/Hesam-AHT`)

**3. Subgroup-Disaggregated Faithfulness in Explainable AI**
Context: XAI · Fairness · Trustworthy ML
- Introduced Worst Subgroup Faithfulness (WSF), Faithfulness Disparity (FD) and the Explanation Desert Index (EDI).
- SHAP beat LIME globally (PGI 0.159 vs 0.115), but its faithfulness for women was about one-fifth of that for men (0.044 vs 0.208) and negative for under-25s.
- Reproducible pipeline with an interactive Streamlit demo.
- `Code ↗` → TODO: repo URL (placeholder `https://github.com/Hesam-AHT`). Optional TODO: a "Demo ↗" link once Amirhesam gives the Streamlit URL.

**4. Mistake Detection in Procedural Videos**
Context: Advanced Machine Learning · Politecnico di Torino
- Step-level mistake detection and recipe-level verification from pre-extracted video features.
- Compared MLP, LSTM and Transformer temporal models; temporal models outperformed non-temporal baselines.
- No code link.

---

## 12. Projects tab (`data-page="projects"`, replaces the Portfolio article)

### 12.1 Filters
Keep the template's two filter controls: the button row (`.filter-list`, for large screens) and the select box (`.filter-select-box`, for small screens). Both get the same five options:

`All` · `Computer vision` · `Trustworthy AI` · `Agentic AI` · `NLP`

**Important:** the template's JavaScript lower-cases the clicked button's `innerText` and compares it with each item's `data-category`. So the `data-category` values must be exactly `computer vision`, `trustworthy ai`, `agentic ai` and `nlp`, and the select's default label stays "Select category".

### 12.2 Project cards (no images)
Remove the `<figure class="project-img">` and the eye-icon hover. Each item is:

```html
<li class="project-item active" data-filter-item data-category="computer vision">
  <div class="project-card">
    <p class="project-card-category">Computer vision · Medical AI</p>
    <h3 class="project-card-title">Glomeruli segmentation in kidney biopsies</h3>
    <p class="project-card-text">YOLOv8x-seg on whole-slide images reaches mask mAP@50 0.993.</p>
    <!-- optional: <a class="project-card-link" href="…" target="_blank" rel="noopener">Code ↗</a> -->
  </div>
</li>
```

The seven projects, in this order:

| # | data-category | Category label | Title | Text | Code link |
|---|---|---|---|---|---|
| 1 | computer vision | Computer vision · Medical AI | Glomeruli segmentation in kidney biopsies | YOLOv8x-seg on whole-slide images reaches mask mAP@50 0.993. | none |
| 2 | computer vision | Computer vision | Semantic correspondence with DINOv2 | Fine-tuned DINOv2 reaches 69.1% PCK@0.10 on SPair-71k. | TODO |
| 3 | computer vision | Computer vision · Video | Mistake detection in procedural videos | MLP, LSTM and Transformer models for step-level mistake detection. | none |
| 4 | trustworthy ai | Trustworthy AI | Subgroup faithfulness in XAI | Three metrics expose fairness gaps in SHAP and LIME explanations, with a Streamlit demo. | TODO |
| 5 | agentic ai | Agentic AI · RAG | Agentic research assistant | Multi-agent question answering over scientific papers with line-level citations. | TODO |
| 6 | agentic ai | Agentic AI | Multi-agent fraud detection | LangGraph agents issue FRAUD / REVIEW / CLEAN verdicts on payments. | TODO |
| 7 | nlp | NLP · LLM fine-tuning | Qwen 2.5 text classification | QLoRA fine-tune on an A100: 0.979 macro-F1, 3rd of 43 in the MALTO hackathon. | TODO |

Until Amirhesam supplies the real repository URLs, every "TODO" link points to `https://github.com/Hesam-AHT`.

### 12.3 Grid (this matters: an earlier draft let the last card stick out)
Override the template's `.project-list` columns at every breakpoint with one rule:

```css
.project-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(min(100%, 230px), 1fr));
  gap: 16px;
}
```

Remove the template's `grid-template-columns` overrides for `.project-list` in the 580px and 1024px media queries. Every card must have the same width, including a card alone on the last row, and none may extend past the white panel.

---

## 13. JavaScript (`assets/js/script.js`)

The template's script fails at the first missing element, and that stops the tab navigation. Remove these blocks **together with** their HTML:

- the testimonials and modal block (`testimonialsItem`, `modalContainer`, `modalCloseBtn`, `overlay`, `modalImg`, `modalTitle`, `modalText` and their listeners)
- the contact form block (`form`, `formInputs`, `formBtn`)

Keep the sidebar toggle, the custom select, the filter and the page navigation unchanged. After editing, open the page with the browser console open: **there must be zero errors.**

---

## 14. Layout, components, accessibility

### 14.1 Responsive behaviour
The template's breakpoints stay as they are. Check the page at **375px, 768px, 1024px and 1440px** wide:
- There's no horizontal scrolling at any width.
- On phones the navbar sits at the bottom, as in the template, and the "Show Contacts" toggle opens and closes the contacts.
- From 1250px up, the sidebar sits beside the content and shows the contacts permanently, as in the template.

### 14.2 New CSS
Append the new classes at the end of `style.css`, under a comment `/* #CUSTOM — Amirhesam */`:
`.status-line`, `.status-dot`, `.news-list`, `.chip-list`, `.chip`, `.affiliation-chip`, `.cv-button`, `.seeking-card`, `.research-card`, `.research-card-title`, `.research-card-context`, `.research-card-list`, `.card-link`, `.project-card`, `.project-card-category` (12px, weight 600, accent), `.project-card-title` (15px, weight 500, heading colour), `.project-card-text` (13px), `.project-card-link`.

`.project-card`: `height: 100%`, a white background, a 1px `--jet` border, 16px radius, 20px padding, `box-shadow: 0 1px 2px rgba(16,24,40,.04), 0 6px 18px rgba(16,24,40,.05)`, and a flex column with a 6px gap.

### 14.3 Accessibility
- Every image has a meaningful `alt`, and every decorative `ion-icon` has `aria-hidden="true"`.
- Icon-only links have an `aria-label` (for example `aria-label="GitHub profile"`).
- Every external link has `target="_blank" rel="noopener"`.
- The whole page works with the keyboard alone (Tab, Enter), and focus is visible.
- Touch targets are at least 44px high.

---

## 15. Still needed from Amirhesam (keep as TODO placeholders until supplied)

| Item | Where it goes | Status |
|---|---|---|
| CV PDF for the public site (recommended: a copy **without the phone number**) | `assets/files/Amirhesam_Torkashvand_CV.pdf` | TODO |
| Repo URL: Semantic Correspondence | Research card 2, Projects #2 | TODO |
| Repo URL: Subgroup Faithfulness (and the Streamlit demo URL, optional) | Research card 3, Projects #4 | TODO |
| Repo URL: Agentic Research Assistant | Projects #5 | TODO |
| Repo URL: Multi-Agent Fraud Detection | Projects #6 | TODO |
| Repo URL: MALTO Qwen 2.5 classification | Projects #7 | TODO |
| Photo | `assets/images/avatar.jpg` | ✅ supplied |

---

## 16. Checks before publishing

Serve the site locally (for example `python3 -m http.server 8000`) and confirm each of these:

- [ ] The About tab shows on load; all four tabs switch correctly; and the page scrolls to the top on each switch.
- [ ] All five Projects filters work, both the buttons (wide screens) and the select box (narrow screens).
- [ ] Every Projects card has the same width and stays inside the white panel at every width in section 14.1.
- [ ] The browser console shows zero errors and zero 404s (no requests to deleted template images).
- [ ] No demo content is left: search the files for `Richard`, `Lorem`, `Nemo enim`, `example.com`, `Daniel`, `Jessica`, `Finance`, `Orizon`, `Brawlhalla`.
- [ ] The phone number is nowhere: search every file for `tel:` and for the phone number printed on the CV.
- [ ] Every fact and number on the page matches this plan exactly (its content was checked against the CV and Amirhesam's updates).
- [ ] Islamic Azad University is **not** listed under Affiliations.
- [ ] Every link opens the right target, and external links open in a new tab.
- [ ] The light theme is applied everywhere, with no dark panels left (check the navbar, the select dropdown and the scrollbar).
- [ ] A Lighthouse check in Chrome DevTools scores Accessibility ≥ 95 and Performance ≥ 90 on mobile.

---

## 17. Publish on GitHub Pages

1. Commit to `main` in `Hesam-AHT/Hesam-AHT.github.io` with a clear message, for example "Build portfolio site from approved design".
2. On GitHub, go to **Settings → Pages**: set **Source** to "Deploy from a branch", **Branch** to `main`, and the folder to `/ (root)`. Save.
3. Wait for the "pages build and deployment" run in the **Actions** tab to finish. It usually takes 1–2 minutes.
4. Open https://hesam-aht.github.io and repeat the checks in section 16 on the live site, including on a phone.

Later updates: edit, commit and push to `main`, and the site redeploys automatically.

---

## 18. README.md

```markdown
# Amirhesam Torkashvand — personal site

Source for https://hesam-aht.github.io — M.Sc. student in AI & Data Analytics at Politecnico di Torino.

Built with plain HTML, CSS and JavaScript, hosted on GitHub Pages.

Based on the [vCard personal portfolio template](https://github.com/codewithsadee/vcard-personal-portfolio) by codewithsadee (MIT License — see `LICENSE`).
```

---

## 19. CLAUDE.md (for future updates)

Create `CLAUDE.md` at the repository root with exactly this content. Claude reads this file automatically whenever it works in this repository, so later edits follow the same rules without anyone needing to repeat them.

```markdown
# Rules for editing this site

This is Amirhesam Torkashvand's portfolio, live at https://hesam-aht.github.io.
It's plain HTML, CSS and JavaScript on GitHub Pages (branch `main`, root folder), with no build step.
Pushing to `main` publishes the change in a minute or two.

## Where things are (all in index.html)
- Profile card and contacts: `<aside class="sidebar">`
- Tabs: four `<article data-page="…">` blocks, in order: about, resume, research, projects
- News: About tab, "News & updates" list, newest first, format `Mon YYYY · text`
- Resume entries: Resume tab, `li.timeline-item` in the Education, Experience or Teaching timeline, newest first
- Research write-ups: Research tab, one card per project
- Project cards: Projects tab, one `li.project-item` each. Its `data-category` must be one of
  `computer vision`, `trustworthy ai`, `agentic ai`, `nlp`. A new category also needs a matching
  filter button AND select item, with the same text.
- CV: `assets/files/Amirhesam_Torkashvand_CV.pdf`. Photo: `assets/images/avatar.jpg`

## Rules
- Never add a phone number anywhere.
- Never invent results, numbers, dates or skills. Use only what Amirhesam provides.
- Keep the light theme: colours live in `:root` of `assets/css/style.css`, accent `#9a6700`.
- A nav button's text, lower-cased, must equal its article's `data-page`, and buttons and articles
  must stay in the same order (script.js depends on this).
- Keep `LICENSE` unchanged (MIT, vCard template by codewithsadee).

## After every change
1. Serve locally (`python3 -m http.server 8000`): zero console errors, all tabs and filters work,
   nothing overflows at 375px and 1440px wide.
2. Commit to `main` with a clear message, then check the live site.
```
