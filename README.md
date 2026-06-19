# Service-Business Landing Page — Template

A self-contained landing page with a built-in **5-step instant-quote calculator** and booking flow.
Hosted on **GitHub Pages**, embeddable in **GoHighLevel** (or any site) via an auto-resizing iframe.

> The files currently contain sample **"Iara Cleaning"** content as a working example. Customize per client (see below).

## Files
- `index.html` — the landing page app. Self-contained: design, fonts, and the interactive quote calculator are all bundled inside. (It's a Claude design export.)
- `embed.html` — wrapper that reports its height to the parent page so the embed auto-resizes (no scrollbars / cut-off).
- `images/` — hero photo.
- `.nojekyll` — makes GitHub Pages serve the files exactly as-is.

## Create a new client site from this template
1. Click **“Use this template” → Create a new repository**. Name it for the client (e.g. `acme-cleaning`).
2. In the new repo: **Settings → Pages →** Source = *Deploy from a branch*, Branch = `main`, Folder = `/ (root)` → **Save**.
   Site goes live at `https://<your-username>.github.io/<repo-name>/`.
3. Customize the content (below).
4. Embed it in GoHighLevel (snippet below), pointing at your new repo's `embed.html`.

## What to customize per client (inside `index.html`)
The page content lives in a `<script type="__bundler/template">` block (the design, stored as text):
- **Business name** (e.g. "Iara Cleaning") — logo, headings, footer
- **Hero image** — replace `images/hero-home.jpg`
- **Services & prices** — the calculator's `SERVICES` and `FREQ` values
- **Reviews / testimonials**, **service-area chips**, **contact info** (phone, email)

⚠️ **Editing gotcha:** this is a *bundled* app. Any `</script>` inside the template text must be written escaped as `<\/script>`, or the page breaks with `Error unpacking: Unterminated string in JSON`. Easiest path: **ask Claude to make the edits.**

## Embed in GoHighLevel
Add a **Custom JS/HTML** element to a blank, zero-padding page and paste:

```html
<iframe id="site-embed" src="https://<your-username>.github.io/<repo-name>/embed.html"
        title="Business name" scrolling="no"
        style="width:100%;border:0;display:block;height:3500px;"></iframe>
<script>
  window.addEventListener('message', function(e){
    if (e.data && typeof e.data.siteHeight === 'number'){
      var f = document.getElementById('site-embed');
      if (f) f.style.height = e.data.siteHeight + 'px';
    }
  });
</script>
```
