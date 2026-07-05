# Glances Docker Monitor for Stream Deck

Watch your Docker containers on your Elgato Stream Deck, powered by the
[Glances](https://github.com/nicolargo/glances) monitoring server.

> **This is the public home for the plugin: releases history, documentation, and
> [issue tracking](../../issues).** The plugin's source code is not published here.

## Features

Each container gets a row of live-updating keys:

- **Name** — on a background colored by container status (green running/healthy,
  orange paused/restarting/starting, red stopped/unhealthy). Press to open the
  container's web UI.
- **CPU %**, **Memory**, **Uptime** — colored by Glances' own thresholds (green OK,
  blue ≥50%, purple ≥70%, red ≥90%). Press any metric key to sort the list by it;
  press again to flip the direction. Default sort: highest CPU first.
- **Scroll** — page through all containers manually (▲/▼ keys) or automatically on
  a configurable interval.
- **Host Metrics** — one key cycling overall CPU, memory, swap, load average,
  network and disk I/O for the host.
- **Switch Host** — monitor any number of Glances servers; press to cycle, shows
  online/offline at a glance.

Works on any Stream Deck — actions are individual keys you arrange to fit your device.

## Requirements

- Stream Deck software 6.5 or later (Windows 10+ / macOS 12+).
- A [Glances](https://nicolargo.github.io/glances/) server with the containers
  plugin enabled: `pip install glances[containers]`, then `glances -w`
  (default port 61208). Optional authentication via `glances -w --password`.

## Setup

1. Add **Container Name / CPU / Memory / Uptime** keys to a row; give each the same
   **List row** number (Row 1 for the top container, Row 2 below, …).
2. Open any key's settings → **Glances connection** → add your host(s): label,
   host/IP, port, protocol, and credentials if your server uses them.
3. Optionally set a URL template (e.g. `http://{host}:8080`) and per-container URL
   overrides on a Name key, so pressing it opens that container's web UI.
4. Add **Scroll**, **Host Metrics**, and **Switch Host** keys as you like.

## Getting the plugin

Elgato Marketplace release is planned — watch this repo for announcements.

## Support

Found a bug or want a feature? [Open an issue](../../issues/new). Please include
your Stream Deck software version, OS, and Glances version.

## Version history

See [CHANGELOG.md](CHANGELOG.md).

---

© Mark Williams (Marktastic). All rights reserved. Not affiliated with or endorsed
by the Glances project or Elgato.
