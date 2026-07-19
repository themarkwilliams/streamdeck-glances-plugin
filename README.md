# Docker Monitor for Stream Deck

Watch your Docker container performance on your Elgato Stream Deck, powered by the
[Glances](https://github.com/nicolargo/glances) monitoring server.

> **This is the public home for the plugin: releases history, documentation, and
> [issue tracking](../../issues).** 

## Features

### Host

- **Host Metrics** - one key showing a host metric. Either select a specfic metric from a dropdown or cyle through several. Available metrics: 
    - CPU
    - memory
    - swap
    - load average
    - network
    - disk I/O
    - disk usage
    - temperature
    - GPU
    - host uptime
    - process count
    - top process
    - IP address
    - fan speed
- **Switch Host** - monitor any number of Glances servers; 
    - Any button shows the host configuration options. Enter ip/url, port and protocol. 
    - Press the Switch Host button to cycle between configured hosts.
    - Switch Host button shows a color indicator of host status.
    - Auto switch between hosts on a configurable interval (default: 20 seconds, idle hosts are switch away 50% faster).

### Container 

Each container gets a row of live-updating keys - all the same **Container Metric** action; each key's column setting picks its face:

- **Container Metric** - pick per key; metric values are colored by Glances' own thresholds (green OK, blue ≥50%, purple ≥70%, red ≥90%).
    - **Container Name** - displays on a background indicating container status 
        - Green -  running/healthy
        - Orange - paused/restarting/starting
        - Dark Orange - unhealthy. 
        - Press to open the container's web UI 
            - Published port is detected automatically
            - Link available indicated by an arrow on the button
            - Override to use a custom URL template / per-container override. 
            - Set URL = none to turn off the linking action where port exists, but doesn't render a useful UI.
    - **CPU**
    - **Memory**
    - **Uptime**
    - **Status**
    - **Disk I/O**
    - **Network**
    - **Image**
- **Sort
  List** - Press a metric key to sort the list by it; press again to flip the direction.  (Default sort: highest CPU first.)
- **Scroll List **- page through all containers manually (▲/▼ keys or a Stream Deck+ dial, wrapping at the ends) or automatically on a configurable interval.
    - Containers rotate every 4 seconds by default. If you manually scroll the list, it will resume auto scrolling after 8 seconds.
- **Alerts Only** - optionally hide healthy, quiet containers and show just the
  ones over your CPU/MEM thresholds, or failing their health check.
- **Container Metrics** by default will show the same container per row. If you want to adjust that, you can override the List Row assignment from Auto to a different row selection. 

Works on any Stream Deck - actions are individual keys you arrange to fit your device, and a ready-made 15-key profile is included.

## Requirements

- Stream Deck software 6.9 or later (Windows 10+ / macOS 12+).
- A [Glances](https://nicolargo.github.io/glances/) server with container support.

    - Optional authentication via `glances -w --username`.

## Setup

1. Install the bundled 15-key profile (offered on install, or press the **Install/Open
   Profile** key), or add **Container** keys to rows and pick each key's
   column - each key detects its list row automatically from its position on
   the deck (topmost plugin row = first container).

   - **One container, every metric**: keys on the same physical deck row already
     share a container automatically. For any other layout - say a block of
     Name/CPU/MEM/Uptime keys all dedicated to the list's top container - set
     each key's **List row** to **Manual** with the *same* row number, then give
     each key a different column. All of them track whichever container occupies
     that list position (combine with sorting: row 1 = highest CPU).
1. Open any key's settings → **Glances connection** → add your host(s): label,
   host/IP, port, protocol, and credentials if your server uses them - then press
   **Test** to verify.
1. Optionally set a URL template (e.g. `https://{name}.lan`) or per-container URL
   overrides on a Name key; with nothing configured, pressing a name opens the
   container's first published port.
1. Add **Scroll**, **Host Metrics**, and **Switch Host** keys as you like.

## Getting the plugin

Elgato Marketplace release is planned - watch this repo for announcements.

## Reporting Issues

Found a bug or have a feature request? Please [open an issue](../../issues/new/choose)
and fill out the relevant template.

Before submitting:

- Check the [existing issues](../../issues) to avoid duplicates.
- Include your Glances version and Stream Deck software version.

## Version history

See [CHANGELOG.md](CHANGELOG.md).