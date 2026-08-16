# susanna-bekker.github.io

Source for **https://susannabekker.com** — the apex personal site.

The landing page is an implementation of the **Susanna Bekker Design System**
(Claude Design project `710d14dc`), specifically its `templates/landing`
template: a flat matte plum field, the wordmark in gold, and three panels
linking out to the rest of the work.

Plain static HTML and CSS. No build step, no JavaScript, and no external
requests — the fonts and the grain texture are served from this repo.

## Layout

```
index.html            landing page
404.html              same field, one panel back to the home page
CNAME                 custom domain, written by Settings → Pages
assets/css/tokens.css design-system tokens, vendored — see the header comment
assets/css/site.css   the landing page itself
assets/fonts/         Rammetto One and Jost, woff2, SIL Open Font License 1.1
assets/img/           texture-grain.png, from the design system
```

`tokens.css` is a copy of the design system's token files, so it is not
hand-edited: when the system changes, re-copy the blocks. Everything specific
to this page lives in `site.css` and refers to those tokens rather than to
literal colours or sizes.

## The three panels

| Panel | Links to |
|---|---|
| LION-8 | `lion-8.susannabekker.com` (self-hosted on a VPS) |
| Late Phase Effect | the ORCID record — **placeholder** |
| Which cosmic object are you? | `/which-cosmic-object-are-you/` ([its own repo](https://github.com/susanna-bekker/which-cosmic-object-are-you)) |

The late-phase panel has no site of its own yet, so it points at the papers on
ORCID. Repoint it once that site exists.

## Adding a page

Any project repo in this account with Pages enabled is published at
`susannabekker.com/<repo-name>`; a folder here is published at the same shape of
URL. Keep the two namespaces disjoint — a folder and a project repo of the same
name would both claim the same path.

```bash
mkdir about
$EDITOR about/index.html      # -> susannabekker.com/about
```

Link `/assets/css/tokens.css` and follow the design system for anything new.

## Deployment

- **Source**: `main` branch, root folder, deployed by GitHub Pages. Pushing to
  `main` publishes; what is committed is what is served.
- **DNS**: Cloudflare, two grey-cloud (DNS-only) CNAMEs — `@` and `www` — both
  to `susanna-bekker.github.io`. Grey cloud is required: a proxied record breaks
  the HTTP challenge GitHub uses to issue its certificate.
- **`CNAME`**: leave it in place. If this repo ever switches to a GitHub Actions
  build, make sure `CNAME` lands in the build output too.
