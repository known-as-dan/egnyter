# egnyter

A single static page that hands off an Egnyte link to the Egnyte Desktop App. Google Sheets
only accepts `http`/`https`/`mailto` links, so an `egnyte://` deep link can't live in a cell —
this page lets the cell stay a normal https link, and offers a click that opens the folder in
the desktop app (or in the browser). Nothing is stored, sent, or logged; the whole thing is one
HTML file with inline CSS/JS, and the link is built client-side from the query string.

**URL format:** `https://known-as-dan.github.io/egnyter/?u=<url-encoded Egnyte URL>`

The `u` parameter must match `^(https?|egnyte)://[a-z0-9-]+\.egnyte\.com/[^\s]*$` — anything
else renders an error and no links at all (the page is public, so this guard is what keeps it
from being an open redirect). Either scheme works: `https://…` and `egnyte://…` produce the
same result, with the rest of the URL preserved byte-for-byte.

**In Google Sheets**, with the Egnyte URL in `Y2`:

```
=HYPERLINK("https://known-as-dan.github.io/egnyter/?u=" & ENCODEURL(Y2), "📁")
```

---

עיצוב ופיתוח: [Shiny Pages](https://shinypages.com) — דן סביצ׳קה

Built by Dan Svichka / [Shiny Pages](https://shinypages.com). The page carries the same
watermark treatment as [meshekalexander.com](https://meshekalexander.com) and Mikumit:
both logo lockups (navy for light, white for dark) are inlined as WebP data URIs so the
page stays a single self-contained file with zero network requests.
