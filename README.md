# eisseattle-redirect

Serves **eisseattle.com** — the legacy Express Installation Services domain —
and sends every request to https://www.stridenw.com/.

## Why this is its own repository

GitHub Pages allows **one** custom domain per repository (the `CNAME` file holds
a single value). `stridenw-site` is claimed by `stridenw.com`; pointing a second
apex domain at the same Pages IPs returns GitHub's "There isn't a GitHub Pages
site here" 404. A second domain therefore needs a second repo.

## Why not a 301

Wix served a real 301 here. GitHub Pages cannot issue one for a domain it
serves — it returns 200 and the redirect happens in the browser
(`<meta http-equiv="refresh">` plus `location.replace`). Weaker for SEO, which
is why the page is `noindex, follow` with a `canonical` at the destination:
crawlers pass the link equity on and do not index this shell.

A true 301 needs an edge layer. When eisseattle.com's nameservers can finally be
moved to Cloudflare, replace this with a Cloudflare redirect rule and archive
the repo.

`404.html` is a copy of `index.html`, so *any* path redirects, not just the root.

## Do not touch the DNS beyond A and CNAME

eisseattle.com carries **live Google Workspace MX**. Its A records and `www`
point here; nothing else about the zone may change.
