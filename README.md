# injamam.com — portfolio + blog + editable dashboard

A Jekyll site: the scrollytelling homepage, a Markdown blog, a Decap CMS
dashboard (at /admin), plus editable tools (site name, favicon, footer,
analytics, injected scripts) and built-in SEO + sitemap.

---


## A. Updating the site on GitHub (after edits)

You do **NOT** need to delete the old files. Two ways:

**Easiest (overwrite via web):**
1. Repo → **Add file → Upload files**.
2. Unzip this package and drag in the files/folders that changed (or all of
   them). Uploading a file with the same path **overwrites** it.
3. **Commit changes.** GitHub rebuilds automatically (~1 min).

> Only "delete then re-upload" if you renamed/removed files and want a clean
> slate. For normal edits, overwrite-upload is enough. `index.html`,
> `_data/cv.json`, `_config.yml`, `admin/`, `_layouts/`, `assets/` must stay at
> the repo root.

**Best for frequent edits:** use the dashboard (Section C) — it commits for you.

---

## B. First-time go-live (recap)
1. Repo → **Settings → Pages** → Source **Deploy from a branch** → `main` / root.
2. DNS: four A records `@` → 185.199.108–111.153, and `www` CNAME →
   `hi-injamam.github.io`. `CNAME` file already sets `injamam.com`.
3. Wait for the check, then tick **Enforce HTTPS**.

---

## C. Activate the CMS dashboard (/admin)

The dashboard edits content through GitHub. GitHub login needs a small, free
OAuth relay (GitHub Pages can't do the login handshake alone).

1. In `admin/config.yml`, set `repo: hi-injamam/portfolio` and `branch: main`.
2. Deploy a free **Decap CMS OAuth relay** (a copy-paste Cloudflare Worker —
   search "decap cms cloudflare worker oauth"). It gives you a URL.
3. Create a **GitHub OAuth App** (GitHub → Settings → Developer settings →
   OAuth Apps): Homepage `https://injamam.com`, callback = your worker's
   `/callback` URL. Copy the Client ID/Secret into the worker.
4. Put the worker URL into `admin/config.yml` as `base_url:`.
5. Visit `https://injamam.com/admin`, log in with GitHub. Every save commits to
   the repo and the site rebuilds itself.

> No dashboard? You can always edit `_data/cv.json` and add posts in `_posts/`
> directly in GitHub's web editor. The CMS is a convenience, not a requirement.

---

## D. The editable tools

All live under **CV content → CV — all blocks & copy** in the dashboard, or in
`_data/cv.json`:

- **Site name / title** — `settings.title` (browser tab + SEO title).
- **Meta description** — `settings.description` (search + link previews).
- **Favicon** — `settings.faviconText` (1–2 letters in the gradient square).
- **Analytics (GA4)** — put your `G-XXXXXXXXXX` in `settings.ga4`. Blank = off.
- **Injected scripts** — `settings.headScripts` / `settings.bodyEndScripts`
  accept any raw tags (Search Console meta, pixels, etc.).
- **Footer** — `footer.text`, `footer.links` (label/URL/external), `footer.copyright`.
- **Blog posts** — dashboard "Blog posts → New", or add `YYYY-MM-DD-title.md`
  to `_posts/`.
- **Photo** — replace `assets/img/avatar.jpg`.
- **Preloader** — the signature intro; short + auto-dismiss (edit in `index.html`).

---

## E. Google Search Console + SEO

SEO tags (title, description, Open Graph, Twitter card, canonical, JSON-LD) and
`sitemap.xml` + `robots.txt` are generated automatically (jekyll-seo-tag +
jekyll-sitemap).

**Search Console setup:**
1. Add the property `injamam.com` in Search Console.
2. **Verify** — either:
   - **DNS:** add the TXT record they give you in ExonHost Manage DNS, or
   - **HTML tag:** paste their `<meta name="google-site-verification" …>` into
     `settings.headScripts` in the dashboard.
3. **Submit sitemap:** `https://injamam.com/sitemap.xml`.

That's it — the OG/Twitter cards mean shared links unfurl with your name, tagline,
and photo.

---

## Structure
- `index.html` — homepage (content from `_data/cv.json`).
- `_data/cv.json` — all CV blocks, copy, settings, footer.
- `_posts/` — blog posts. `blog.html` — blog index. `privacy.md` — privacy page.
- `admin/` — Decap CMS. `_layouts/` — blog/page shells (with SEO + favicon + GA4).
- `assets/` — CSS + image uploads. `CNAME` — custom domain.

Note: brand/tool logos load live from Google's favicon service — they appear on
the real domain; local previews may show some as text/monograms.
