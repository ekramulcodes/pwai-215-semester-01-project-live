# ক্লাস ১.৩ : CSS3 ও Tailwind CSS-এর সূচনা

| | |
|---|---|
| **You will type** | `package.json` (via npm), `tailwind.config.js` (~25 lines), `src/input.css` (~25 lines), classes on `index.html` |
| **Start from** | `class-02-forms-media/project` |
| **End result** | `class-03-tailwind-intro/project` |
| **Needs** | Node.js 18+ installed · VS Code extension **Tailwind CSS IntelliSense** |
| **Time plan** | 20 min CSS3 recap · 25 min setup · 50 min styling · 10 min homework |

---

## Part A – CSS3 recap in 20 min (scratch file, not saved in the project)

Make `playground.html` and show these 5 ideas with plain CSS:

```html
<style>
  .box {
    padding: 20px;            /* space inside   */
    margin: 20px;             /* space outside  */
    border: 2px solid blue;   /* the edge       */
    border-radius: 12px;      /* rounded corners (CSS3) */
    transition: transform 0.3s;   /* smooth change (CSS3) */
  }
  .box:hover { transform: scale(1.05); }       /* pseudo-class */
  @media (min-width: 768px) { .box { padding: 40px; } }  /* responsive */
</style>
<div class="box">Hover me</div>
```

> Say: "Tailwind is **not a new language**. Every Tailwind class is just one of these CSS lines with a short name.
> `p-5` = `padding: 1.25rem`, `rounded-xl` = `border-radius: 0.75rem`, `hover:scale-105` = the hover rule above."

---

## Part B – Install Tailwind CLI (25 min)

> Why not the CDN `<script>`? The CDN is for experiments – it is slow and Tailwind says "not for production".
> The CLI creates a **small, real CSS file** with only the classes you used.

### Step 1 · Terminal (in the project folder)
```bash
npm init -y
```
```bash
npm install -D tailwindcss@3
```
```bash
npx tailwindcss init
```

| Command | Explain |
|---------|---------|
| `npm init -y` | Creates `package.json` – the project's "ID card" (name, scripts, tools). |
| `npm install -D tailwindcss@3` | Downloads Tailwind into `node_modules`. `-D` = only needed while developing. `@3` = version 3. |
| `npx tailwindcss init` | Creates `tailwind.config.js`. |

### Step 2 · `tailwind.config.js`
```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ['./public/**/*.html'],
  theme: {
    extend: {
      colors: {
        brand: {
          50: '#eef6ff',
          100: '#d9eaff',
          500: '#337dff',
          600: '#1b5ef5',
          700: '#1449e1',
          900: '#19378f',
        },
      },
      fontFamily: {
        sans: ['Inter', 'sans-serif'],
        display: ['Poppins', 'sans-serif'],
      },
    },
  },
  plugins: [],
};
```

| Line | Explain |
|------|---------|
| `content` | **Most important line.** Tailwind reads these files and only creates CSS for classes it finds. `**` = all sub-folders. Wrong path = no styles! |
| `theme.extend` | **Add** to Tailwind's defaults (without `extend` you would **replace** them and lose all default colours). |
| `colors.brand` | Our own colour → we can now write `bg-brand-600`, `text-brand-500`… Change it once, the whole site changes. |
| `fontFamily.display` | Creates the class `font-display`. |

### Step 3 · `src/input.css`
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```
- `base` = reset (removes browser default margins, list bullets, heading sizes – **show the page now: everything looks "plain"**)
- `components` = our reusable classes like `.btn`
- `utilities` = all the small classes like `p-4`, `text-xl`

### Step 4 · Scripts in `package.json`
```json
  "scripts": {
    "dev": "tailwindcss -i ./src/input.css -o ./public/assets/css/style.css --watch",
    "build": "tailwindcss -i ./src/input.css -o ./public/assets/css/style.css --minify"
  },
