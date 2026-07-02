# injamam.com — portfolio + blog + content dashboard

A Jekyll site: the scrollytelling CV homepage, a Markdown blog, and a Decap CMS
dashboard (at /admin) to edit both — all hostable free on GitHub Pages.

## What's where
- `index.html` — the CV homepage. Reads its content from `_data/cv.json`.
- `_data/cv.json` — every CV block + headline/copy. Edited via the dashboard.
- `_posts/` — blog posts (Markdown). New posts show on the homepage + `/blog/`.
- `admin/` — the Decap CMS dashboard (`/admin`).
- `assets/img/avatar.jpg` — your photo. Swap it (same name) to change it.
- `blog.html`, `privacy.md`, `_layouts/` — blog list, privacy page, page shells.
- `CNAME` — your custom domain.

---

## GO LIVE — exact steps

### 1. Create the repo
- New GitHub repo, e.g. `portfolio` (Public).
- Upload every file/folder here, keeping the structure. (Web UI: "Add file → Upload files", drag the whole folder in, Commit.)

### 2. Turn on GitHub Pages
- Repo **Settings → Pages**.
- Source: **Deploy from a branch** → `main` / `(root)` → Save.
- Wait ~1 min; it builds at `https://YOURNAME.github.io/portfolio`.

### 3. Point your domain (injamam.com)
At your registrar's DNS, add four A records for the apex `@`:
`185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
and a CNAME for `www` → `YOURNAME.github.io`.
The included `CNAME` file already sets `injamam.com`. Back in Settings → Pages,
wait for the check, then tick **Enforce HTTPS**.

### 4. Point the CMS at your repo
Edit `admin/config.yml`:
- `repo:` → `YOURNAME/portfolio`
- `branch:` → `main`

### 5. Enable dashboard login (one-time)
GitHub login for the dashboard needs a tiny free OAuth relay (GitHub Pages can't
do it alone). Easiest path:
- Deploy a free **Cloudflare Worker OAuth** for Decap (search "decap cms cloudflare
  worker oauth" — it's a copy-paste worker).
- Register a **GitHub OAuth App** (Settings → Developer settings → OAuth Apps),
  callback URL = your worker's `/callback`.
- Put the worker URL into `admin/config.yml` as `base_url:`.
Then visit `https://injamam.com/admin`, log in with GitHub, and edit away —
every save commits to the repo and the site rebuilds automatically.

> Prefer zero setup? Skip step 5 and just edit `_data/cv.json` and add files to
> `_posts/` directly in GitHub's web editor. The dashboard is optional.

### 6. (Optional) local preview
`bundle install` then `bundle exec jekyll serve` → http://localhost:4000
For the CMS locally: `npx decap-server` and open `/admin` (uses `local_backend`).

---

## Editing content
- **CV blocks & copy:** dashboard → "CV content", or edit `_data/cv.json`.
- **Blog posts:** dashboard → "Blog posts → New", or add `YYYY-MM-DD-title.md` to `_posts/`.
- **Photo:** replace `assets/img/avatar.jpg`.
- **Chart data / role-switch logos:** in `_data/cv.json` under `chart` and `switches`.

## Notes
- Company/tool logos load live from Google's favicon service — they appear once
  the site is on a real domain (some previews block external images).
- Booking button points to your Google Calendar page; change it in `index.html`.
