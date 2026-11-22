# ক্লাস ১.১ : ওয়েব পরিচিতি, HTML5 ফান্ডামেন্টালস ও সেমান্টিক ট্যাগ

| | |
|---|---|
| **You will type** | 1 file: `public/index.html` (~85 lines) |
| **Start from** | `class-00-starter/project` (only images) |
| **End result** | `class-01-html5-semantics/project` |
| **Time plan** | 20 min theory · 60 min live coding · 15 min Q&A · 10 min homework |

---

## Part A – Theory (20 min, no code)

Draw this on the whiteboard:

```
You type URL → Browser asks DNS "where is nadia.dev?" → DNS gives IP
→ Browser asks the server → Server sends back HTML, CSS, JS, images → Browser draws the page
```

- **HTML** = structure (the skeleton) · **CSS** = design (the clothes) · **JS** = behaviour (the muscles)
- **Semantic tag** = a tag whose *name explains its meaning*. `<nav>` tells Google and screen readers "this is navigation". `<div>` says nothing.

---

## Part B – Live coding

### Step 1 · Open the project (2 min)
Open `class-00-starter/project` in VS Code. Show the `public/assets/images` folder.

> Say: "`public` is the folder visitors will see. Everything inside it goes online."

Create `public/index.html`.

### Step 2 · The HTML5 skeleton (10 min)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ekramul Islam – Front-End Developer</title>
  <meta name="description" content="Freelance front-end developer building fast, responsive websites.">
</head>
<body>

</body>
</html>
```

| Line | Explain |
|------|---------|
| `<!DOCTYPE html>` | Tells the browser "this is modern HTML5". Always line 1. |
| `<html lang="en">` | Root of the page. `lang` helps Google and screen readers (use `bn` for a Bangla site). |
| `<head>` | Information **about** the page – not shown on screen. |
| `<meta charset="UTF-8">` | Lets the page show every language's letters (Bangla, emoji ✓). |
| `<meta name="viewport" ...>` | Makes the page fit mobile screens. Without it, phones show a tiny zoomed-out desktop page. |
| `<title>` | Text on the browser tab and the blue link in Google results. |
| `<meta name="description">` | The grey text under the link in Google results. |
| `<body>` | Everything visible goes here. |

> Shortcut: in VS Code type `!` then press **Tab** – Emmet writes the skeleton. Type it by hand the first time.

✅ **Check:** Open with Live Server → blank page, tab shows the title.

### Step 3 · Header and navigation (8 min)

```html
  <header>
    <a href="index.html">Ekramul.dev</a>
    <nav aria-label="Main">
      <ul>
        <li><a href="#about">About</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="contact.html">Contact</a></li>
      </ul>
    </nav>
  </header>
```

| Line | Explain |
|------|---------|
| `<header>` | The top area of the page (logo + menu). |
| `<a href="index.html">` | The logo is a link back to the home page – every website does this. |
| `<nav aria-label="Main">` | Main navigation. `aria-label` gives it a name for screen readers. |
| `<ul>` / `<li>` | A menu is a **list of links**, so we use a list. |
| `href="#about"` | `#` = jump to the element with `id="about"` on the **same page**. |
| `href="contact.html"` | Goes to **another page** (we build it in Class 1.2). |

### Step 4 · Main + hero section (8 min)

```html
  <main>
    <section id="hero">
      <h1>I build fast, modern websites</h1>
      <p>Hi, I'm Ekramul – a front-end developer from Dhaka. I turn ideas into responsive websites.</p>
      <a href="contact.html">Hire me</a>
      <img src="assets/images/avatar.svg" alt="Portrait of Ekramul Islam" width="400" height="400">
    </section>
  </main>
```

| Line | Explain |
|------|---------|
| `<main>` | The unique content of this page. **Only one** per page. |
| `<section id="hero">` | A themed block. The "hero" is the big first block of a website. |
| `<h1>` | The most important heading. **Only one `<h1>` per page** – Google reads it as the page topic. |
| `<img src alt width height>` | `alt` = text for blind users and if the image fails. `width/height` stop the page "jumping" while loading. |

### Step 5 · About section (7 min)

```html
    <section id="about">
      <h2>About me</h2>
      <p>I build websites with <strong>HTML5</strong> and <strong>Tailwind CSS</strong> for small businesses.</p>
      <h3>Skills</h3>
      <ul>
        <li>HTML5</li>
        <li>CSS3</li>
        <li>Tailwind CSS</li>
        <li>Git &amp; GitHub</li>
      </ul>
    </section>
```

- Heading order: `h1 → h2 → h3`. **Never skip** (no `h1 → h4`).
- `<strong>` = important text (not just bold). 
- `&amp;` = the `&` character. In HTML, `&` starts a special code, so write it as `&amp;`.

✅ **Check:** Click "About" in the menu → page jumps down.

### Step 6 · Projects with `<article>` and `<figure>` (12 min)

Type **one** project, explain it, then copy-paste for the other two.

```html
    <section id="projects">
      <h2>Projects</h2>

      <article>
        <figure>
          <img src="assets/images/restaurant.svg" alt="Spice Garden website screenshot" width="800" height="500">
          <figcaption>Restaurant landing page</figcaption>
        </figure>
        <h3>Spice Garden</h3>
        <p>A one-page website with menu and reservation form.</p>
        <a href="https://example.com">Live demo</a>
      </article>

    </section>
```

| Tag | Explain |
|-----|---------|
| `<article>` | A piece of content that makes sense **on its own** (a blog post, a product, a project card). |
| `<figure>` + `<figcaption>` | An image together with its caption. |

> Ask students: "Is a project card a `section` or an `article`?" → `article`, because you could share it alone.

### Step 7 · Footer (5 min)

```html
  <footer>
    <address>
      Email: <a href="mailto:hello@example.com">hello@example.com</a>
    </address>
    <p>&copy; 2026 Ekramul Islam</p>
  </footer>
```

- `<address>` = contact information of the page owner.
- `mailto:` opens the visitor's email app. (`tel:` would open the phone dialer.)
- `&copy;` = ©

✅ **Final check:** Page shows everything top-to-bottom, no design. *That is correct* – design comes in Class 1.3.

---

## Part C – Show the difference (5 min)

Open DevTools → **Lighthouse** → Accessibility. Then temporarily change `<nav>` to `<div>` and `alt` to nothing and run it again. The score drops → semantics matter.

## Common mistakes
- Two `<h1>` tags on one page
- Missing `alt` on images
- Using `<br><br><br>` for spacing (spacing is CSS's job)
- Spaces or capital letters in file names (`My Page.html` ❌ → `my-page.html` ✅)

## Homework
1. Replace Ekramul's content with **your own** name, bio and skills.
2. Add one more `<section id="education">` with an `<h2>` and a list.
3. Check your page at https://validator.w3.org/#validate_by_input → 0 errors.
