# Ahmed Ashour · Portfolio (v2)

Alternate version: no "Four areas I work in" section (site, video and CV), plus the redesigned sidebar CV.

Personal portfolio site: one static HTML page with no build step and no dependencies.

```
portfolio/
├── index.html                 ← the whole site (HTML + CSS + JS inline)
├── .nojekyll                  ← tells GitHub Pages to serve files as-is
├── README.md
└── assets/
    ├── Ahmed_Ashour_CV.pdf    ← "Download CV" button
    ├── portfolio-intro.mp4    ← 38-second intro video (embedded on the site, also good for LinkedIn)
    └── video-poster.jpg       ← thumbnail shown before the video plays
```

---

## Host it on GitHub Pages (personal account)

Your site will be live at **`https://asho30.github.io`**.

> ⚠️ This machine's `gh` CLI and Git credentials are signed in to your **work** account.
> Follow the steps below so nothing gets pushed under the work account.

### Option A: upload through the browser (easiest, no Git needed)

1. Sign in to **github.com with your personal account** (a private/incognito window helps keep it separate from the work account).
2. Click **+ → New repository**.
   - Repository name: **`asho30.github.io`** (exactly your username plus `.github.io`)
   - Visibility: **Public**
   - Click **Create repository**.
3. On the empty repo page, click **uploading an existing file**.
4. Drag in **everything inside** the `portfolio` folder: `index.html`, `.nojekyll`, `README.md` and the `assets` folder.
   - `.nojekyll` is hidden on Windows. In File Explorer, turn on **View → Show → Hidden items** before you drag.
5. Click **Commit changes**.
6. Go to **Settings → Pages**. Under *Build and deployment*, set **Source: Deploy from a branch**, **Branch: `main` / `(root)`**, then **Save**.
7. Wait 1–2 minutes and open `https://asho30.github.io`.

### Option B: Git from the command line

Add your personal account to `gh` alongside the work one:

```powershell
gh auth login                   # pick GitHub.com → HTTPS → log in with the PERSONAL account
gh auth switch                  # choose the personal account
gh auth status                  # confirm the personal account is the active one
```

Then create the repo and push it from the `portfolio` folder:

```powershell
cd "D:\My AI\My Operations\portfolio"
git init -b main
git config user.name  "Ahmed Ashour"
git config user.email "<your-personal-email>"      # repo-local only, so work repos are untouched
git add .
git commit -m "Initial portfolio"
gh repo create asho30.github.io --public --source . --push
```

Turn on Pages (same as step 6 above), or from the CLI:

```powershell
gh api -X POST repos/asho30/asho30.github.io/pages -f "source[branch]=main" -f "source[path]=/"
```

Switch back to work afterwards with `gh auth switch`.

### Updating the site later

Edit `index.html`, then either re-upload it in the browser (Option A) or run:

```powershell
git add . ; git commit -m "Update portfolio" ; git push
```

GitHub redeploys automatically within about a minute.

### Optional: custom domain

1. Buy a domain (e.g. `ahmedashour.dev`).
2. Repo **Settings → Pages → Custom domain**, enter it and save. GitHub adds a `CNAME` file.
3. At your DNS provider, add:
   - `A` records for `@` → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `CNAME` record for `www` → `asho30.github.io`
4. Tick **Enforce HTTPS** once the certificate is issued.

---

## Things to check before publishing

- **Phone number:** neither the site nor `assets/Ahmed_Ashour_CV.pdf` shows your phone number. The PDF is a phone-free copy of the redesigned `CV_Sirdab_Yahoo_v2`, generated from `MY files/2026 Updated/source-html/CV_Sirdab_Yahoo_v2.html` (elements with class `phone` removed). If you edit the CV, regenerate it the same way.
- **CV variant:** the site follows the **Sirdab** timeline (QA Lead at Sirdab, Aug 2024 → Present). Don't mix it with the Edugate variant.
- **Video:** `assets/portfolio-intro.mp4` is about 10 MB, well under GitHub's 100 MB file limit. Leave it out of the upload if you only want it for LinkedIn.

## Preview locally

Double-click `index.html`, or run:

```powershell
cd "D:\My AI\My Operations\portfolio" ; python -m http.server 8000     # then open http://localhost:8000
```
