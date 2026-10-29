# pub

Static HTML hub for [samf852](https://github.com/samf852). The home page is a generated list of every page under `pages/`. Each page keeps its own address.

Predicted site: <https://samf852.github.io/pub/>

Sample page: <https://samf852.github.io/pub/pages/hello/>

## Add a page

Put the file under `pages/`. Two shapes are picked up:

| File | URL on the site |
| --- | --- |
| `pages/hello/index.html` | `/pages/hello/` |
| `pages/notes.html` | `/pages/notes.html` |

The full Pages URL is that path after `https://samf852.github.io/pub`.

Label the page with a comment near the top of the file, or rely on `<title>`:

```html
<!--
title: Field notes
description: Optional sentence shown on the home page.
-->
```

`title` in that comment wins over `<title>`. If both are missing, the folder or file name is used. `description` wins over `<meta name="description">`.

Link the shared stylesheet with a relative path so it works on this project site (`/pub/`):

- folder page (`pages/hello/index.html`): `../../assets/site.css`
- flat page (`pages/notes.html`): `../assets/site.css`

Link back home the same way (`../../` or `../`).

You do not edit `index.html`. After adding or renaming a page, either:

- run `npm run build` and commit the regenerated `index.html`, or
- just push. The GitHub Actions workflow on `main` runs `npm run build` before deploy, so the live home page lists the new file even if the committed index is stale.

`npm run build` only needs Node. It has no dependencies.

## Enable GitHub Pages

1. Open **Settings → Pages → Build and deployment**.
2. Set **Source** to **GitHub Actions**.

The workflow is `.github/workflows/pages.yml`. It runs on every push to `main`, rebuilds `index.html` from `pages/`, and deploys with `actions/upload-pages-artifact` and `actions/deploy-pages`. The workflow token has `pages: write`.

The first successful run on `main` publishes <https://samf852.github.io/pub/>. Until that run finishes, the URL will 404.

`.nojekyll` is included so a path that starts with `_` is still published if this site is ever built with Jekyll. The Actions deploy does not run Jekyll.
