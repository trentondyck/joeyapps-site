# Joey Android Apps — studio website

The public website for **Joey Android Apps**, an independent Android studio. It doubles as the
**organization website** for the Google Play Organization developer account, gives the studio a
public presence, pitches our Claude Code build pipeline, and links every app to its hosted
privacy policy and terms.

- `index.html` — the whole site (self-contained, inline CSS + a few lines of JS).
- `assets/favicon.svg` — site icon.
- `assets/apps/<app>/` — per-app store assets pulled from each project: `icon.png`,
  `feature.png`, and `shot1..N.jpg` (screenshots, resized for the web).
- `CNAME` — custom domain for GitHub Pages: `home.joeyapps.abrdns.com`.

## Hosting — GitHub Pages

This site is served by **GitHub Pages** from the [`trentondyck/joeyapps-site`](https://github.com/trentondyck/joeyapps-site)
repo (the `main` branch). It is **not** served by the Deck's Caddy.

- **Live URL:** https://home.joeyapps.abrdns.com (the `CNAME` file sets the custom domain).
- **DNS:** the `home.joeyapps` record in the `abrdns.com` zone points at GitHub Pages.
- **Deploy:** push to `main` — GitHub Pages rebuilds automatically. No server, no Caddy reload.

## Updating

1. Edit `index.html` (or refresh assets — see below).
2. `git commit` and `git push`. GitHub Pages publishes within a minute or two.

## Refreshing app assets

App store assets live in each app's own repo (`../cloud-city`, `../lexical-lattice`,
`../voids-horizon`, `../puffers`). To re-pull and optimize them into `assets/apps/`, run a script
like the one used to generate them: copy each app's `store_icon.png` → `icon.png` (256px),
`feature_graphic.png` → `feature.png` (1024×500), and a couple of `screenshots/*` → `shotN.jpg`
(resized to ~880px tall) with Pillow.

## App policies

Every app links to its hosted privacy policy and terms at
`https://policies.joeyapps.abrdns.com/<app>/{privacy-policy,terms-of-service}.html`
(served separately from the `../policies` project).
