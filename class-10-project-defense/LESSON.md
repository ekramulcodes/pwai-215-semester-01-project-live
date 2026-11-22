# ক্লাস ১.১০: সেমিস্টার ১ প্রজেক্ট ডিফেন্স, পোর্টফোলিও রিভিউ ও ফাইনাল এক্সাম

| | |
|---|---|
| **You will type** | Small polish: social-share tags + favicon (5 lines per page), `loading="lazy"`, `404.html` (~20 lines) |
| **Start from** | `class-09-service-packages/project` |
| **End result** | `class-10-project-defense/project` = the **final Semester 01 project** |
| **Time plan** | 30 min final polish (live) · 20 min Lighthouse audit · 60+ min defenses · final exam (separate slot) |

---

## Part A – Final polish, live (30 min)

### 1 · Social sharing + favicon (in every page's `<head>`)
```html
  <meta property="og:title" content="Ekramul Islam – Front-End Developer">
  <meta property="og:description" content="Fast, responsive websites with HTML5 and Tailwind CSS.">
  <meta property="og:image" content="https://your-site.netlify.app/assets/images/avatar.svg">
  <link rel="icon" href="assets/images/favicon.svg" type="image/svg+xml">
```
- `og:` = **Open Graph** – the title/image Facebook, LinkedIn and WhatsApp show when someone shares your link.
  `og:image` must be a **full URL** (use a PNG/JPG 1200×630 for best results).
- `rel="icon"` = the small logo on the browser tab.

> Test: paste your live URL into a WhatsApp chat → preview appears.

### 2 · Lazy-load images below the fold
```html
<img src="assets/images/restaurant.svg" ... loading="lazy" ...>
```
- The browser downloads the image only when the user scrolls near it → faster first load.
- **Don't** lazy-load the hero image (it's visible immediately).

### 3 · Custom 404 page (`public/404.html`)
```html
  <main class="grid min-h-screen place-items-center px-4 text-center">
    <div>
      <p class="text-7xl font-bold text-brand-600">404</p>
      <h1 class="mt-4 text-3xl">Page not found</h1>
      <p class="mt-2">Sorry, this page doesn't exist.</p>
      <a href="index.html" class="btn-primary mt-8">Back to home</a>
    </div>
  </main>
```
- `grid place-items-center min-h-screen` = perfect centring on the full screen (2 classes!).
- Netlify automatically shows `404.html` for wrong URLs. Test: `your-site.netlify.app/abc`.

## Part B – Lighthouse audit together (20 min)
DevTools → **Lighthouse** → Mobile → Analyze. Fix the top issues live. Typical ones:

| Issue | Fix |
|-------|-----|
| Image elements do not have explicit width/height | add `width` + `height` |
| Links do not have a discernible name | add `sr-only` text to icon links/buttons |
| Background and foreground colours do not have enough contrast | darker text, e.g. `text-slate-500` → `text-slate-600` |
| Document does not have a meta description | add `<meta name="description">` |

Target: **90+ in all 4 categories.**

## Part C – Project defense format (per student, ~8 min)

| Time | What the student does |
|------|----------------------|
| 2 min | Show the **live site** on desktop and phone width |
| 2 min | Walk through the **folder structure** and `tailwind.config.js` |
| 2 min | Teacher points at **any 5 lines** → student explains them |
| 1 min | Show GitHub commit history + Netlify form submission |
| 1 min | Show gig text and packages |

Marking: `docs/defense/rubric.md` · Questions: `docs/defense/viva-questions.md`
Students check themselves first with `docs/defense/checklist.md`.

## Portfolio review – what makes a portfolio "hireable"
- Real projects (even practice ones) with **live links** – not just screenshots
- Short case study per project: problem → solution → result
- Clear "Hire me" path: packages → contact form
- Fast, works on mobile, no broken links
- Professional email and photo

## Final exam idea (60–90 min, individual)
Give a screenshot of a simple section (e.g. a team section or a newsletter box). Students must build it with
semantic HTML5 + Tailwind, responsive at 3 breakpoints, push to GitHub, and submit the live link.
