# Projects, Labs and Write-ups

I am Stephen Jude (online I go by **psychCryxt**), a Cybersecurity student at Wentworth Institute of Technology in Boston. This repo is my journal: the problems I run into, the labs I work through, and the projects I build, written up as they happen, with screenshots, so the record is real and not reconstructed later.

Everything here follows one rule: I only post what I actually did. If a step failed before it worked, the failure is in the write-up too, because that is usually the part that teaches the most. Personal details (IP addresses, device addresses and similar) are redacted before anything goes up.

## Write-ups

Short stories of real problems and how they got solved.

- **Nov 10, 2026:** [No Keyboard, No Mouse, Bluetooth Off: Pairing a Magic Mouse to My Ubuntu Mac Mini over SSH](writeups/2026-11-10-bluetooth-over-ssh.md). Sold my wired keyboard and mouse, Bluetooth was off on the mini, and the only way in was a VPN I had set up months earlier.
- **Nov 10, 2026:** [The Article Was Already on My Screen: Getting Past a Subscribe Overlay with Burp Suite](writeups/2026-11-10-burp-overlay.md). A subscribe gate blocked an article halfway. The content was already in my browser, so I treated the gate as what it was: a curtain, not a lock.
- **Nov 11, 2026:** [Nextcloud Said My Connection Was Insecure: Giving It Real HTTPS with Tailscale Serve](writeups/2026-11-11-nextcloud-tailscale-https.md). The phone app flagged my Nextcloud because a bare IP address can't hold a trusted certificate. Now it answers on its own Tailscale name, over real HTTPS.

## Labs

Structured learning, written up lab by lab: PortSwigger Web Security Academy, TryHackMe, and course labs. See the [labs folder](labs/).

## Projects

Bigger documented builds, under [projects](projects/).

- **Nov 11, 2026:** [My Homelab: A Three-Machine Security Lab](projects/homelab-architecture.md). The full setup: a Mac mini base server running Nextcloud and, as of tonight, a Wazuh SIEM; a Dell Latitude being built as a Kali attacker machine; my EliteBook as the viewing seat. One machine defends, one attacks, one watches.

## Journey

Milestones and where I am on the path: [journey.md](journey.md).
