# How to update caihongweng.com

A cheat sheet so you don't forget again.

## The setup (what's connected to what)

```
Your local files (this folder)
        │
        │  git push
        ▼
GitHub repo: David7779/caihong-site
        │
        │  auto-deploys on every push
        ▼
Vercel (hosting)
        │
        │  serves at
        ▼
caihongweng.com  (custom domain pointing to Vercel)
```

So the only thing you ever need to touch is the **files in this folder**. Push to GitHub, and Vercel deploys it within ~30 seconds.

## Folder structure

```
personal website/
├── index.html                       ← Home page
├── caihongsite/
│   ├── css/
│   │   ├── normalize.css            ← Reset (don't touch)
│   │   └── style.css                ← All site styling
│   ├── document/
│   │   ├── cv.html                  ← CV page
│   │   ├── Publications.html        ← Publications page
│   │   ├── Contact.html             ← Contact page
│   │   └── Fundings.html            ← (currently empty)
│   └── images/
│       └── caihong.jpg              ← Profile photo
└── README.md
```

## Updating content (most common task)

1. Open the file you want to edit (e.g. `Publications.html`) in any text editor — VS Code, TextEdit, etc.
2. Find the text/section and change it. The site is plain HTML, so you'll see things like `<h2>Journal articles</h2>` and your name in `<span class="boldt">Weng, C</span>`.
3. Save the file.
4. Open Terminal and `cd` into this folder:
   ```
   cd "/Users/c.weng/Documents/Claude/Projects/personal website"
   ```
5. Commit and push:
   ```
   git add .
   git commit -m "Add new publication"
   git push
   ```
6. Wait ~30 seconds and refresh caihongweng.com. Done.

## If git asks for a password

GitHub no longer accepts passwords for `git push`. You need a **Personal Access Token**:
1. Go to github.com → Settings → Developer settings → Personal access tokens → Tokens (classic).
2. Generate a token with the `repo` scope.
3. Use that token *instead of your password* when git prompts you.

(Or set up SSH keys for a friendlier setup — Google "GitHub SSH key Mac" if you want.)

## Common edits

**Add a publication** → edit `caihongsite/document/Publications.html`, copy/paste an existing entry as a template, change the text and link.

**Update CV** → edit `caihongsite/document/cv.html`.

**Change contact info / address** → edit `index.html` (and `Contact.html`).

**Replace profile photo** → drop a new file at `caihongsite/images/caihong.jpg` (same filename = no other changes needed).

**Restyle the site** → edit `caihongsite/css/style.css`.

## Preview locally before pushing

Open `index.html` in your browser (double-click it in Finder). It'll render the site locally — no server needed.

## Where things live

- **Live site:** https://caihongweng.com
- **GitHub repo:** https://github.com/David7779/caihong-site
- **Vercel preview URL:** https://caihongsite-david7779.vercel.app
