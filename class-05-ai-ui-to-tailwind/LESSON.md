# ক্লাস ১.৫ : AI Tools দিয়ে UI/UX জেনারেট এবং Tailwind-এ রূপান্তর

| | |
|---|---|
| **You will type** | One new section in `index.html` (~45 lines), by **fixing** AI code |
| **Start from** | `class-04-flexbox-grid/project` |
| **Also open** | `class-05-ai-ui-to-tailwind/ai-raw-output.html` (the AI's answer, with problems) |
| **End result** | `class-05-ai-ui-to-tailwind/project` |
| **Time plan** | 15 min AI workflow · 15 min live prompting · 50 min review + refactor · 15 min students try |

---

## Part A – The workflow (15 min)

```
1. BRIEF     → write clearly what you need
2. GENERATE  → ask the AI (ChatGPT, Claude, Gemini, v0.dev …)
3. REVIEW    → find problems with a checklist
4. REFACTOR  → fix it so it matches OUR project
5. TEST      → responsive + validator
```

> Say: "AI is a fast junior developer. It writes code quickly, but **you** are the senior who reviews it.
> In the project defense you must explain every line – including the lines the AI wrote."

## Part B – Live prompting (15 min)

Write this prompt **in front of students** – explain each line of the prompt:

```
Create a testimonials section for a freelance web developer portfolio.
Use HTML5 semantic tags and Tailwind CSS v3 classes only. No JavaScript.
- Heading: "What clients say"
- 3 testimonial cards: star rating, quote, client name, client role
- Mobile-first: 1 column on phones, 3 columns from md
- Use only these colours: brand-50 to brand-900, slate, amber-400
- Accessible: correct semantic tags for quotes, screen-reader text for the stars
```

| Prompt line | Why |
|-------------|-----|
| "HTML5 semantic … Tailwind v3" | Without it, AI may give React, Bootstrap or Tailwind v4 code. |
| "No JavaScript" | We haven't learned JS. |
| Exact content list | Vague prompt = random result. |
| "Mobile-first … columns" | Otherwise AI often uses fixed widths. |
| "Only these colours" | Keeps our brand consistent. |
| "Accessible" | AI forgets this unless asked. |

Show that **a vague prompt** ("make a testimonial section") gives worse code – that's what `ai-raw-output.html` looks like.

## Part C – Review the AI code (20 min)

Open `ai-raw-output.html`. Ask students to find problems before you show the list.

| # | Problem in AI code | Why it's bad | Fix |
|---|-------------------|--------------|-----|
| 1 | `<div>` everywhere | No meaning for Google/screen readers | `<section>`, `<h2>`, `<figure>`, `<blockquote>`, `<cite>` |
| 2 | Heading is a `<div>` | Page outline is broken | `<h2>` |
| 3 | `style="padding: 80px 0;"` | Inline CSS mixed with Tailwind | `py-20` |
| 4 | `text-[#1e3a8a]` | Random colour, not our brand | `text-slate-900` / `bg-brand-900` |
| 5 | `w-[400px]` + `flex` | Breaks on phones (3×400px!) | `grid md:grid-cols-3` |
| 6 | `<img>` with no `alt`, `width`, `height` | Accessibility + layout jump | Remove photos (we don't have real ones) |
| 7 | Photos from `randomuser.me` | Fake people on a real portfolio = unethical | Names only, or real client photos with permission |
| 8 | "★★★★★" read aloud as "star star star…" | Bad for screen readers | `sr-only` text + `aria-hidden` |
| 9 | Same card classes repeated | We already have `.card` | `class="card"` |

✅ Show it at 375px wide in DevTools → horizontal scroll. Proof that AI code needs review.

## Part D – Refactor live (30 min)

Add after the projects section, before `</main>`:

```html
    <section id="testimonials" class="bg-brand-900 py-20" aria-labelledby="testimonials-title">
      <div class="mx-auto max-w-6xl px-4">
        <h2 id="testimonials-title" class="text-center text-3xl text-white">What clients say</h2>

        <div class="mt-10 grid gap-6 md:grid-cols-3">
          <figure class="card">
            <p class="text-amber-400"><span class="sr-only">Rated 5 out of 5</span><span aria-hidden="true">★★★★★</span></p>
            <blockquote class="mt-4">
              <p>"Ekramul delivered our restaurant site two days early. Mobile view is perfect!"</p>
            </blockquote>
            <figcaption class="mt-6">
              <cite class="font-semibold not-italic text-slate-900">Karim Uddin</cite>
              <span class="block text-sm text-slate-500">Owner, Spice Garden</span>
            </figcaption>
          </figure>
          <!-- copy the figure 2 more times and change the text -->
        </div>
      </div>
    </section>
```

| Code | Explain |
|------|---------|
| `aria-labelledby="testimonials-title"` | The section's name = the text of the `<h2>` with that id. |
| `<figure>` + `<blockquote>` + `<figcaption>` + `<cite>` | The correct HTML for "a quote and who said it". |
| `sr-only` | Tailwind class: hidden on screen, but screen readers read it. |
| `aria-hidden="true"` | Screen readers skip the stars. |
| `not-italic` | `<cite>` is italic by default; we remove it. |
| `block` on the role `<span>` | Puts the role on its own line. |
| `class="card"` | Reusing our component – AI didn't know it exists. |

## Part E – Students try (15 min)
Each student prompts an AI for a **"My process" section** (4 steps: Discuss → Design → Develop → Deliver),
then reviews it with the 9-point table above. 2–3 students share their screen and explain what they fixed.

## Good AI tools for UI
- **ChatGPT / Claude / Gemini** – code from a text prompt or a screenshot
- **v0.dev** – generates UI visually, then export the code
- **Figma AI / Uizard** – generate design mockups first

## Homework
1. Add the "My process" section to your portfolio (use `<ol>` – steps have an order!).
2. Take a screenshot of any website you like, ask AI to convert it to Tailwind, and write down **5 problems** you fixed.
