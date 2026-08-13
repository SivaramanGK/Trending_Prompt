# Muse & Frame — site files

## Folder structure
```
index.html          the whole site (one page)
data/prompts.xlsx    the sheet that controls the "Trending" section
images/               your photos go here
```

## How the "Trending" section works
`index.html` fetches `data/prompts.xlsx` **directly in the browser** (no build
step, no server) using a small library called SheetJS. Whatever rows have
`Yes` in the **Trending (Yes/No)** column show up as cards on the site, in
the order set by the **Order** column.

To update the site: edit `data/prompts.xlsx`, save, and push the change to
GitHub. Refresh the live page — no rebuild needed.

Columns in `data/prompts.xlsx` (sheet tab **"Trending Prompts"**):

| Column | What it does |
|---|---|
| Order | 1 = shows first |
| Trending (Yes/No) | `Yes` shows the card, `No` hides it |
| Title | card heading |
| Category | small label |
| Tag | second small label |
| Prompt Text | the full prompt shown + copied |
| Image Filename | must match a file in `/images` exactly, e.g. `bardot-01.jpg`. Leave blank for a plain color card. |

Don't rename the sheet tab or the column headers — the site looks for those
exact names.

## Adding photos
Drop image files into `/images`, then type the exact filename into the
`Image Filename` column for that row. JPG or WEBP, portrait orientation,
under ~500KB each is a good target so the page stays fast.

## Hosting on GitHub Pages
1. Create a new GitHub repository (public).
2. Upload these three items to the **root** of the repo, keeping the folder
   names exactly: `index.html`, `data/` (with `prompts.xlsx` inside), and
   `images/`.
3. In the repo, go to **Settings → Pages**.
4. Under "Build and deployment", set **Source: Deploy from a branch**,
   branch **main**, folder **/(root)**. Save.
5. GitHub gives you a URL like `https://yourusername.github.io/repo-name/`
   within a minute or two — that's your live site.
6. Every time you edit `prompts.xlsx` or add an image and push the change,
   the live site updates automatically on next page load.

No build tools, npm, or hosting account beyond GitHub itself are needed —
it's a fully static site.

## SEO setup (do this once your GitHub Pages URL is live)

The page ships with an optimized title, meta description, Open Graph/Twitter
tags, and structured data — but four placeholders need your real URL before
they'll work:

1. Open `index.html` and find every line marked `EDIT ME`. Replace
   `https://yourusername.github.io/muse-and-frame/` with your actual GitHub
   Pages URL (from Settings → Pages once it's live).
2. Do the same in `robots.txt` and `sitemap.xml`.
3. Add a 1200×630px image named `og-cover.jpg` to `/images` — this is the
   preview picture shown when the link is shared on WhatsApp, Facebook, or X.
4. Optional: add a small square `favicon.png` to `/images` (32×32 or 64×64) —
   it's the icon shown in the browser tab and search results.
5. Submit your sitemap in **Google Search Console** (search "Google Search
   Console", add your site as a property, verify ownership, then paste
   `https://yourusername.github.io/muse-and-frame/sitemap.xml` under Sitemaps).
   This is what actually gets Google to notice and start indexing the page —
   nothing in the HTML alone makes that happen.

### On ranking "at the top"
Meta tags and structured data make the page *eligible* to rank well and to
show a clean title/description/image in search results and social shares.
They do not control your rank against other sites — that depends on things
outside any single page: how many other sites link to yours, how often the
content is updated, page speed, and how directly it matches what people
search for. Realistic path: keep the Trending sheet genuinely updated,
use specific long-tail titles in each prompt (e.g. "Bardot studio portrait
prompt" rather than just "prompt 1"), and give it a few weeks to months —
that's normal even for well-optimized pages.
