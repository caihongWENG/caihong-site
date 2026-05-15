# How to update caihongweng.com — your complete guide

A reference for future-you. Keep this file in the workspace folder.

---

## 1. The big picture: where everything lives

Your website is made of three pieces. Each does one job.

```
┌──────────────────────────────────────────────────────────────┐
│  YOUR MAC                                                    │
│  /Users/c.weng/Documents/Claude/Projects/personal website/  │
│  ↑ this is where you edit files                              │
└────────────────────────┬─────────────────────────────────────┘
                         │  git push
                         ▼
┌──────────────────────────────────────────────────────────────┐
│  GITHUB (cloud)                                              │
│  https://github.com/caihongWENG/caihong-site                 │
│  ↑ this stores the official version of your code             │
└────────────────────────┬─────────────────────────────────────┘
                         │  webhook fires automatically
                         ▼
┌──────────────────────────────────────────────────────────────┐
│  VERCEL (hosting)                                            │
│  https://vercel.com/caihongs-projects/caihong-site           │
│  ↑ this builds and serves your site                          │
└────────────────────────┬─────────────────────────────────────┘
                         │  serves at
                         ▼
┌──────────────────────────────────────────────────────────────┐
│  https://caihongweng.com                                     │
│  ↑ your domain, registered with IONOS, points to Vercel      │
└──────────────────────────────────────────────────────────────┘
```

**Key takeaway**: you only ever edit files in the **personal website** folder. Everything else is automatic.

---

## 2. Account access — what you need to remember

| Service | Account | Used for |
|---------|---------|----------|
| GitHub | `caihongWENG` | Stores your code |
| Vercel | `caihongs-projects` team | Hosts your site |
| IONOS | (your domain account) | Owns the `caihongweng.com` domain |



### GitHub Personal Access Token

When you `git push`, GitHub asks for a password. You can't use your GitHub login password (GitHub disabled that in 2021). You need a **Personal Access Token**.

- Create one at: https://github.com/settings/tokens → "Generate new token (classic)" → check the `repo` scope.
- Copy it the moment GitHub shows it — you only see it once.
- Paste it as the password when git prompts.
- On macOS, your token is saved in **Keychain** automatically, so you only have to paste it once.

If push prompts you again later, your token probably expired. Generate a new one with the same steps.

---

## 3. Folder structure — what each file does

```
personal website/
├── index.html                       Home page (bio, news, contact)
├── README.md
├── HOW-TO-UPDATE.md                 This file
├── .gitignore                       Tells git which files to skip
├── caihongsite/
│   ├── css/
│   │   ├── normalize.css            Browser style reset (don't touch)
│   │   └── style.css                ALL site styling (colors, layout, fonts)
│   ├── document/
│   │   ├── cv.html                  CV page (simple PDF link)
│   │   ├── CV_Caihong_WENG.pdf      Your downloadable CV
│   │   ├── Publications.html        Publications page
│   │   ├── Teaching.html            Teaching page
│   │   ├── Service.html             Scientific Service page
│   │   ├── Contact.html             Contact page
│   │   └── Outreach.html            Redirect stub (old page, kept for old links)
│   └── images/
│       ├── caihong.jpg              Your profile photo (round on home page)
│       ├── outreach1.jpg            SpraakLab booth photo
│       ├── outreach2.jpg            Tongue tattoos photo
│       ├── outreach3.jpg            Hallo! screen photo
│       ├── service1.jpg             26th RJC group photo (yellow door)
│       └── service2.jpg             RJCP 2025 organizing team photo
```

---

## 4. The everyday workflow — how to make any change

This is the 4-step recipe. Every change uses these same steps.

### Step 1 — Edit a file

Open the file you want to change in any text editor:
- **VS Code** (recommended, free): https://code.visualstudio.com
- **TextEdit** (built into Mac, just less convenient)
- Anything else you're comfortable with

Make your changes and **save**.

### Step 2 — Preview locally before pushing

Open Terminal:

```
cd "/Users/c.weng/Documents/Claude/Projects/personal website"
python3 -m http.server 8000
```

Then open http://localhost:8000 in your browser. The site renders exactly as it will live. Press `Ctrl+C` in Terminal to stop the preview when done.

### Step 3 — Commit and push

In Terminal (same folder):

```
git add .
git commit -m "describe what you changed"
git push
```

- `git add .` stages all your changes
- `git commit` packages them with a description
- `git push` sends them to GitHub

### Step 4 — Watch it go live

Wait ~30 seconds. Refresh https://caihongweng.com. Done.

If you want to confirm the deploy happened, check https://vercel.com/dashboard — you'll see a green "Ready" indicator on the latest deployment.

---

## 5. Common tasks — how to do specific things

### Add a new publication

1. Open `caihongsite/document/Publications.html`
2. Find the right section (Journal articles / Conference Proceedings / Conference presentations)
3. Copy an existing entry as a template
4. Change the text, year, and DOI link
5. Save, commit, push.

### Add a news item to the home page

1. Open `index.html`
2. Find the `<div class="news-list">` block
3. Add a new `<div class="news-item">` at the TOP (newest first)
4. Use this template:

   For an upcoming event:
   ```html
   <div class="news-item">
       <span class="news-badge upcoming">Upcoming</span>
       <span class="news-content">Poster presentation at <span class="ital">Conference Name</span>, City (Month Day–Day, Year)</span>
   </div>
   ```

   For a publication:
   ```html
   <div class="news-item">
       <span class="news-badge published">New Publication</span>
       <span class="news-content">Paper in <span class="ital">Journal Name</span>: <a href="https://doi.org/..." class="link">Paper Title</a> (Year)</span>
   </div>
   ```

