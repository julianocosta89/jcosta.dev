# jcosta.dev

This is my webpage, built using [Hugo][hugo] and [Blowfish][blowfish].

Accessible at <https://jcosta.dev>

## Local development

```sh
git submodule update --init   # fetch the Blowfish theme
hugo server -D                # http://localhost:1313, drafts included
```

Use the Hugo **extended** version pinned in `.github/workflows/hugo.yaml`.

New content starts from the archetypes, which create a page bundle:

```sh
hugo new content posts/my-post
hugo new content talks/my-talk
```

Put a `featured.jpg` in the bundle for the card and header image.

## Hosting

- **Production:** GitHub Pages, deployed by `.github/workflows/hugo.yaml` on push to `main`.
  GitHub Pages can't set response headers, so the Content Security Policy is a
  `<meta>` tag in `layouts/partials/extend-head.html`.
- **Previews:** Netlify deploy previews (`netlify.toml`, `static/_headers`).

Renovate keeps Hugo, the Blowfish submodule and the Dash0 Web SDK up to date.

[hugo]: https://gohugo.io/
[blowfish]: https://blowfish.page/
