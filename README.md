# Joey Android Apps — organization website

Static site that serves as the **organization website** required for the Google Play
**Organization** developer account (health apps must publish from an org account). It also gives
the studio a public presence and links to each app's privacy policy / terms.

- `index.html` — the whole site (self-contained, inline CSS).
- `assets/` — app icons (e.g. `puffers.png`).

## Deploy (target: `home.joeyapps.abrdns.com`, on the Deck's shared Caddy)

1. **DNS** — in Google Cloud DNS (the `abrdns.com` zone, same place as the other subdomains), add:

   ```
   Type: A   Host: home.joeyapps   Value: 64.180.241.202
   ```

   (Same WAN IP as `puffers.joeyapps.abrdns.com` / `policies.joeyapps.abrdns.com`.)

2. **Caddy** — append this block to `/etc/caddy/Caddyfile` (static file server, auto-HTTPS):

   ```
   home.joeyapps.abrdns.com {
       root * /home/deck/claude-projects/joeyapps-site
       file_server
   }
   ```

3. **Reload** the shared proxy (provisions the TLS cert automatically):

   ```
   sudo systemctl restart bcparks-caddy
   ```

Then `https://home.joeyapps.abrdns.com` is the URL to enter as the **Organization website** in the
Play Console org account.

## Updating
Edit `index.html` and `git commit`. Caddy serves the files directly — no rebuild, no restart needed
for content changes.
