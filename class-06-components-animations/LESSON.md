# ক্লাস ১.৬ : Tailwind Advanced Components & Animations

| | |
|---|---|
| **You will type** | Mobile menu (~20 lines), 2 custom animations in config (~15 lines), hover effects, form error style |
| **Start from** | `class-05-ai-ui-to-tailwind/project` |
| **End result** | `class-06-components-animations/project` |
| **Time plan** | 10 min recap · 80 min live coding (4 mini-projects) · 15 min Q&A |

> Today we make the site feel "alive" – and we still write **zero JavaScript**.

---

## Mini-project 1 · Sticky glass header (5 min)

```html
  <header class="sticky top-0 z-40 border-b border-slate-200 bg-white/80 backdrop-blur">
```

| Class | Explain |
|-------|---------|
| `sticky top-0` | Header scrolls normally, then **sticks** to the top. |
| `z-40` | Stays **above** other content (higher z = closer to you). |
| `bg-white/80` | White with 80% opacity (the `/80`). |
| `backdrop-blur` | Blurs what's behind it → "glass" effect (CSS3 `backdrop-filter`). |

## Mini-project 2 · Mobile menu with the Popover API (25 min)

**Problem:** on phones, the menu is too wide. **Plan:** hide it on phones, show a ☰ button that opens a side panel.

### 2a. Hide the desktop menu on phones
```html
        <ul class="hidden gap-6 md:flex">
```
- `hidden` = `display: none` on phones. `md:flex` = show as flex from 768px.

### 2b. The ☰ button (after `</nav>`, inside the header's `<div>`)
```html
      <button type="button" popovertarget="mobile-menu" class="rounded-lg p-2 hover:bg-slate-100 md:hidden">
        <span class="sr-only">Open menu</span>
        <svg class="h-6 w-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M4 6h16M4 12h16M4 18h16"/></svg>
      </button>
```

| Code | Explain |
|------|---------|
| `popovertarget="mobile-menu"` | **HTML5 magic:** clicking this button opens/closes the element with `id="mobile-menu"`. No JavaScript! |
| `md:hidden` | Opposite of the menu: visible on phones, hidden from 768px. |
| `sr-only` text | The button has only an icon, so we give screen readers a text. |
| `<svg>` with `<path d="M4 6h16…">` | Three lines = ☰ icon. `M` = move to, `h16` = draw 16 to the right. `stroke="currentColor"` = same colour as the text. |

### 2c. The panel (after the `</div>`, still inside `<header>`)
```html
    <nav id="mobile-menu" popover aria-label="Mobile" class="m-0 ml-auto h-dvh w-64 bg-white p-6 shadow-2xl backdrop:bg-slate-900/50">
      <button type="button" popovertarget="mobile-menu" popovertargetaction="hide" class="mb-6 font-semibold">✕ Close</button>
      <ul class="space-y-4 text-lg">
        <li><a href="#about" class="hover:text-brand-600">About</a></li>
        <li><a href="#projects" class="hover:text-brand-600">Projects</a></li>
        <li><a href="contact.html" class="hover:text-brand-600">Contact</a></li>
      </ul>
    </nav>
```

| Code | Explain |
|------|---------|
| `popover` | Hidden by default; shown on top of everything when its button is clicked. Also closes with **Esc** or clicking outside – free accessibility! |
| `m-0 ml-auto` | Browsers centre popovers; this pushes it to the **right edge**. |
| `h-dvh` | Full screen height (dynamic viewport height – works with mobile browser bars). |
| `backdrop:bg-slate-900/50` | `backdrop:` styles the dark layer behind the popover. |
| `popovertargetaction="hide"` | This button only **closes**. |
| `space-y-4` | Vertical space between list items. |

✅ **Check:** DevTools → 375px → click ☰ → panel slides in. Click outside or press Esc → closes.

> Copy the same code into `contact.html` (links become `index.html#about`, `index.html#projects`).

## Mini-project 3 · Hover effects with `group` (20 min)

### 3a. Button lift + press (in `input.css`)
```css
  .btn-primary {
    @apply btn bg-brand-600 text-white hover:-translate-y-0.5 hover:bg-brand-700 active:scale-95;
  }
```
- `hover:-translate-y-0.5` = move up 2px on hover. `active:scale-95` = shrink a little while clicking (feels like a real button).
- The smooth motion comes from `transition` we wrote in `.btn` in Class 1.3.

### 3b. Card lift
```css
  .card {
    @apply rounded-2xl border border-slate-200 bg-white p-6 transition duration-300 hover:-translate-y-1 hover:shadow-xl;
  }
```

### 3c. Zoom the image when hovering the **card** – the `group` trick
```html
        <article class="card group flex flex-col">
          <figure class="overflow-hidden rounded-xl">
            <img ... class="transition duration-500 group-hover:scale-110">
```

| Class | Explain |
|-------|---------|
| `group` on the parent | Marks the card as a "group". |
| `group-hover:scale-110` on the child | "When the **parent** is hovered, zoom **me** 110%". Normal `hover:` would only work when hovering the image itself. |
| `overflow-hidden` on the figure | Cuts off the zoomed part so the image stays inside its rounded box. |

## Mini-project 4 · Custom animations (20 min)

Tailwind has `animate-spin`, `animate-pulse`, `animate-bounce`. We'll create **our own** in `tailwind.config.js` → inside `extend`:

```js
      keyframes: {
        'fade-up': {
          '0%': { opacity: '0', transform: 'translateY(24px)' },
          '100%': { opacity: '1', transform: 'translateY(0)' },
        },
        float: {
          '0%, 100%': { transform: 'translateY(0)' },
          '50%': { transform: 'translateY(-12px)' },
        },
      },
      animation: {
        'fade-up': 'fade-up 0.8s ease-out both',
        float: 'float 5s ease-in-out infinite',
      },
```

| Part | Explain |
|------|---------|
| `keyframes` | The **steps** of the movement (CSS3 `@keyframes`). `0%` = start, `100%` = end. |
| `fade-up` | Starts invisible and 24px lower → ends visible in place. |
| `float` | Up and down forever. |
| `animation` | Creates the class `animate-fade-up` = name + duration + easing + repeat. |
| `both` | Keep the start style before and the end style after. |
| `infinite` | Repeat forever. |

Use them in the hero:
```html
      <div class="animate-fade-up">           <!-- text -->
      <img ... class="... animate-float ...">  <!-- photo -->
```

### Accessibility: respect "reduce motion" (bottom of `input.css`)
```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation: none !important;
    transition: none !important;
  }
}
```
> Some people get dizzy from animations and turn them off in their phone/OS settings. This rule respects that.

## Bonus (if time) · Friendly form errors (5 min)
```css
  .form-input:user-invalid {
    @apply border-red-500;
  }
```
- `:user-invalid` = invalid **after the user has typed/left the field**. (`:invalid` would make the form red before the user even starts.)

## Common mistakes
- Forgot `group` on the parent → `group-hover:` does nothing
- `popovertarget` and `id` spelled differently → button does nothing
- Restart `npm run dev` after changing `tailwind.config.js` if new classes don't appear
- Too many animations → looks cheap. Rule: 1–2 animations per page.

## Homework
1. Make a "Back to top" link (`href="#hero"`) fixed at the bottom-right (`fixed bottom-6 right-6`) with a hover animation.
2. Create your own keyframe animation (e.g. `wiggle`) and use it on the "Hire me" button on hover only (`hover:animate-wiggle`).
