# bitcoincharlotte.bitcoinwallet.guide redirect

Single-purpose GitHub Pages site that 301-redirects `bitcoincharlotte.bitcoinwallet.guide/*`
→ `bitcoinwallet.guide/*`, preserving the hash (`#w=...&c=...`) used by the picker.

## Why this exists

The printed QR code points to `https://bitcoincharlotte.bitcoinwallet.guide/#w=...`.
A Namecheap URL Redirect was originally used, but Namecheap forwards are HTTP-only —
phones default to HTTPS, get a cert error, and bail.

This repo provides a real GitHub-Pages-hosted page with a Let's Encrypt cert,
which then does a client-side redirect to the canonical site, preserving the hash.

## How it works

1. DNS: `bitcoincharlotte.bitcoinwallet.guide` CNAME → `BitcoinCharlotte.github.io`
2. GitHub Pages serves `index.html` with auto-provisioned TLS
3. `<meta http-equiv="refresh">` handles no-JS clients (loses hash but at least lands them on the site)
4. JavaScript `window.location.replace()` preserves the hash for everyone else

## Files

- `index.html` — the redirect page
- `CNAME` — tells GitHub Pages which custom domain serves this
- `.nojekyll` — skip Jekyll processing for faster builds

## Don't add features to this

If anything here grows beyond redirect logic, move it into the main
`bitcoinwallet.guide` repo and wire up additional subdomain forwards there.