```
- `-i` = input file (we write), `-o` = output file (browser reads). **Never edit the output file.**
- `--watch` = rebuild automatically every time you save. `--minify` = smallest file for going live.

```bash
npm run dev
```
Keep this terminal open all class.

### Step 5 · Link the CSS + fonts in every page's `<head>`
```html
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&amp;family=Poppins:wght@600;700&amp;display=swap">
  <link rel="stylesheet" href="assets/css/style.css">
```

---

## Part C – Style the page (50 min)

### Step 6 · Base styles with `@layer base` (add to `input.css`)
```css
@layer base {
  body {
    @apply font-sans text-slate-700;
  }
  h1, h2, h3 {
    @apply font-display font-semibold text-slate-900;
  }
}
```
- `@layer base` = default style for plain HTML tags.
- `@apply` = "use these Tailwind classes inside my CSS".

### Step 7 · Our first component – a button (CSS3 + Tailwind together)
```css
@layer components {
  .btn {
    display: inline-block;
    padding: 0.75rem 1.5rem;
    border-radius: 0.75rem;
    font-weight: 600;
    transition: background-color 0.2s ease, transform 0.2s ease;
  }
  .btn-primary {
    @apply btn bg-brand-600 text-white hover:bg-brand-700;
  }
}
```
> Say: "`.btn` is **plain CSS3**. `.btn-primary` uses **@apply**. Both are valid – this is how they work together.
> Rule: make a component only for things you repeat many times (buttons, cards). Everything else: classes in HTML."

### Step 8 · Hero section – read each class aloud
```html
    <section id="hero" class="mx-auto max-w-6xl px-4 py-20">
      <h1 class="text-4xl font-bold leading-tight md:text-6xl">I build <span class="text-brand-600">fast, modern</span> websites</h1>
      <p class="mt-6 max-w-xl text-lg">Hi, I'm Ekramul – ...</p>
      <a href="contact.html" class="btn-primary mt-8">Hire me</a>
      <img src="assets/images/avatar.svg" alt="..." width="400" height="400" class="mt-10 w-64 rounded-3xl shadow-xl">
    </section>
```

| Class | CSS it makes | Meaning |
|-------|-------------|---------|
| `max-w-6xl` | `max-width: 72rem` | Content never gets wider than 1152px |
| `mx-auto` | `margin-left/right: auto` | Centre the box |
| `px-4` / `py-20` | padding left-right 1rem / top-bottom 5rem | Space inside |
| `text-4xl` | `font-size: 2.25rem` | Big text |
| `md:text-6xl` | same, but only from 768px | **Preview of responsive** (full lesson in 1.4) |
| `leading-tight` | `line-height: 1.25` | Lines closer together |
| `mt-6` | `margin-top: 1.5rem` | Space above |
| `max-w-xl` | `max-width: 36rem` | Short lines are easier to read |
| `rounded-3xl shadow-xl` | border-radius + box-shadow | CSS3 effects |

> **Number scale:** `1` = 0.25rem = 4px. So `p-4` = 16px, `mt-8` = 32px. Students only need to remember this one rule.

### Step 9 · Header, About, Projects, Footer
Type the classes for the header and the **first** project card together with students, then let them finish the
other two cards and the footer themselves (5 min). Compare with the final file.

```html
      <article class="mt-8 rounded-2xl border border-slate-200 p-6">
```
- `border border-slate-200` → 1px light-grey border. `hover:text-brand-600` on links → colour change on hover.

### Step 10 · Change the brand colour live
Change `600: '#1b5ef5'` to a green like `'#16a34a'` → save → the whole site changes. This is the power of a config.

✅ **Check:** Page has fonts, colours and spacing. Header links are still stacked and project cards are full width –
**that is expected**. Layout (Flexbox/Grid) is next class.

## Common mistakes
- Forgot `npm run dev` → new classes have no effect
- Wrong `content` path → no styles at all
- Editing `style.css` directly → your changes disappear on the next build
- Typos like `bg-blue600` (no error, just nothing happens – IntelliSense helps)

## Homework
1. Pick your own brand colour (use https://uicolors.app to make 50–900 shades).
2. Style `contact.html`: heading sizes, spacing, `btn-primary` on the submit button.
