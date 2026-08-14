# EqDe Capital — website

Front end for EqDe Capital, a GDFS Group company. Static site, no build step:
plain HTML and CSS, hosted on GitHub Pages.

## Structure

```
.
├── index.html      the sign-in gate
├── 404.html        branded not-found page
├── dashboard.html  the desk (served locally by desk_server.py, not by Pages)
├── robots.txt      blocks search engines while access is team-only
├── CNAME           the custom domain (one line, no https://)
└── assets/
    ├── eqde-mark.jpg          the EqDe Capital mark
    ├── og-card.png            link-preview image, 1200×630
    ├── favicon-32.png
    ├── favicon-512.png
    ├── apple-touch-icon.png
    ├── gdfs-logo-white.png    knockout, used on the dark pages
    └── gdfs-logo.png          navy, for light backgrounds
```

## Brand

The mark is gold and silver on black. Everything on the site is derived from it —
do not substitute colours by eye.

| Token | Hex | Use |
|---|---|---|
| Ground | `#050506` | Page background. The mark's own ground is `#000000`; it is blended with `mix-blend-mode: screen` so no rectangle shows. |
| Gold | `#C9A227` | Accent, focus rings, button |
| Gold light | `#E7CC79` | Button highlight |
| Gold dark | `#8F6B1E` | Button edges |
| Paper | `#F3F4F6` | Body text |
| Muted | `#7E838C` | Labels, secondary text |

Type: IBM Plex Sans for the interface, IBM Plex Mono for labels and figures.
No display face — the mark carries the wordmark, so a second one competes with it.

The favicon is the infinity mark alone; the full lockup is unreadable at 32px.

## Deploying

Upload every file above, keeping `assets/` as a folder. Settings → Pages →
Source: *Deploy from a branch* → `main` / `/ (root)`. Pushing any change
redeploys in about a minute.

DNS, at the registrar:

```
A     @    185.199.108.153
A     @    185.199.109.153
A     @    185.199.110.153
A     @    185.199.111.153
CNAME www  <github-username>.github.io
```

Then Settings → Pages → **Enforce HTTPS** once the certificate issues.

## Security — read before sharing the link

**The sign-in form does not authenticate anyone, and it cannot.** A static page has
no secret to check against, and anything checked in JavaScript is readable by the
visitor. The form posts to `/api/session`; until that endpoint exists it reports
plainly that sign-in is not connected rather than pretending to admit anyone.

**Cloudflare Access is the real gate.** It rejects unauthenticated requests at the
edge, so the page is never served to anyone outside the allow-list.

When the Access policy is written, it must cover **the whole origin, every path** —
not just the app. `/api/universe` now returns client names, quantities and values.
It used to be stripped of client identity on the server; that strip was removed
deliberately so the desk can see which accounts hold a name. There is no longer a
server-side guard behind Access.

Until Access is in place, treat the URL as public.

## Still to do

- [ ] Cloudflare Access in front of the domain, covering every path
- [ ] `/api/session` on the backend, or drop the form and let Access do the asking
- [ ] Remove the seeded figures the dashboard ships with, so nothing invented
      renders before the engine answers
