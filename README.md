# PHP2Shell Vendor Watch

A single-page, live dashboard of vendors and software affected by the **PHP2Shell** remote code
execution vulnerabilities **CVE-2026-109618** and **CVE-2026-109619** (fixed in PHP 8.2.35 / 8.3.36 /
8.4.27 / 8.5.12).

It has four views, all built from the NCSC-NL php2shell list:

- **Actionable** — only entries that are *Vulnerable* or have a *Fix* for either CVE.
- **Full list** — the complete NCSC-NL inventory, every status including investigation leads.
- **Index A–Z** — a directory of every supplier, with product counts, a status mix, and a link to each supplier's page in the source.
- **Changes** — what NCSC-NL has added, removed, or re-classified since a fixed baseline snapshot.

On load the page fetches the list **live** from the NCSC-NL repository and rebuilds every view, so it is
current each time it is opened. If the live fetch is blocked it falls back to an embedded snapshot. A
single-file **offline build** that makes no network requests is also available.

## Data source, attribution & licence

Every view reproduces the software inventory from the
**[NCSC-NL php2shell repository](https://github.com/NCSC-NL/php2shell)**,
© NCSC-NL (Nationaal Cyber Security Centrum, Netherlands), licensed under the **EUPL-1.2** and published
as **TLP:CLEAR**. The full licence text is in [`LICENSE`](LICENSE).

This project is an **independent derivative work**, distributed under the **EUPL-1.2** in compliance with
the source licence. It is **not affiliated with or endorsed by NCSC-NL**.

NCSC-NL notes its own list is incomplete and still expanding, and that entries are investigation leads
until confirmed by the vendor.

## Security

This is a static page with no backend, no cookies, no storage and no user accounts.

- Strict **Content-Security-Policy**: `default-src 'none'`; scripts and styles from `'self'` only;
  network (`connect-src`) limited to `raw.githubusercontent.com`; fonts from Google Fonts; no inline
  scripts; no framing of third-party content.
- All data rendered into the page is **HTML-escaped**; source links are **scheme-checked** (only
  `http(s)` is allowed, blocking `javascript:` / `data:` links), and open with
  `rel="noopener noreferrer"` and a no-referrer policy.
- No `eval`, no remote scripts, no third-party trackers.

## Running it

- **Hosted:** any static host (GitHub Pages, Cloudflare Pages, Netlify). No build step.
- **Local:** serve the folder over `http://` (for example `python -m http.server`) so the live fetch
  works; opening the file directly via `file://` may block the fetch depending on the browser.

_Not an official source — always confirm against the vendor's own advisory._
