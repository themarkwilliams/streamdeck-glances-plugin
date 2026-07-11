# Docker Monitor for Stream Deck

Watch your Docker containers on your Elgato Stream Deck, powered by the
[Glances](https://github.com/nicolargo/glances) monitoring server.

> **This is the public home for the plugin: releases history, documentation, and
> [issue tracking](../../issues).** 

## Features

Each container gets a row of live-updating keys — all the same **Container**
action; each key's column setting picks its face:

- **Name** — on a background colored by container status (green running/healthy,
  orange paused/restarting/starting, dark orange running-but-unhealthy). Press to
  open the container's web UI — its published port is detected automatically, or
  use a URL template / per-container override. A small link arrow shows when a
  real destination is known.
    - Glances reports only *running* containers by default. To also list stopped
      containers (shown red), set `all=true` under `[containers]` in glances.conf.
- **CPU %**, **Memory**, **Uptime**, **Status**, **Disk I/O**, **Network**, or
  **Image** — pick per key; metric values are colored by Glances' own thresholds
  (green OK, blue ≥50%, purple ≥70%, red ≥90%).
    - Press a CPU/Memory/Uptime key to sort the list by it; press again to flip
      the direction. 
    - Default sort: highest CPU first.
- **Scroll** — page through all containers manually (▲/▼ keys or a Stream Deck+
  dial, wrapping at the ends) or automatically on a configurable interval.
- **Host Metrics** — one key cycling overall CPU, memory, swap, load average,
  network, disk I/O, disk usage, temperature, and GPU — or pin one metric per key.
- **Switch Host** — monitor any number of Glances servers; 
    - Press the Switch Host button to cycle.
    - Switch Host button shows a color indicator of host status.
    - Auto switch between hosts on a configurable interval (idle hosts are left
      twice as fast).
- **Alerts Only** — optionally hide healthy, quiet containers and show just the
  ones over your CPU/MEM thresholds, or failing their health check.

Works on any Stream Deck — actions are individual keys you arrange to fit your
device, and a ready-made 15-key profile is included.

## Requirements

- Stream Deck software 6.5 or later (Windows 10+ / macOS 12+).
- A [Glances](https://nicolargo.github.io/glances/) server with container support.
  Glances is a general system monitor; container stats are one of its plugins, and
  the `[containers]` pip extra installs the Docker/Podman libraries that plugin
  needs: `pip install "glances[containers]"`, then `glances -w` (default port
  61208) — or run the `nicolargo/glances` Docker image, which includes it.
    - Optional authentication via `glances -w --username`.

## Setup

1. Install the bundled 15-key profile (offered on install, or press the **Open
   Profile** key), or add **Container** keys to rows and pick each key's
   column — each key detects its list row automatically from its position on
   the deck (topmost plugin row = first container).
   - **One container, every metric**: keys on the same physical deck row already
     share a container automatically. For any other layout — say a block of
     Name/CPU/MEM/Uptime keys all dedicated to the list's top container — set
     each key's **List row** to **Manual** with the *same* row number, then give
     each key a different column. All of them track whichever container occupies
     that list position (combine with sorting: row 1 = highest CPU).
1. Open any key's settings → **Glances connection** → add your host(s): label,
   host/IP, port, protocol, and credentials if your server uses them — then press
   **Test** to verify.
1. Optionally set a URL template (e.g. `https://{name}.lan`) or per-container URL
   overrides on a Name key; with nothing configured, pressing a name opens the
   container's first published port.
1. Add **Scroll**, **Host Metrics**, and **Switch Host** keys as you like.

## Getting the plugin

Elgato Marketplace release is planned — watch this repo for announcements.

## Reporting Issues

Found a bug or have a feature request? Please [open an issue](../../issues/new/choose)
and fill out the relevant template.

Before submitting:

- Check the [existing issues](../../issues) to avoid duplicates.
- Include your Glances version and Stream Deck software version.

## Version history

See [CHANGELOG.md](CHANGELOG.md).
