# Nodira — Legal

The legal pages for **Nodira**, a personal finance app for Android that keeps
your records on your own device.

Three static HTML files, published with GitHub Pages:

- **[Home](https://farhanz-dev.github.io/Nodira-legal/)** — a short index of the two pages below.
- **[Privacy Policy](https://farhanz-dev.github.io/Nodira-legal/privacy-policy.html)** — what the app collects, what it never touches, and where any of it goes.
- **[Account & Data Deletion](https://farhanz-dev.github.io/Nodira-legal/account-deletion.html)** — how to delete your data yourself, and how to ask us to delete your account.

Both pages are written in Indonesian and English. You choose a language in the
header and the page remembers it; if you print the page, you get both.

## Why these live here and not in the app repository

GitHub Pages only publishes from a repository root or a `/docs` folder. Nodira's
`docs/` folder is full of internal engineering notes that were never meant to be
read by anyone but the people building the app, so publishing it to serve two
HTML files was never an option. A repository of its own was simpler.

It also means there is exactly one copy of each page. Keeping a second copy in
the app repository sounds harmless until the two quietly drift apart, and these
particular pages are the ones registered with Google Play.

## Working on them

No build step, no dependencies. Edit an HTML file, push, and the site updates in
about half a minute.

To look at your changes first:

```bash
python -m http.server 8757 --bind 127.0.0.1
```

Then open <http://127.0.0.1:8757/>.

Nothing is loaded from another server — no fonts, no scripts, no analytics. A
page that promises your data stays on your device has no business fetching
anything from somebody else's.

---

© 2026 Nodira · `com.nodira.app`
