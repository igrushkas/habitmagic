# Habit Magic - Deployment & Security Notes

## Current Setup
- **Hosting**: GitHub Pages (free)
- **Deploy branch**: `master` (merged from feature branches via PR)
- **Feature branch**: `claude/simplify-app-design-DFvRO`
- **Backup of original master**: `claude/backup-master-DFvRO`
- **Domain**: myhabitmagic.com (custom domain with HTTPS)
- **Repo**: PUBLIC (required for free GitHub Pages)
- **Code loading**: Source files loaded directly (`app.js?v=20260219rX`, `styles.css?v=20260219rX`) — NOT minified

## Important Rules
1. **DO NOT make the repo private** — GitHub Pages on free accounts only works with PUBLIC repos. Making it private will take the site down immediately (404 error).
2. **Push to feature branch**, then merge via PR on GitHub:
   ```
   git push -u origin claude/simplify-app-design-DFvRO
   ```
   Direct push to `master` returns 403 from this environment — user merges PRs on GitHub manually.
3. **Minification is currently NOT used** — `index.html` references source `app.js` and `styles.css` directly with cache-bust query params.

## Minification (Available but Not Active)
- `app.js` → `app.min.js` via `terser`
- `styles.css` → `styles.min.css` via `clean-css-cli`
- Build tool: `./build.sh`
- Currently bypassed: `index.html` loads source files directly for easier debugging during active development

## Options to Make Repo Private (Future)
1. **GitHub Pro** ($4/month) — allows private repo + GitHub Pages
2. **Move to Hostinger** — deploy via FTP/SFTP, then make GitHub repo private for free
   - User already pays for Hostinger hosting
   - Would need FTP credentials + target folder (usually `public_html/`)
   - Can set up GitHub Actions for auto-deploy

## Git Setup
- **Remote**: `origin https://github.com/igrushkas/habitmagic.git`
- **Feature branch**: `claude/simplify-app-design-DFvRO`
- **Deploy branch**: `master`

## Tech Stack
- Frontend: Vanilla JS, CSS (no framework)
- Backend: Firebase Auth (Google OAuth) + Firestore
- Audio: 10 Mixkit MP3 celebration sounds in `/audio/`
- Payments: Lemon Squeezy placeholder URLs in code (migration to Stripe planned — awaiting Stripe Payment Links from owner)
- Webhook: Firebase Cloud Function for payment webhook (currently Lemon Squeezy, will need updating for Stripe)

## Business Status
- **IRS EIN**: Pending — owner cannot reach IRS to create EIN. Required before finalizing Stripe setup.
- **Stripe migration**: Blocked on EIN + owner providing Stripe Payment Links for 4 products (Starter monthly/annual, Pro monthly/annual)
