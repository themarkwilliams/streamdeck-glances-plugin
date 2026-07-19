# Changelog

All notable changes to the Docker Monitor Stream Deck plugin.
Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versions follow SemVer.

## [1.0.0] - 2026-07-19
First consolidated release, summarizing the 0.1.x development line.

### Added
- Container dashboard: a single Container Metrics action per key, with a column picker for Name, CPU, Memory, Uptime, Status, Disk I/O, Network, or Image. Names are colored by container status (green healthy, orange transitioning, dark orange failing health check); metric values follow Glances' own threshold colors.
- Live sorting: press any metric key to sort the list by that column, press again to flip. Status sorts problem containers first; Disk I/O and Network sort by throughput. Default: highest CPU on top.
- Automatic row detection: container keys learn their list row from their physical position on the deck; a Manual row setting lets several keys track one container.
- Press a Name key to open that container's web UI: published ports are detected automatically, with a URL template and per-container overrides for reverse proxy setups, and a "none" override to disable a link. A small arrow shows when a real destination is known.
- Scrolling: manual keys or a Stream Deck+ dial with wrap-around, plus optional auto-scroll with a configurable interval and pause.
- Host metrics: fourteen pages (CPU, memory, swap, load, network, disk I/O, disk usage, temperature, GPU, host uptime, process count, top process, IP address, fan speed), pinned one per key or cycling, picked from a dropdown.
- Multi-host: add any number of Glances servers, verify each with a built-in Test button, switch by key press (with a reachability color) or auto-rotate on an interval that skips idle hosts quickly.
- Alerts Only mode: hide healthy, quiet containers and show just the ones over your configurable CPU/MEM thresholds or failing health checks.
- A bundled 15-key profile plus an Install/Open Profile key to jump to it.
- Optional HTTP Basic authentication; works with Glances 3 and 4.
- Diagnostics: rotating logs with startup version, poll failures on state change, unhandled errors, and a periodic memory/health heartbeat.

### Changed
- Release process: dev (patch) versions are tracked in the private changelog; the public changelog and GitHub Releases carry minor/major versions only.
