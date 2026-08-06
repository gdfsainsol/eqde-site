# EqDe Capital — website

Front end for EqDe Capital, a GDFS Group company. Static site, no build step:
plain HTML and CSS, hosted free on GitHub Pages.

## Structure

```
.
├── index.html      front page — intro film, then the sign-in gate
├── 404.html        branded not-found page
├── robots.txt      blocks search engines while access is team-only
├── CNAME           the custom domain (one line, no https://)
└── assets/
    ├── intro.mp4              the 30s film (2.2 MB, compressed from 24.7 MB)
    ├── gdfs-logo.png          transparent, for light backgrounds
    ├── gdfs-logo-white.png    knockout, used as the video watermark
    ├── og-card.png            link-preview image, 1200×630
    ├── favicon-32.png
    ├── favicon-512.png
    └── apple-touch-icon.png
```

## Brand colours

Sampled directly from the GDFS mark — do not guess replacements.

| Token | Hex | Use |
|---|---|---|
| Navy | `#263054` | Wordmark, headings, top bar of the EqDe mark |
| Swoosh blue | `#4E6FB2` | Button gradient start |
| Swoosh cyan | `#0B9DD0` | Focus rings, mid gradient |
| Swoosh green | `#16B774` | "De", data segments, session dot |
| Gold | `#F2B705` | Single accent rule under the tagline |

Type: Archivo (wordmark), IBM Plex Sans (interface), IBM Plex Mono (labels,
figures), Newsreader (tagline and display lines).

## Deploying

1. Create a repository on GitHub — public, since Pages is free only on public repos.
2. Upload every file above, keeping `assets/` as a folder.
3. Edit `CNAME` to contain your domain on one line, e.g. `eqdecapital.com`.
4. Settings → Pages → Source: *Deploy from a branch* → `main` / `/ (root)`.
5. At your registrar, point the domain at GitHub:

   ```
   A     @    185.199.108.153
   A     @    185.199.109.153
   A     @    185.199.110.153
   A     @    185.199.111.153
   CNAME www  <your-github-username>.github.io
   ```

6. Back in Settings → Pages, tick **Enforce HTTPS** once the certificate issues.

Pushing any change redeploys in about a minute.

## Security — read before launch

`index.html` contains a sign-in form that **does not authenticate anyone**. A static
page cannot verify a credential; anything checked in JavaScript is readable by the
visitor. The form is a shell waiting for a real gate.

Put **Cloudflare Access** in front of the domain before sharing the link. It rejects
unauthenticated requests at the edge, so the page is never served to anyone outside
the allow-list. Free for up to 50 users, with one-time email codes and an access log.

Until that is in place, treat the URL as public.

## Still to do

- [ ] Cloudflare Access in front of the domain
- [ ] Real domain in `CNAME`, real address in the email placeholder
- [ ] Decide whether "seventeen years" belongs to EqDe Capital or GDFS Group
- [ ] Session flag so returning team members skip the intro
- [ ] The application itself — Universe, Client desk, Diagnostics, Execution
