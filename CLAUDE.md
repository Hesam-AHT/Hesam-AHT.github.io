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
