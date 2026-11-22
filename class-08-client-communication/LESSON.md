# ক্লাস ১.৮ : ক্লায়েন্ট কমিউনিকেশন ও AI প্রম্পট দিয়ে গিগ/কভার লেটার তৈরি

| | |
|---|---|
| **You will type** | No website code today. 3 Markdown files in `docs/`: `gig.md`, `cover-letter.md`, `client-messages.md` |
| **Start from** | `class-07-git-deploy/project` |
| **End result** | `class-08-client-communication/project/docs/` |
| **Time plan** | 20 min communication rules · 30 min gig with AI · 25 min cover letter · 20 min role-play |

---

## Part A – Communication rules (20 min)

| Do ✅ | Don't ❌ |
|------|---------|
| Reply within a few hours | Leave a client on "seen" |
| Short, clear messages | Long paragraphs, "Dear Sir, I am a hard-working…" |
| Ask questions **before** giving a price | Quote without knowing the scope |
| Confirm the requirements in writing | Start work on assumptions |
| Send progress links (your Netlify preview!) | Disappear until the deadline |
| Stay on the platform before an order | Ask for WhatsApp/email/payment outside Fiverr/Upwork → **account ban** |

**The 4 questions to ask before quoting:** pages/sections · design ready or not · deadline · reference websites.

## Part B – Write a gig with AI (30 min)

Show the prompt live and explain each line:

```
Act as a top-rated Fiverr seller coach.
Write a Fiverr gig for a beginner-to-intermediate front-end developer who builds
responsive websites with HTML5 and Tailwind CSS.
Include:
1. A gig title under 80 characters that starts with "I will"
2. 5 search tags
3. A description under 1200 characters: hook, services list, why choose me, call to action
4. 3 FAQs
Tone: friendly and confident. Do not invent fake experience or reviews.
```

| Prompt part | Why |
|-------------|-----|
| "Act as …" | Gives the AI a role → better quality. |
| Exact limits (80 chars, 1200 chars) | These are Fiverr's real limits. |
| Numbered list of parts | AI answers in the same structure. |
| "Do not invent fake…" | AI loves to write "10 years of experience". Lying gets you bad reviews. |

Then **edit the AI output together** → save as `docs/gig.md`. Rules for editing:
- Add your **real** portfolio link (from Class 1.7!)
- Remove anything that isn't true
- Make the first sentence about the **client's** problem, not about you

## Part C – Cover letter for a real job post (25 min)

Open a real Upwork job post with students. Prompt:

```
Write an Upwork proposal (max 150 words) for this job post: [PASTE JOB POST]
- Start with the client's problem, not "Hi, I am"
- Mention this relevant project from my portfolio: [PROJECT + LINK]
- Give a short 3-step plan
- End with one smart question about their project
```

Why the structure works:
1. Client reads the **first 2 lines** in the list → make them about *their* problem.
2. A link to similar work beats any "I am expert" sentence.
3. A plan shows you understood the job.
4. A question invites a reply → starts the conversation.

Save the template in `docs/cover-letter.md`.

## Part D – Role-play (20 min)
Pairs: one student is the client (uses a scenario card), the other replies using `docs/client-messages.md`.

Scenario cards:
1. "I need a website for my bakery. How much?" (no details)
2. "Can you also add a blog for free?" (scope creep)
3. "Send me your WhatsApp number." (outside-platform request)
4. "The colour is wrong, I wanted dark blue." (revision request)

Then commit:
```bash
git add docs && git commit -m "docs: add gig, cover letter and client message templates" && git push
```

## Homework
1. Finish your gig text (don't publish yet – packages come next class).
2. Write 2 cover letters for 2 real job posts.
