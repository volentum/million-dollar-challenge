# The Million Dollar Challenge — Public Customization Page

A static, two-page site that lets loan officers and realtors personalize the
Million Dollar Challenge deck with their own name, headshot, brokerage, brand
color, and contact info — then download it as PDF or standalone HTML.

## What's in this folder

| File         | What it is                                                         |
|--------------|--------------------------------------------------------------------|
| `index.html` | Public landing page. Live preview on the right, customization form on the left. |
| `deck.html`  | Standalone 14-slide deck. Self-contained — works on its own too.   |
| `vercel.json`| Vercel config: clean URLs, no caching for HTML.                    |
| `.gitignore` | Standard ignores.                                                  |

Both HTML files are fully self-contained — no build step, no dependencies.
Drop them on any static host (Vercel, Netlify, S3, GitHub Pages, etc.).

## Deploy to Vercel via GitHub (recommended)

This setup gives you continuous deploys: every commit to `main` redeploys
automatically. Best when you want to update copy or branding over time.

### 1. Create the GitHub repo

1. Go to **github.com/new**
2. Name it something like `million-dollar-challenge`
3. Choose **Public** or **Private** (Vercel works with both)
4. Click **Create repository** (do NOT initialize with a README — we have one)

### 2. Push these files

On your local machine, in this folder:

```bash
git init
git add .
git commit -m "Initial deploy"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/million-dollar-challenge.git
git push -u origin main
```

(Replace `YOUR-USERNAME` with your GitHub username. Copy the exact URL from the
repo page GitHub showed you in step 1.)

### 3. Connect Vercel

1. Go to **vercel.com** and log in (or sign up — free)
2. On your dashboard click **Add New → Project**
3. Find your `million-dollar-challenge` repo and click **Import**
4. Vercel auto-detects it as a static site. Leave all defaults alone.
5. Click **Deploy**

~30 seconds later you'll get a public URL like
`million-dollar-challenge-abc123.vercel.app`. That's your live page.

### 4. (Optional) Custom domain

In your Vercel project: **Settings → Domains → Add**. Type the domain you want
(e.g. `mdc.yourcompany.com`). Vercel will show you a DNS record to add wherever
your domain is hosted. SSL is automatic.

### 5. Updating the site

Make any change to the files. Then:

```bash
git add .
git commit -m "Update copy"
git push
```

Vercel redeploys automatically in about 30 seconds.

## Alternative: Drag-and-drop deploy (skip GitHub entirely)

If you don't want a Git workflow:

1. Zip this folder
2. Go to **vercel.com → Add New → Project**
3. Drop the zip onto the deploy area
4. Click Deploy

Trade-off: no auto-deploy on edits — you have to drag a new zip every time you
change something.

## File structure when deployed

- `yourdomain.com/`           → the customize page (`index.html`)
- `yourdomain.com/deck`       → the standalone deck (clean URL, thanks to `vercel.json`)
- `yourdomain.com/deck.html`  → also works

## What runs where

Everything is **client-side**. There is no server, no database, no API.

- **Live preview** — the customize page inlines the deck HTML and renders it in an iframe via `srcdoc`
- **Image uploads** — files become base64 data URIs, stored in the user's browser only
- **Persistence** — settings save to `localStorage` per browser. Clearing browser data wipes a user's draft.
- **Downloads** — generated client-side as Blob URLs

This means there is **no agent data on your server** at any point. You're hosting two static HTML files. That's it.

## License / brand

Brand colors and typography follow the Team Banosian brand guide. Replace
the headshot/logo placeholders in `deck.html` with your team's assets if you
want a baked-in default before agents customize.
