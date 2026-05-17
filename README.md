# Lumi Studio — Legal Site

Static HTML pages for Apple App Store Connect's mandatory **Privacy Policy URL** field, plus a public Terms of Service link for users who tap "Terms" in the app's paywall.

Generated automatically by `outputs/build_legal_site.py` from `assets/legal/*.txt`. **Don't hand-edit these HTML files** — they will be overwritten on the next regeneration. Edit the source `.txt` files in `assets/legal/` and re-run the script.

## What's in here

| File | Content |
|---|---|
| `index.html` | Landing page with 4 cards (EN/ES × Terms/Privacy). Linked from `<repo>.github.io/<repo>/` root. |
| `terms.html` | English Terms of Service |
| `terms-es.html` | Spanish Terms of Service |
| `privacy.html` | English Privacy Policy |
| `privacy-es.html` | Spanish Privacy Policy |

All 5 files are self-contained (inline CSS, no external dependencies, no JS). Mobile-friendly. Renders identically offline. Apple-reviewer-friendly.

## One-time GitHub Pages setup (5 minutes)

1. **Create a new public GitHub repo.** Name it `lumistudio-legal` (or any name — that becomes part of the URL).
   - Owner = your GitHub user OR an org you own
   - **Public** (private repos can't serve GitHub Pages on the free plan)

2. **Push these 5 files** to the repo's `main` branch:
   ```bash
   cd /Users/projects/Documents/beauty-persona-dev/legal_site
   git init -b main
   git add .
   git remote add origin https://github.com/<YOUR-GH-USER>/lumistudio-legal.git
   git commit -m "Initial legal site"
   git push -u origin main
   ```

3. **Enable GitHub Pages:**
   - Repo → Settings → Pages (left sidebar)
   - **Source:** Deploy from a branch
   - **Branch:** `main` / `/ (root)` → Save
   - GitHub will build + publish within 1-2 minutes
   - You'll get a URL like `https://<YOUR-GH-USER>.github.io/lumistudio-legal/`

4. **Verify** the URLs are live by opening each in a browser:
   - `https://<YOUR-GH-USER>.github.io/lumistudio-legal/`
   - `https://<YOUR-GH-USER>.github.io/lumistudio-legal/terms.html`
   - `https://<YOUR-GH-USER>.github.io/lumistudio-legal/privacy.html`
   - `https://<YOUR-GH-USER>.github.io/lumistudio-legal/terms-es.html`
   - `https://<YOUR-GH-USER>.github.io/lumistudio-legal/privacy-es.html`

## Paste these into App Store Connect

After the GitHub Pages URL is live, go to **ASC → My Apps → Lumi Studio → App Information**:

| ASC field | Value |
|---|---|
| **Privacy Policy URL** (English locale) | `https://<YOUR-GH-USER>.github.io/lumistudio-legal/privacy.html` |
| **Marketing URL** (optional) | leave blank for V1 OR point to your lumistudio.live homepage |

When you add **Spanish (Mexico) localization** in ASC for the V1.1 LATAM launch, set:

| ASC field (Spanish localization) | Value |
|---|---|
| **Privacy Policy URL** | `https://<YOUR-GH-USER>.github.io/lumistudio-legal/privacy-es.html` |

## Regenerating after a source edit

If you change any `assets/legal/*.txt` file (e.g., update the effective date, fix a typo, add a section), re-generate the HTML:

```bash
cd /Users/projects/Documents/beauty-persona-dev
python3 outputs/build_legal_site.py    # regenerates legal_site/*.html

cd legal_site
git add -A
git commit -m "Update legal docs: <reason>"
git push
```

GitHub Pages re-publishes within 1-2 minutes after push. **No ASC change needed** — same URL serves the new content. Apple does not require re-review for legal-page content changes (since the URL is the contract, not the contents at any given moment).

## Future migration to lumistudio.live

When you're ready to move off GitHub Pages onto your own domain:

1. Set up Cloudflare Pages / Vercel / Netlify pointing at this repo
2. Deploy under `lumistudio.live/legal/` (or wherever you prefer)
3. Update ASC Privacy Policy URLs to the new paths
4. Keep the GitHub Pages repo as fallback for ~30 days, then archive

This is a metadata-only change in ASC, no binary re-review required.
