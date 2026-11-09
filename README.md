# KOGYouth Growth Groups · 青少年成长小组查经

Bible studies for our high-school growth groups — passage, discussion and prayer, term by term.

**Live site:** https://w69gjcn72j-dotcom.github.io/kogyouth-studies/ · **中文：** https://w69gjcn72j-dotcom.github.io/kogyouth-studies/index-cn.html

Part of [Word & Prayer](https://w69gjcn72j-dotcom.github.io/sermon-library/) — St Paul's Anglican
Church Kogarah.

## Layout

Everything sits **flat at the repository root**, the same way `sermon-library` works.
No subfolders. English and Chinese live side by side, Chinese files carrying a `-cn`
suffix, and every page has a language toggle in its top-right corner.

| File | Role |
|---|---|
| `index.html` / `index-cn.html` | The browse pages. Each holds its own `STUDIES` list. |
| `NNN-slug.html` / `NNN-slug-cn.html` | One page per study, in each language. |
| `*.webmanifest` | One per language — that is what gives each its home-screen icon. |
| `ky-icon-*.png` | The icon set (32 / 180 / 192 / 512 / 1024), shared by both languages. |
| `site.json` | Titles, manifests and icon prefix, read by `add-study.py`. |
| `add-study.py` | Turns a `.docx` into pages and updates the browse lists. |

## Adding a study

```bash
python3 add-study.py "path/to/study.docx" \
    --group "Term 1 2026" \
    --ref "Mark 10:35-45" \
    --note "February 2026"
```

Add `--cn-docx "path/to/中文.docx"` to publish the Chinese version at the same time,
with its own `--cn-title`, `--cn-group`, `--cn-idea` and `--cn-blurb` as needed. Leave
the Chinese arguments off and only the English page is written — the Chinese one can be
added later with `--lang cn --n 7` to attach it to an existing entry.

Then check and push:

```bash
python3 add-study.py --check
git add -A && git commit -m "Add: …" && git push
```

`--check` confirms every entry has a page, every page has an entry, and that each
English page's Chinese counterpart actually exists.

## Adding one by hand

1. Copy `001-template-how-to-add-a-study.html` to `NNN-your-title.html` (and `001-template-how-to-add-a-study-cn.html` to
   `NNN-your-title-cn.html` for the Chinese).
2. Replace the `<title>`, the `<h1>`, the `.meta` line, the `.bigidea` block and
   everything inside `<div class="ms">`. Keep the back-link and the language toggle.
3. Add a matching entry to `const STUDIES = [` in `index.html`, and to the one in
   `index-cn.html`, at the top of its group:

   ```js
   {
     "n": 2,
     "title": "The King and his Kingdom",
     "ref": "Mark 1:1–13",
     "group": "Term 1 2026",
     "note": "February 2026",
     "idea": "The one-sentence big idea.",
     "blurb": "Two sentences on what this study covers.",
     "page": "002-the-king-and-his-kingdom.html"
   }
   ```

4. Commit and push. GitHub Pages redeploys in about a minute.

## Publishing

Settings → Pages → Source: *Deploy from a branch* → `main` / `/ (root)`.

## Home-screen icons

Open https://w69gjcn72j-dotcom.github.io/kogyouth-studies/ in Safari → Share → **Add to Home Screen** to save it as
**KOGYouth**. Open `index-cn.html` and do the same to save **青少年查经**.
The two share one icon image but have separate manifests, so both can sit on the home
screen at once — the same arrangement as 每日灵修 and Daily Devotions.

---

*Soli Deo Gloria · 唯独荣耀归于神*
