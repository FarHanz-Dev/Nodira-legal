# Nodira — Legal

The privacy policy and account deletion pages for **Nodira**, an offline-first
personal finance tracker for Android. Plain static HTML, served through GitHub
Pages. These URLs are the ones registered with Google Play Console and compiled
into the app itself, so they are load-bearing: if a page 404s, the app's store
listing is out of compliance.

## Live pages

| Page | URL |
|---|---|
| Landing | <https://farhanz-dev.github.io/Nodira-legal/> |
| Privacy Policy | <https://farhanz-dev.github.io/Nodira-legal/privacy-policy.html> |
| Account & Data Deletion | <https://farhanz-dev.github.io/Nodira-legal/account-deletion.html> |

Both content pages are bilingual — Indonesian and English in a single document,
with a language switch in the header.

## Why this is its own repository

GitHub Pages can only publish from a repository root or a `/docs` folder. In the
Nodira app repository, `docs/` holds internal engineering rules — including the
Founding Member slot count, a number the product deliberately never shows
anywhere. Publishing that folder to serve two HTML files would have exposed all
of it.

There is deliberately **no copy of these pages in the app repository**. One
existed once and was removed: two identical HTML files in two places diverge on
the first edit that forgets one of them, and what would diverge here is a
binding statement made to Google Play.

## Editing rules

**The text is a legal commitment, not copy.** It is written from verified app
behaviour, and it must stay consistent with the Data safety declaration in Play
Console. Those two disagreeing is among the most common rejection reasons. If
one changes, change the other.

**Do not bump `Policy version` casually.** The number on the page mirrors
`UserConsent.currentVersion` in the app. Raising it invalidates every stored
consent record, so every signed-in user is asked to consent again on next
launch. Raise it only for a material change — not for a typo, and not for a
clarification that only strengthens the user's position.

**If a URL changes, three places move together:** the file here, the two
constants in `lib/core/config/support_config.dart`, and both fields in Play
Console (Privacy policy, and Data safety → Account deletion). Changing one of
the three silently breaks the other two.

## Page structure

- **One language at a time.** The header switch remembers the choice in
  `localStorage` and defaults to the browser's language.
- **Without JavaScript, both languages render** — stacked, exactly as the pages
  behaved before the switch existed. Nobody can lose access to the text.
- **Printing shows both languages** and drops the navigation chrome. Legal
  documents get printed and archived as PDFs.
- **No external fonts, no CDN, no third-party requests.** A page that promises
  your data goes nowhere has no business calling someone else's server to render
  itself.

## Working on it

There is no build step. Edit the HTML, commit, push — Pages republishes in about
half a minute.

```bash
python -m http.server 8757 --bind 127.0.0.1   # then open http://127.0.0.1:8757/
```

When changing layout, verify that the **text** did not change: strip both the
old and new page to plain text and compare them. Reordering a paragraph is easy
to do by accident and nearly impossible to spot by eye — it has already happened
once, to the deletion-request instructions.

---

© 2026 Nodira · `com.nodira.app`
