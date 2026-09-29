# NARVI Scope of Work: Gap Analysis

Sep 29, 2026 · Raju Vedprakash

## Summary

The scope fits in the 10-hour budget. The site is healthier than the SOW assumes: the build and news pipeline have never failed, and no internal link is broken. The real problems are elsewhere. The homepage cards look clickable but aren't links, the admin page has no real protection, 14 of 19 pages share one meta description, and the RSS feed is linked but empty.

- **Source:** *narviai.com Technical Audit — Initial Scope of Work*, prepared by Akeim Joseph for Ronny Carter (iskpro.com), dated Sep 23, 2026. $400 fixed fee for 10 hours.
- **How this was checked:** the repo at commit `29573fe` was built locally with the `github-pages` gem. All 19 generated pages were scanned for links, meta tags, the analytics script and the feed link, and loaded at 375 px phone width. GitHub Actions run history was read through the API.
- **What wasn't checked:** the live site at narviai.com and the GoatCounter dashboard. No repo files were changed.

## Requirements vs current state

3 items are broken, 3 work only partly, and 5 are fine. Priority items are listed first, as in the SOW.

| SOW item | What the repo does today | Status | Fix |
| --- | --- | --- | --- |
| I. Broken click-through links, homepage (High) | 0 broken internal links across 19 built pages. The real problem: the 3 homepage focus cards are `<div>`s styled like links (blue border and lift on hover) that go nowhere. Their A.R.C.H.O.N. and PRISM tags look like chips but aren't links either. | Broken | Change the cards to `<a>` pointing at `/research/`, `/projects/archon/` and `/projects/prism/`. Edit `index.md` only. |
| I. Admin portal access (High) | `/admin/` is hidden only by `robots.txt` and a `noindex` tag. Anyone with the URL can read it, and its source sits in the repo. | Broken | Put a real access gate in front of it. The options are in Recommended approach. |
| II. Duplicate meta descriptions | 14 of 19 pages use the site-wide description. Both papers publish "Abstract" as their description, because jekyll-seo-tag falls back to the first line of the page. Only the 3 project pages are unique. | Broken | Add a `description:` to each page's front matter. For papers, map it from their existing `summary`. |
| II. RSS feed integration | The feed `<link>` is in the `<head>` of all 19 pages. But `feed.xml` has 0 entries, because jekyll-feed only reads `_posts`. There's no Gemfile: the plugin is enabled in `_config.yml`, not a Gemfile as the SOW says. | Partly working | Point jekyll-feed at the `research` collection in `_config.yml`. No change to collection structure. |
| II. Build/deploy pipeline | There's no custom build workflow: Pages uses GitHub's built-in branch build. 48 of 48 runs succeeded (Sep 15–29). `fetch-news.js` writes an empty list if HN or arXiv returns an HTTP error, and the push has no retry or concurrency guard. | Partly working | Keep the previous data on a failed fetch. Add `concurrency:` and `git pull --rebase` before the push. Optionally add a PR build check. |
| II. GoatCounter integration | The script is on 19 of 19 pages, including `/admin/`. | OK | None needed. Optionally filter `/admin/` in the dashboard so internal visits don't inflate traffic. |
| II. Broken images | The site has no `<img>` tags (the logo is inline SVG). | OK | None. |
| II. Malformed front matter | The build completes with 0 warnings. | OK | None. |
| II. Orphaned pages | Only `/admin/` has no inbound link, which is intentional. `scripts/fetch-news.js` is published as a public file by accident. | OK | Add `scripts` to `exclude:` in `_config.yml`. |
| II. Mobile responsiveness | No sideways scrolling at 375 px on Home, News, a paper or the CV. The Admin table overflows by 12 px. Side rails are hidden below 1180 px by design. | Partly working | Let the Admin table scroll horizontally. |
| III. Access & security | No secrets are referenced anywhere. The workflow uses the default `GITHUB_TOKEN`, so Maintain-level repo access is enough. | OK | None. |

## Risks and dependencies

The admin fix is the only item that depends on something outside the repo. Everything else is a small file edit.

- **GitHub Pages can't do server-side login.** A real gate needs either a proxy in front of the domain or encryption of the page itself. Which option works depends on where narviai.com's DNS is managed (not visible from the repo).
- **A public repo exposes the admin source.** If the repo is public, `admin/index.md` and its layout can be read on GitHub whatever gate the site has. Today the page only shows counts and links, so the exposure is low. The SOW leaves visibility as a separate decision.
- **Meta descriptions and the scope limit.** Adding `description:` to the two papers touches research-file front matter, not the paper text. It needs an explicit OK, because the SOW puts published research content, including "Throttled Intelligence", out of scope.
- **Feed fix and the scope limit.** Feeding the `research` collection is a `_config.yml` change, not a collection-structure change. It stays within scope.
- **Scheduled runs are unreliable on timing.** The news cron is set for 13:00 UTC, but runs actually started between 13:03 and 19:54 UTC. That's normal GitHub queueing. It isn't a failure, but "daily" can mean a stale feed for most of a day.
- **Verifying the fixes live.** The deliverable is "shipped and verified live". Every push to `main` rebuilds the site in about 40 seconds, so each fix can be checked on narviai.com right after it merges.

## Recommended approach

Ship the two priority fixes first, as the SOW asks. Then work through the audit items and finish with the written findings and a phase-two proposal. The plan below adds up to exactly 10 hours.

| Step | Work | Hours | Output |
| --- | --- | --- | --- |
| 1 | Homepage click-through: turn the 3 focus cards into links, then re-run the link scan | 1.0 | PR, verified live |
| 2 | Admin access gate, as chosen below | 2.5 | PR, plus DNS or proxy config if needed, verified live |
| 3 | Unique meta descriptions for all 19 pages (papers pending the scope OK) | 1.0 | PR |
| 4 | Feed the research collection, and validate `feed.xml` | 0.5 | PR |
| 5 | News pipeline hardening: keep previous data on a failed fetch, concurrency guard, pull before push | 1.5 | PR |
| 6 | Health fixes: exclude `scripts/`, fix the Admin table overflow, GoatCounter check on the live site | 1.0 | PR |
| 7 | Written findings list: broken, fine, recommended next | 1.5 | Document |
| 8 | Phase-two scope and timeline, for the Friday review | 1.0 | Document |

**Options for the admin gate:**

| Option | How it works | Cost | Trade-off |
| --- | --- | --- | --- |
| Cloudflare Access (recommended) | Proxies narviai.com through Cloudflare and requires an email one-time code for `/admin/*` | Free up to 50 users | Needs the DNS moved to Cloudflare. This is real server-side auth. |
| StatiCrypt | Encrypts the built admin page with a password. The browser decrypts it after the password is entered. | Free | No DNS change. But it's one shared password with no per-user access or revocation, and it needs a build step. |
| Remove the page from the public site | Drop `/admin/` and rely on the GoatCounter and GitHub dashboards, which already have logins | Free | Simplest, but loses the word-count and feed-health view. |

All PRs go to a branch and are merged by the owner, which matches the SOW's Maintain-level access.

## Open questions for the client

- [ ] Which click-through links were reported as broken? The scan found none. If a specific link was seen failing on the live site, which page and which link?
- [ ] Where is narviai.com's DNS managed, and can it move to Cloudflare for the admin gate?
- [ ] Which admin gate option is preferred: Cloudflare Access, StatiCrypt, or removing the page?
- [ ] Can `description:` be added to the two papers' front matter, given research content is out of scope?
- [ ] Should admin visits stay in GoatCounter's totals or be filtered out?
- [ ] Is the repo staying public? That decides how much the admin gate actually protects.
