# camari8.site

Static site for **CAMARI8 Cube** — the app's landing page and its user guide, served by
Cloudflare Pages at <https://camari8.com/>.

## What is here

| Path | What it is |
| --- | --- |
| `index.html` | Landing page. Also hands `?puzzle=…` links to the installed app. |
| `guide/index.html` | The full user guide, as an ordinary HTML page. |
| `_redirects` | Cloudflare Pages rules: alternate guide URLs redirect to `/guide/`. |

## The guide page is generated — do not edit it by hand

`guide/index.html` is produced from `docs/USER_GUIDE.md` in the app repository by
`tools/build_guide_page.js` there. The Markdown is the only copy that is maintained; this HTML
is its rendering. Editing the HTML directly would be undone the next time the guide is rebuilt.

To refresh it after a change to the guide:

```powershell
# in the app repository
npm run guide
node tools/build_guide_page.js "D:/projects/camari8.site/guide/index.html"
```

Then commit and push this repository. The script prints its own self-check: heading, table and
list counts, and whether every internal link in the guide still resolves to a heading.

## Publishing

Cloudflare Pages project `camari8-site`, built from this repository's `main` branch with no
build command and no output directory override (the site is plain static files). The custom
domains `camari8.com` and `www.camari8.com` point at the project; the `*.pages.dev` hostname
stays available for previews and works everywhere `camari8.com` does.
