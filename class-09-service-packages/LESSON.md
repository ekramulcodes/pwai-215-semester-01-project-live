# ক্লাস ১.৯ : ফ্রিল্যান্স সার্ভিস প্যাকেট ও অফার তৈরি

| | |
|---|---|
| **You will type** | Pricing section (~60 lines) + FAQ accordion (~30 lines) in `index.html`, "Services" menu link, `docs/packages.md` |
| **Start from** | `class-08-client-communication/project` |
| **End result** | `class-09-service-packages/project` |
| **Time plan** | 30 min business (no code) · 45 min pricing section · 20 min FAQ · 10 min homework |

---

## Part A – Designing packages (30 min, whiteboard)

**Why 3 packages?**
- **Basic** = low price, gets people in the door (deliberately limited)
- **Standard** = what you actually want to sell → mark it "Most popular"
- **Premium** = makes Standard look like a good deal (anchor)

> Most clients pick the middle one. That's why it's highlighted.

**How to set a price:**
```
hourly target × estimated hours + 20% buffer (revisions + messages)
$8 × 12 hours = $96 → + 20% = $115 → round to $120
```

**Live research:** open Fiverr, search "tailwind landing page", look at 3 sellers' packages together.
Fill `docs/packages.md` as a table with the class.

---

## Part B – Pricing section (45 min)

### Step 1 · Section + grid (add before the testimonials section)
```html
    <section id="services" class="py-20" aria-labelledby="services-title">
      <div class="mx-auto max-w-6xl px-4">
        <h2 id="services-title" class="text-center text-3xl">Services &amp; pricing</h2>
        <p class="mt-3 text-center">Fixed prices. Clear deliverables. No surprises.</p>

        <div class="mt-14 grid items-start gap-8 md:grid-cols-3">
          <!-- 3 cards go here -->
        </div>
      </div>
    </section>
```
> Recap from 1.4: `grid md:grid-cols-3` → 1 column on phones, 3 on tablets+.

### Step 2 · A normal card (Basic)
```html
          <article class="card flex flex-col">
            <h3 class="text-xl">Basic</h3>
            <p class="mt-2 text-sm">A simple one-page website.</p>
            <p class="mt-6"><span class="text-5xl font-bold text-slate-900">$50</span> / project</p>
            <p class="mt-1 text-sm">Delivery in 3 days</p>
            <ul class="mt-6 flex-1 space-y-3 text-sm">
              <li class="flex gap-2"><span class="text-brand-600" aria-hidden="true">✓</span> 1 landing page</li>
              <li class="flex gap-2"><span class="text-brand-600" aria-hidden="true">✓</span> Responsive design</li>
              <li class="flex gap-2"><span class="text-brand-600" aria-hidden="true">✓</span> Contact form</li>
              <li class="flex gap-2"><span class="text-brand-600" aria-hidden="true">✓</span> 1 revision</li>
            </ul>
            <a href="contact.html" class="btn mt-8 w-full border border-slate-300 text-center hover:border-brand-600">Choose Basic</a>
          </article>
```

| Code | Explain |
|------|---------|
| `card flex flex-col` | Reuse our card; children in a column. |
| `<span class="text-5xl">$50</span> / project` | Big price, small unit – `<span>` styles part of a line. |
| `flex-1` on the `<ul>` | List takes the extra space → all buttons line up at the bottom (same trick as 1.4). |
| `aria-hidden="true"` on ✓ | Screen readers don't need to say "check mark" each time. |
| `btn … w-full` | Re-use `.btn` from 1.3, full width. |

Copy it for **Premium** and change the text.

### Step 3 · The highlighted card (Standard)
```html
          <article class="relative rounded-3xl bg-brand-900 p-8 text-white shadow-2xl ring-2 ring-brand-500 flex flex-col md:-translate-y-4">
            <p class="absolute -top-3 left-1/2 -translate-x-1/2 rounded-full bg-amber-400 px-3 py-1 text-xs font-bold text-slate-900">MOST POPULAR</p>
            <h3 class="text-xl text-white">Standard</h3>
            ...
            <a href="contact.html" class="btn mt-8 w-full bg-white text-center text-brand-900 hover:bg-brand-50">Choose Standard</a>
          </article>
```

| Class | Explain |
|-------|---------|
| `bg-brand-900 text-white` | Dark card → it stands out. |
| `ring-2 ring-brand-500` | An outline ring (like a border, but doesn't change size). |
| `md:-translate-y-4` | Lifted 16px up – only on tablets+ (on phones, cards are stacked). |
| `relative` (parent) + `absolute` (badge) | **Positioning lesson:** the badge is placed relative to the card. |
| `-top-3` | Badge sticks out 12px above the card. |
| `left-1/2 -translate-x-1/2` | **The classic centring trick:** move the left edge to the middle, then pull back by half its own width. |

✅ **Check:** 3 cards, middle one lifted with the badge; on phones, stacked.

### Step 4 · Add "Services" to the menus
Add `<li><a href="#services" …>Services</a></li>` to the desktop and mobile menus (and `index.html#services` on `contact.html`).

---

## Part C – FAQ accordion with `<details>` (20 min)

```html
    <section id="faq" class="bg-slate-50 py-20" aria-labelledby="faq-title">
      <div class="mx-auto max-w-3xl px-4">
        <h2 id="faq-title" class="text-center text-3xl">Frequently asked questions</h2>
        <div class="mt-10 space-y-4">
          <details class="group card">
            <summary class="flex cursor-pointer list-none items-center justify-between font-semibold text-slate-900">
              What do you need from me to start?
              <span class="text-2xl text-brand-600 transition group-open:rotate-45" aria-hidden="true">+</span>
            </summary>
            <p class="mt-3">Your logo, text, images and 2–3 websites you like.</p>
          </details>
          <!-- copy for each question -->
        </div>
      </div>
    </section>
```

| Code | Explain |
|------|---------|
| `<details>` + `<summary>` | **HTML5 accordion – no JavaScript.** Click the summary → the rest opens/closes. Works with keyboard too. |
| `list-none` | Removes the default ▶ triangle. |
| `group` on details + `group-open:rotate-45` | When the `<details>` is open, rotate the `+` 45° → it becomes `×`. Same `group` trick as Class 1.6! |
| `cursor-pointer` | Shows the hand cursor so users know it's clickable. |

> Tip: FAQs answer the questions clients ask in messages → fewer messages, more orders.

## Part D – Commit and deploy
```bash
git add . && git commit -m "feat: add pricing packages and FAQ" && git push
```
Check the live site updated.

## Common mistakes
- Badge is placed relative to the whole page → forgot `relative` on the card
- Buttons at different heights → forgot `flex flex-col` + `flex-1`
- Prices on the website and on Fiverr don't match → keep `docs/packages.md` as the single source

## Homework
1. Set **your own** 3 packages based on research and update the website + `docs/packages.md`.
2. Add an "Add-ons" row under the pricing cards (grid of 4 small cards).
3. Publish your Fiverr gig with the 3 packages (gig text from Class 1.8).
