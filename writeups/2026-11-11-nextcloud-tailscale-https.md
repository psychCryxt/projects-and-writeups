# Nextcloud Said My Connection Was Insecure: Giving It Real HTTPS with Tailscale Serve

*November 11, 2026*

My home Nextcloud (running in Docker on my Ubuntu server) worked fine in the browser, but the phone app kept warning me the connection was insecure. This is the fix, problem by problem. My real server name and addresses are redacted; anywhere you see `your-server.your-tailnet.ts.net`, picture my machine's own Tailscale name in its place.

## Problem 1: The phone app said the connection was insecure

I was reaching Nextcloud through the server's raw Tailscale IP address over plain HTTP. A bare IP address can't have a trusted HTTPS certificate, so the Nextcloud app flagged it, even though Tailscale already encrypts the traffic itself. Encryption was there; proof of identity was not.

**Solution:** Use Tailscale's built-in HTTPS. I enabled MagicDNS and HTTPS certificates in the Tailscale admin console, which let my server get a real certificate for its own name, `your-server.your-tailnet.ts.net`.

## Problem 2: Nextcloud wasn't serving anything over HTTPS

Nextcloud was only listening on port 10081 over HTTP, so something had to sit in front of it and handle the certificate.

**Solution:** Tailscale Serve:

```bash
sudo tailscale serve --bg --https=443 http://localhost:10081
```

Tailscale now accepts HTTPS on port 443 (tailnet only), handles the certificate, and passes plain HTTP to the Nextcloud container on port 10081.

The honest wrinkle: my first attempt failed. Run as my normal user, Tailscale answered "serve config denied" and told me to use sudo (or set myself as the operator once with `tailscale set --operator=$USER`). Even the first sudo attempt failed on a mistyped password. Real sessions, again.

![The full session: the denied first attempt, then Serve coming up, then the Nextcloud config (server name and addresses redacted)](images/Watermarked%20Nextcloud%20screenshot.png)

## Problem 3: Nextcloud would reject or misbehave behind the new address

Nextcloud only answers to domains it trusts, and it didn't know it was now behind an HTTPS proxy, so it could refuse the hostname or generate http:// links.

**Solution:** I used `occ` inside the Nextcloud container to set four things: the new hostname as a trusted domain, `overwriteprotocol` to https, `overwrite.cli.url` to the new HTTPS address, and the proxy as a trusted proxy.

```bash
docker exec -u www-data nextcloud php occ config:system:set trusted_domains 2 --value=your-server.your-tailnet.ts.net
docker exec -u www-data nextcloud php occ config:system:set overwriteprotocol --value=https
docker exec -u www-data nextcloud php occ config:system:set overwrite.cli.url --value=https://your-server.your-tailnet.ts.net
docker exec -u www-data nextcloud php occ config:system:set trusted_proxies 0 --value=127.0.0.1
```

## Problem 4: The phone app was still pointing at the old IP address

**Solution:** I added the account again in the app using `https://your-server.your-tailnet.ts.net`. Valid certificate, no more warning.

## Things to remember

- Port 443 here is used by Tailscale Serve on my tailnet only. It is not exposed to my LAN or the internet.
- My original port 10081 still works directly on the LAN.
- I can check the setup with `tailscale serve status` and turn it off with `tailscale serve --https=443 off`.
- From now on, always use the .ts.net name, not the IP.

*Worked through with help from Claude AI.*
