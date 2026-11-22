# ক্লাস ১.২ : মোডার্ন ফরম, মিডিয়া এবং HTML5 ভ্যালিডেশন

| | |
|---|---|
| **You will type** | `contact.html` (new, ~95 lines – header/footer are copy-paste), `thank-you.html` (15 lines), video in `index.html` (7 lines) |
| **Start from** | `class-01-html5-semantics/project` |
| **End result** | `class-02-forms-media/project` |
| **Time plan** | 10 min recap · 70 min live coding · 15 min validation · 10 min homework |

---

## Step 1 · Create `contact.html` (5 min)
Copy `index.html` → rename to `contact.html`. Delete everything **inside** `<main>`.
Change the `<title>` and `description`. Change the menu links to `index.html#about` and `index.html#projects`.

> Say: "`#about` alone only works on the same page. From another page we write `index.html#about`."

## Step 2 · The `<form>` tag (5 min)

```html
    <section id="contact">
      <h1>Let's work together</h1>
      <p>Fill in the form and I will reply within 24 hours.</p>

      <form action="thank-you.html" method="POST">

      </form>
    </section>
```

| Attribute | Explain |
|-----------|---------|
| `action` | **Where** the data goes when the user clicks Send. For now, a thank-you page. In Class 1.7 Netlify will receive it. |
| `method="POST"` | Send the data hidden in the request body. `GET` would put it in the URL – bad for personal data. |

## Step 3 · Text fields + validation (15 min)

```html
        <fieldset>
          <legend>About you</legend>

          <label for="name">Full name *</label>
          <input type="text" id="name" name="name" required minlength="3" placeholder="e.g. Karim Uddin">

          <label for="email">Email *</label>
          <input type="email" id="email" name="email" required placeholder="you@company.com">

          <label for="phone">Phone</label>
          <input type="tel" id="phone" name="phone" pattern="01[3-9][0-9]{8}" placeholder="01XXXXXXXXX"
                 title="11-digit Bangladeshi number, e.g. 01712345678">
        </fieldset>
```

| Code | Explain |
|------|---------|
| `<fieldset>` + `<legend>` | Groups related fields with a title. Long forms feel shorter. |
| `<label for="name">` + `id="name"` | Connects the label to the input. Click the label → cursor jumps into the box. **Demo this!** |
| `name="name"` | The key the server receives (`name=Karim`). No `name` = the value is **not sent**. |
| `type="email"` | Browser checks for `@` and a domain. On phones it shows the `@` keyboard. |
| `type="tel"` | Opens the number keypad on phones. |
| `required` | Can't submit if empty. |
| `minlength="3"` | At least 3 characters. |
| `placeholder` | Grey hint text. It is **not** a label replacement. |
| `pattern="01[3-9][0-9]{8}"` | A rule (regex): starts with `01`, then a digit 3–9, then exactly 8 digits = 11 digits total. |
| `title` | Shown in the error bubble when the pattern fails. |

✅ **Check:** Click "Send" with empty fields → the browser stops you. Type `abc` in email → error. Type `0123` in phone → error. **No JavaScript was needed!**

> Add the `<button type="submit">Send request</button>` now (before `</form>`) so you can test.

## Step 4 · Select, radio, date, textarea (15 min)

```html
        <fieldset>
          <legend>Your project</legend>

          <label for="service">Service *</label>
          <select id="service" name="service" required>
            <option value="">-- Choose a service --</option>
            <option value="landing">Landing page</option>
            <option value="business">Business website</option>
            <option value="convert">Design to code</option>
          </select>

          <p>Package *</p>
          <label><input type="radio" name="package" value="basic" required> Basic</label>
          <label><input type="radio" name="package" value="standard"> Standard</label>
          <label><input type="radio" name="package" value="premium"> Premium</label>

          <label for="deadline">Deadline</label>
          <input type="date" id="deadline" name="deadline">

          <label for="message">Project details *</label>
          <textarea id="message" name="message" rows="5" required minlength="20"></textarea>
        </fieldset>
```

| Code | Explain |
|------|---------|
| `<option value="">` | Empty first option + `required` = user **must** pick something real. |
| `type="radio"` with the **same `name`** | Only one can be selected. Different names = not a group (demo the bug!). |
| `<label><input> Basic</label>` | Wrapping the input inside the label also connects them – no `for`/`id` needed. |
| `type="date"` | Free calendar picker. |
| `<textarea rows="5">` | Multi-line text. It has a closing tag, unlike `<input>`. |

## Step 5 · Checkbox + submit (5 min)

```html
        <label><input type="checkbox" name="consent" required> I agree to be contacted *</label>

        <button type="submit">Send request</button>
```

- A `required` checkbox must be ticked.
- `<button type="submit">` sends the form. (`type="reset"` would clear it.)

Then create `thank-you.html` (simple page: `<h1>Thank you!</h1>` + link home) and submit a valid form.

## Step 6 · Media: video with captions (10 min) – in `index.html` → About section

```html
      <h3>Say hello</h3>
      <video controls width="640" height="360" poster="assets/images/video-poster.svg">
        <source src="assets/media/intro.mp4" type="video/mp4">
        <track kind="captions" src="assets/media/intro-captions.vtt" srclang="en" label="English">
        Your browser does not support video.
      </video>
```

| Code | Explain |
|------|---------|
| `controls` | Shows play/pause/volume. Without it there are no buttons. |
| `poster` | Image shown before the video plays. |
| `<source type>` | You can add several formats; the browser plays the first it supports. |
| `<track kind="captions">` | Subtitles from a `.vtt` file – for deaf users and people watching without sound. Open the `.vtt` file and show its simple format. |
| Text inside | Fallback for very old browsers. |

> Students record their own 15-second intro on a phone and save it as `assets/media/intro.mp4`. Also mention `<audio controls>` works the same way.

## Step 7 · Embed a map with `<iframe>` (5 min) – in `contact.html`

```html
    <section id="location">
      <h2>Where I work</h2>
      <iframe title="Map of Dhaka" src="https://www.openstreetmap.org/export/embed.html?bbox=90.35%2C23.70%2C90.45%2C23.82&amp;layer=mapnik"
              width="600" height="300" loading="lazy"></iframe>
    </section>
```

- `<iframe>` = a window showing another website (maps, YouTube).
- `title` is required for accessibility. `loading="lazy"` loads it only when the user scrolls near it → faster page.
- For Google Maps: Share → Embed a map → copy the `src`.

## Step 8 · HTML validation (15 min)
1. Go to https://validator.w3.org/#validate_by_input, paste `contact.html` → fix all errors.
2. Break something on purpose (remove a `</label>`, duplicate an `id`) → show the error messages.

## Common mistakes
- `for` and `id` don't match → clicking the label does nothing
- Radio buttons with different `name` values → all can be selected
- Forgetting `name` → field is not sent
- Using `placeholder` instead of a `<label>`

## Homework
1. Add a "How did you find me?" `<select>` and a "Budget" `<input type="number" min="50">`.
2. Record your intro video and add it.
3. 0 errors in the validator for both pages.