5. Remove the oldest item to keep the list to 4 items max.
6. After events happen, change "Upcoming" to "Presented" by editing the badge text and class.

### Replace your CV PDF

1. Drop the new `.pdf` into `caihongsite/document/` named exactly `CV_Caihong_WENG.pdf` (overwrite the existing one).
2. Commit, push. The download link automatically picks up the new file.

### Add a new course to Teaching

1. Open `caihongsite/document/Teaching.html`
2. Find the right academic year `<h3>` (or add a new one)
3. Add a new `• <span class="boldt">Course Name</span> (lectures/tutorials), Term, level course at University.`
4. Save, commit, push.

### Update your bio on the home page

1. Open `index.html`
2. Find the `<div class="PHD home-bio">` section
3. Edit the text inside the `<p>` tags
4. Save, commit, push.

### Add a new outreach event or conference you organised

1. Open `caihongsite/document/Service.html`
2. Find the right section (Public Engagement and Outreach / Conference and Workshop Organization)
3. Copy an existing `<h3>` block as a template
4. Update title, date, location, photo, and description text.
5. If you have a new photo:
   - Save it to `caihongsite/images/` as `outreach4.jpg` (or similar new name)
   - Add an `<img src="/caihongsite/images/outreach4.jpg" alt="…">` inside the `<div class="photo-row">` block

### Change a colour (e.g., accent green)

1. Open `caihongsite/css/style.css`
2. Search for `rgb(45, 90, 61)` (your current forest green)
3. Replace all instances with the new color (e.g., a burgundy `rgb(120, 40, 40)`)
4. Save, commit, push.

### Change an email or phone number

The email is in two places:
1. `index.html` — search for `c.weng@rug.nl`
2. `caihongsite/document/Contact.html` — same email
Update both, commit, push.

---

## 6. Common errors and fixes

### `git push` says "Authentication failed"

→ Your Personal Access Token expired or is wrong. Generate a new one at https://github.com/settings/tokens with `repo` scope, paste it as password.

### `git push` says "Everything up-to-date" but you made changes

→ You forgot `git add .` and `git commit` before `git push`. Run all three commands in order.

### Push went through but caihongweng.com still shows old content

→ Wait 30 seconds, then hard-refresh (`Cmd + Shift + R`). If still old after 2 minutes, check https://vercel.com/dashboard for a build error.

### Image doesn't show up

→ Check the filename and path. The site is case-sensitive. `Image.jpg` ≠ `image.jpg`. Also make sure the file is committed (`git add caihongsite/images/`).

### `git push` says "permission denied"

→ Your token doesn't have `repo` scope. Regenerate the token and tick the `repo` checkbox.

### You broke something and want to undo your last changes

```
git restore .
```

This throws away all uncommitted changes. Use carefully — there's no undo.

### You pushed a mistake and want to roll back the live site

```
git log
```
(find the previous good commit hash, e.g. `abc1234`)

```
git revert HEAD
git push
```

This creates a new commit that undoes the last one. Vercel re-deploys.

---

## 7. Important URLs to keep handy

- **Live site:** https://caihongweng.com
- **GitHub repo:** https://github.com/caihongWENG/caihong-site
- **Vercel dashboard:** https://vercel.com/dashboard
- **Vercel project (deployments, logs):** https://vercel.com/caihongs-projects/caihong-site
- **Personal Access Tokens:** https://github.com/settings/tokens
- **DOIs (for publications):** https://doi.org
- **ORCID:** https://orcid.org/0009-0002-8989-7231

---

## 8. Site structure cheat sheet

### Pages (in nav order)

| Tab | File | What's there |
|-----|------|--------------|
| Home | `index.html` | Photo, bio, News section, contact emails |
| Publications | `caihongsite/document/Publications.html` | Journal articles, conference proceedings, presentations |
| Teaching | `caihongsite/document/Teaching.html` | Courses by academic year |
| CV | `caihongsite/document/cv.html` | Brief message + PDF download link |
| Scientific Service | `caihongsite/document/Service.html` | Outreach + conference organisation, with photos |
| Contact | `caihongsite/document/Contact.html` | Email |

### Styling conventions used

- **Bold text**: wrap in `<span class="boldt">word</span>`
- **Italic text**: wrap in `<span class="ital">word</span>`
- **Link in text** (green colour): `<a href="..." class="link">text</a>`
- **Right-aligned date** (in CV/Service): `<span class="date">Month Year</span>`

### CSS classes that control the home page

- `.home-bio` — bio section width (currently 1000px max)
- `.news-section` — News section card, width, background
- `.news-badge` — base styles for the badges (Upcoming, New Publication)
- `.news-badge.upcoming` — gold background, pulses
- `.news-badge.published` — green background, static
- `.academic-links` — ORCID, Google Scholar, ResearchGate icons row
- `.keywords` — hashtag-style keywords (currently unused but CSS retained)

---

## 9. The 60-second update — TL;DR

You opened this file because you want to make a quick change. Here's the minimum:

1. Open the relevant `.html` file (probably `index.html` for news, `Publications.html` for papers, etc.) in VS Code.
2. Edit. Save.
3. Open Terminal:
   ```
   cd "/Users/c.weng/Documents/Claude/Projects/personal website"
   git add .
   git commit -m "what you changed"
   git push
   ```
4. Wait 30 seconds. Refresh caihongweng.com.

---

## 10. If you ever get truly stuck

You can always paste this file (or the relevant section) into a Claude or ChatGPT conversation and ask for help. The repo, the file paths, the workflow — everything's documented here so any AI assistant can pick up where you left off.

The site is intentionally simple HTML/CSS — no build steps, no dependencies, no databases. Anyone (including future-you, with a refresher) can maintain it.

— File last updated: May 2026
