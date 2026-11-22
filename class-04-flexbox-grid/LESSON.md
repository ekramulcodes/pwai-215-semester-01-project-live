# ক্লাস ১.৪ : Tailwind Flexbox, Grid ও রেসপন্সিভ লেআউট Design

| | |
|---|---|
| **You will type** | Layout classes + a few wrapper `<div>`s in both pages, `.card` and `.form-input` components |
| **Start from** | `class-03-tailwind-intro/project` |
| **End result** | `class-04-flexbox-grid/project` |
| **Time plan** | 15 min theory · 75 min live coding · 15 min device testing |

---

## Part A – Theory (15 min, whiteboard)

```
FLEXBOX = one direction (a row OR a column)      GRID = rows AND columns together
[logo]              [About][Projects][Contact]    [card][card][card]
                                                  [card][card][card]
Use for: navbars, buttons in a row, centering     Use for: card lists, page layouts
```

**Mobile-first rule:** classes without a prefix = **all screens**. Prefixes mean "**from this width and up**":

| Prefix | Starts at | Device |
|--------|-----------|--------|
| (none) | 0px | phones |
| `sm:` | 640px | large phones |
| `md:` | 768px | tablets |
| `lg:` | 1024px | laptops |

> So `grid sm:grid-cols-2 lg:grid-cols-3` reads: "1 column on phones, 2 from 640px, 3 from 1024px".

Open DevTools → device toolbar (Ctrl + Shift + M) and keep it open all class.

---

## Part B – Live coding

### Step 1 · Navbar with Flexbox (15 min)
We need a wrapper `<div>` so the background stays full width but the content is centred.

```html
  <header class="border-b border-slate-200 bg-white">
    <div class="mx-auto flex max-w-6xl flex-wrap items-center justify-between gap-4 px-4 py-4">
      <a href="index.html" class="...">Ekramul<span class="text-brand-600">.dev</span></a>
      <nav aria-label="Main">
        <ul class="flex gap-6">
          ...
        </ul>
      </nav>
    </div>
  </header>
```

| Class | Explain |
|-------|---------|
| `flex` | Children (logo + nav) sit **in a row**. |
| `items-center` | Centre them **vertically**. |
| `justify-between` | Push them to the **two ends** (logo left, menu right). |
| `flex-wrap` | On very small screens, the menu can wrap to the next line instead of overflowing. |
| `gap-4` / `gap-6` | Space **between** items (better than margin on each item). |
| `<ul class="flex">` | The list items also sit in a row. |

> Demo: remove `justify-between` → everything sticks left. Try `justify-center`, `justify-end`.

### Step 2 · Hero with Grid (15 min)
Wrap the text in a `<div>` so the hero has **two children**: text and image.

```html
    <section id="hero" class="mx-auto grid max-w-6xl items-center gap-12 px-4 py-20 md:grid-cols-2">
      <div>
        <h1 ...>...</h1>
        <p ...>...</p>
        <a ...>Hire me</a>
      </div>
      <img ... class="mx-auto w-full max-w-sm rounded-3xl shadow-xl">
    </section>
```

| Class | Explain |
|-------|---------|
| `grid` | Turn on grid. Default = 1 column (phone: text on top, image below). |
| `md:grid-cols-2` | From tablet: 2 equal columns side by side. |
| `items-center` | Vertically centre the text next to the image. |
| `w-full max-w-sm` | Image fills its column but never bigger than 24rem. |

✅ **Check:** drag the DevTools width from 375px to 1200px and watch the layout switch at 768px.

### Step 3 · Skills as badges with `flex-wrap` (5 min)
```html
          <ul class="mt-3 flex flex-wrap gap-2">
            <li class="rounded-full bg-white px-4 py-1 text-sm shadow-sm">HTML5</li>
```
- `flex-wrap` → badges go to the next line when there's no space.

### Step 4 · About as 2 columns on laptop (5 min)
Inner `<div class="mx-auto grid max-w-6xl gap-12 px-4 lg:grid-cols-2">` with two `<div>`s: text | video.
Add `aspect-video` to the video → always 16:9.

### Step 5 · Project cards grid (15 min)
First make a `.card` component in `input.css` (we repeat it 3+ times):

```css
  .card {
    @apply rounded-2xl border border-slate-200 bg-white p-6;
  }
```

Then wrap the three `<article>`s:

```html
      <div class="mt-8 grid gap-6 sm:grid-cols-2 lg:grid-cols-3">
        <article class="card flex flex-col">
          ...
          <p class="mt-2 flex-1">...</p>
          <a ...>Live demo</a>
        </article>
```

| Class | Explain |
|-------|---------|
| `grid gap-6 sm:grid-cols-2 lg:grid-cols-3` | 1 → 2 → 3 columns. **The most used layout on the internet.** |
| `flex flex-col` on the card | Card children stacked in a column… |
| `flex-1` on the paragraph | …the paragraph takes all extra space, so every "Live demo" link lines up at the bottom even if texts are different lengths. |

### Step 6 · Footer: column on phone, row on desktop (5 min)
```html
    <div class="mx-auto flex max-w-6xl flex-col items-center justify-between gap-2 px-4 py-8 sm:flex-row">
```
- `flex-col` (phone) → `sm:flex-row` (bigger). Very common pattern.

### Step 7 · Contact form layout (15 min)
Install the official forms plugin (it gives nice default form styles):
```bash
npm install -D @tailwindcss/forms
```
`tailwind.config.js` → `plugins: [require('@tailwindcss/forms')],` – restart `npm run dev`.

Add a component:
```css
  .form-input {
    @apply mt-1 block w-full rounded-xl border-slate-300 focus:border-brand-500 focus:ring-brand-500;
  }
```

Layout ideas (see final `contact.html`):
- Page: `grid lg:grid-cols-3` → info + map in 1 column, form takes `lg:col-span-2`.
- Each `<fieldset class="grid gap-5 sm:grid-cols-2">` → two fields per row.
- Wrap every label + input pair in a `<div>` (one grid cell each).
- Long fields (phone, package, message) get `sm:col-span-2` → full row.
- Radio buttons: `<div class="flex flex-wrap gap-6">`.

---

## Part C – Device testing (15 min)
Check both pages at **360px, 768px, 1280px**. Rule: **no horizontal scrollbar** ever.
Then open the Live Server URL on your phone (same Wi-Fi: use the computer's IP, e.g. `http://192.168.0.5:5500`).

## Common mistakes
- Putting `md:` on the **wrong** class: `md:grid` + `grid-cols-2` ❌ → `grid md:grid-cols-2` ✅
- Forgetting the wrapper `<div>` → grid has 4 children instead of 2
- Using fixed widths like `w-[500px]` → breaks on phones (use `w-full max-w-…`)

## Homework
1. Make the "Skills" list a 2-column grid on phones and 4 columns on laptops (instead of badges) – then decide which looks better.
2. Add a 4th project card – the grid should handle it automatically.
