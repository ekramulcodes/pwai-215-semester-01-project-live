# ক্লাস ১.৭ : Git, GitHub ও Netlify/Vercel-এ ডিপ্লয়মেন্ট

| | |
|---|---|
| **You will type** | `.gitignore` (3 lines), `README.md` (~12 lines), `netlify.toml` (3 lines), 2 attributes on the form – plus **terminal commands** |
| **Start from** | `class-06-components-animations/project` |
| **End result** | `class-07-git-deploy/project` + a **live website** |
| **Before class** | Students create a free GitHub account and install Git |
| **Time plan** | 15 min theory · 35 min Git · 15 min GitHub · 30 min deploy · 10 min homework |

---

## Part A – Theory (15 min)

```
Git    = a "save game" system on YOUR computer (history of every change)
GitHub = a website that stores your Git project online (backup + portfolio + teamwork)
Netlify / Vercel = take your GitHub project and make it a live website (free)
```

The 3 areas of Git (draw it):
```
Working folder  --git add-->  Staging area  --git commit-->  History  --git push-->  GitHub
(you edit)                    (ready to save)                (saved)                  (online)
```

## Part B – Git on your computer (35 min)

### Step 1 · One-time setup
```bash
git --version
```
```bash
git config --global user.name "Your Name"
```
```bash
git config --global user.email "you@example.com"
```
> Use the **same email** as your GitHub account – that's how GitHub knows the commits are yours.

### Step 2 · `.gitignore` – what Git must NOT save
```
node_modules/
.DS_Store
.env
```

| Line | Explain |
|------|---------|
| `node_modules/` | Thousands of downloaded files. Anyone can recreate them with `npm install`. **Never commit.** |
| `.DS_Store` | Junk file Mac creates. |
| `.env` | Secret keys/passwords (we'll use these later). |

### Step 3 · First commit
```bash
git init
```
```bash
git status
```
```bash
git add .
```
```bash
git commit -m "feat: first version of my portfolio"
```

| Command | Explain |
|---------|---------|
| `git init` | Start tracking this folder (creates a hidden `.git` folder). Run **once** per project. |
| `git status` | "What changed?" – run it all the time. Red = not staged, green = staged. Show that `node_modules` is **not** listed. |
| `git add .` | Stage **all** changes (`.` = current folder). |
| `git commit -m "..."` | Save a snapshot with a message. |

### Step 4 · Make a change, commit again (live demo of the daily loop)
Change the hero text → save →
```bash
git status
```
```bash
git diff
```
```bash
git add .
```
```bash
git commit -m "fix: update hero text"
```
```bash
git log --oneline
```
- `git diff` = show exactly which lines changed. `git log --oneline` = list of all saves.

**Commit message rule:** `type: what you did` → `feat:` new thing · `fix:` correction · `style:` design · `docs:` README

## Part C – GitHub (15 min)
1. GitHub → **New repository** → name `portfolio` → Public → **don't** tick "Add README" → Create.
2. Copy the commands GitHub shows:
```bash
git branch -M main
```
```bash
git remote add origin https://github.com/YOUR-USERNAME/portfolio.git
```
```bash
git push -u origin main
```

| Command | Explain |
|---------|---------|
| `git branch -M main` | Name the main branch `main`. |
| `git remote add origin URL` | Connect this folder to the GitHub repo. `origin` = nickname for that URL. |
| `git push -u origin main` | Upload. `-u` remembers it – next time just `git push`. |

Refresh GitHub → your code is online. Show the README is displayed on the repo page.

### Branch + Pull Request (if time, 10 min)
```bash
git switch -c feature/new-section
```
```bash
git push -u origin feature/new-section
```
On GitHub → **Compare & pull request** → Merge. Then:
```bash
git switch main
```
```bash
git pull
```
> Say: "Teams never work directly on `main`. Clients love seeing clean PRs."

## Part D – Deploy (30 min)

### Netlify
`netlify.toml` in the project root:
```toml
[build]
  command = "npm run build"
  publish = "public"
```
- `command` = Netlify runs this to create the minified CSS.
- `publish` = only the `public` folder goes online (not `src`, not `node_modules`).

Then: netlify.com → **Add new site → Import from Git → GitHub** → choose the repo → **Deploy**.
→ Site settings → change the name to `yourname.netlify.app`.

### Netlify Forms – receive contact form messages for free
```html
      <form name="contact" action="thank-you.html" method="POST" data-netlify="true" ...>
        <input type="hidden" name="form-name" value="contact">
```
- `data-netlify="true"` → Netlify detects the form while deploying and stores every submission.
- `name="contact"` + the hidden `form-name` → which form the data belongs to.
- Commit + push → submit the live form → Netlify dashboard → **Forms** → the message is there. 🎉

### Vercel (alternative – show quickly)
vercel.com → **Add New Project → Import** the repo → Build command `npm run build`, Output directory `public` → Deploy.

### Automatic deploys
Change something → `git add . && git commit -m "..." && git push` → refresh the live site after ~30 seconds. **This is the professional workflow.**

## Common mistakes
- `node_modules` pushed to GitHub → forgot `.gitignore` *before* the first commit (fix: `git rm -r --cached node_modules`)
- Live site has no styles → wrong `publish` folder or `style.css` path
- `git push` asks for a password → GitHub needs a **personal access token** or GitHub Desktop / VS Code sign-in
- Commit messages like "update", "asdf" ❌

## Homework
1. At least **5 more commits** with good messages.
2. Live URL added to `README.md` and to your GitHub profile.
3. Submit the live link + GitHub link in the class group.
