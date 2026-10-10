# egnyter

A single static page that hands off an Egnyte link to the Egnyte Desktop App. Google Sheets
only accepts `http`/`https`/`mailto` links, so an `egnyte://` deep link can't live in a cell —
this page lets the cell stay a normal https link, and offers a click that opens the folder in
the desktop app (or in the browser). Links are not stored, sent, or logged; only the
auto-close preference is stored locally in the browser. The whole thing is one
HTML file with inline CSS/JS, and the link is built client-side from the query string.

**URL format:** `https://known-as-dan.github.io/egnyter/?u=<url-encoded Egnyte URL>`

Open `https://known-as-dan.github.io/egnyter/` without a query string to paste an
Egnyte URL and generate a shareable handoff link. The generator includes copy and
preview buttons and accepts both web and `egnyte://` links. Existing `?u=` links
continue to show the desktop/browser choices. Link generation stays in the browser.

**After choosing a destination:** the browser option opens Egnyte in the current
tab, so it replaces the chooser. The desktop option keeps the native `egnyte://`
handoff and then attempts to close the chooser tab. By default, if the launch
prompt or app takes focus, the close attempt waits until focus returns. If you
have already enabled the browser's "Always allow" option for Egnyte, check the
matching checkbox on the chooser. This preference is remembered in that browser
and makes the close attempt run after 1.5 seconds without waiting for focus to
return. It does not change or detect the browser's actual permission setting;
uncheck it if the launch prompt appears again. Browsers may refuse
to close tabs depending on how they were opened; in that case, the chooser stays
available with a note that it can be closed manually. The page cannot confirm
that the desktop app successfully opened the folder.

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
