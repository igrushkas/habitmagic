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

## Branding
- **Tagline/Slogan**: "Turn Chaos Into Magic"
- **No ADHD language** — use "busy brains" / inclusive language everywhere
- **Contact**: support@myhabitmagic.com (Titan Email, 1GB)

## Tech Stack
- Frontend: Vanilla JS, CSS (no framework)
- Backend: Firebase Auth (Google OAuth) + Firestore
- Audio: 10 Mixkit MP3 celebration sounds in `/audio/`
- Payments: Lemon Squeezy placeholder URLs in code (migration to Stripe planned — awaiting Stripe Payment Links from owner)
- Webhook: Firebase Cloud Function for payment webhook (currently Lemon Squeezy, will need updating for Stripe)

## Backups

### Git Tag Backup
- **Tag**: `backup-before-merge-20261117-221405` — snapshot of feature branch before merging to master (Nov 17 2026)
- Restore: `git checkout backup-before-merge-20261117-221405`

### File Backups (in repo)
- **`/backup/`** — Original master files from Nov 7 2026 (app.js.bak, index.html.bak, styles.css.bak, minified versions)
- **`/before/`** — Pre-redesign master files from Nov 7 2026 (app.min.js, firebase-config.js, index.html, manifest.json, styles.min.css)

### Git Branch Backup
- **`claude/backup-master-DFvRO`** — Full copy of original master before any changes

### What Changed Before Backup (Nov 7-17, 2026)
1. **UI redesign**: Single-task focus, maximized focus mode, simplified forms, 20px rounded buttons, typography consolidation
2. **Pricing tiers with caps**: Free (3 goals, 5 badges), Starter (10 goals, 12 badges, Focus Timer, Panic Button), Pro (unlimited, Pick For Me, priority support)
3. **Branding**: Removed all ADHD references, replaced with "busy brains" / inclusive language
4. **Legal pages**: /terms.html (30-day refund, founding member program), /privacy.html (GA4 disclosure)
5. **Google Analytics**: GA4 (G-QYPMGS8DKZ) installed on all pages
6. **SEO**: sitemap.xml, robots.txt, Open Graph meta tags
7. **Content pages**: /resources.html (8 strategies), /quiz.html (focus quiz), /blog.html (3 articles)
8. **Landing page fixes**: meta description, badge count (18), Pick For Me copy, help section rewrite
9. **Service worker**: Caches all new pages, fixed source file references
10. **Demo mode**: All 4 mode tabs unlocked, badge seeds, stats, wheel data populated

## Business Status
- **IRS EIN**: Pending — owner calling IRS Nov 18 2026. Required before finalizing Stripe setup.
- **Stripe migration**: Blocked on EIN + owner providing Stripe Payment Links for 4 products (Starter monthly/annual, Pro monthly/annual)

## What Is NOT Working Yet
1. **Stripe checkout**: URLs are still Lemon Squeezy placeholders. Buttons go to dead links. Blocked on owner providing Stripe Payment Links.
2. **Tier cap enforcement**: app.js does not enforce goal limits (3 Free / 10 Starter), badge locks, or streak caps yet. Everyone gets full access.
3. **Paywall gate**: `isProUser()` returns `true` for everyone. No real tier checking.
4. **Stripe webhooks**: Firebase Cloud Function still configured for Lemon Squeezy, not Stripe.
5. **Referral rewards**: Tracking code stores referrals in Firestore. No reward promised — will decide later.
6. **Blog publishing**: Static HTML — new posts require manual editing of blog.html.
7. **Google Search Console**: Sitemap submitted but property not yet verified by owner.
8. **Contact email**: DONE — support@myhabitmagic.com (Titan Email, 1GB inbox)

## Feedback System
- **Sends to**: Firebase Firestore, collection `bugs_and_feedback` + email notification via EmailJS
- **Email destination**: support@myhabitmagic.com (Titan Email)
- **Email relay**: EmailJS (free tier — 200 emails/month, 2 templates)
- **Data collected**: Checked issues (per section), section comments, user email, page URL, user agent, timestamp
- **Access**: View in Firebase Console > Firestore > bugs_and_feedback collection, or check support@myhabitmagic.com inbox

### EmailJS Setup (DONE)
- **Account**: emailjs.com (free tier, 200 emails/month, resets monthly)
- **Service**: SMTP via Titan Email (smtp.titan.email:465 SSL) — Service ID: `service_ia7v9fh`
- **Template**: "Contact Us" — Template ID: `template_locpj2l`
- **Template variables**: `{{name}}`, `{{email}}`, `{{title}}`, `{{time}}`, `{{message}}`
- **Public Key**: `4sPwRxcT_5aTtvwyf` (in index.html)
- **Code**: Keys wired in index.html + app.js (no placeholders remaining)
