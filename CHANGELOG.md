# Changelog

All notable changes to the Glances Docker Monitor Stream Deck plugin.
Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versions follow SemVer.

## [Unreleased]

## [0.1.1] - 2026-07-05

Initial release.

### Added
- Seven Stream Deck actions backed by the Glances REST API (v4 with v3 fallback).
- Container Name key — name on a status-colored background (green running/healthy, orange paused/restarting/starting, red stopped/unhealthy); press opens the container's URL (per-container mapping, `{name}`/`{host}` template, or the Glances web UI as fallback).
- Container CPU / Memory / Uptime keys — values in Glances threshold colors (green / blue ≥50 / purple ≥70 / red ≥90); pressing a metric key sorts the list by it, pressing again flips direction. Default sort: CPU descending.
- Scroll List key — moves the visible container window up/down; shows list position. Optional auto-scroll pages through the list on a configurable interval.
- Host Metrics key — cycles CPU, memory, swap, load average, network and disk I/O for the host, on a configurable interval or per press (or pin one metric per key).
- Switch Host key — shows the active Glances host (green online / red offline) and cycles through any number of configured host profiles.
- Property inspectors (dependency-free): shared connection editor for host profiles (label, host/IP, port, protocol, optional Basic-auth credentials), refresh/auto-scroll/scroll-pause settings; URL template + per-container URL overrides with live container-name suggestions.
- Automatic row detection: container keys bind to list rows by their physical position on the deck (topmost plugin row = first container); the explicit Row setting remains as an override.
- Alerts-only mode: optionally list only containers needing attention (not running, unhealthy, or ≥50% CPU/MEM).
- Stream Deck + dial support for Scroll List: rotate to scroll, press to jump to the top, with list position on the touchscreen.
- Bundled starter profiles for 15-key decks and the XL, offered on install.
- Diagnostics for long-run troubleshooting: startup/version log line, unhandled-error logging, and a 15-minute heartbeat (memory, container count, poll health) in the plugin's rotating log files.

### Fixed
- URL overrides could be silently wiped when editing connection settings (the hosts editor overwrote global settings with a stale copy), which made name keys open the wrong or previous URL. All property-inspector sections now read-modify-write shared settings.
- URLs typed without a scheme (e.g. `192.168.1.10:8080`) now open correctly — `http://` is assumed.

### Changed
- Key presses no longer flash the big green checkmark (sort feedback is the ▲/▼ indicator in the metric label).
- Much larger key text: metric labels (CPU/MEM/UP/LOAD/SWAP/NET/DISK) now match the size of their values, and the scroll-position and host key text was enlarged for readability.
- Pressing a Container Name key with no URL configured now opens the Glances web UI instead of doing nothing.
- Manual scrolling pauses auto-scroll for 8 seconds by default (was 15), configurable via the new Scroll pause setting.
- Poll failures are logged on state change instead of every attempt, so an offline host no longer floods the log.
- Deploy pipeline: `npm run deploy [patch|minor|major]` bumps the version, rolls the changelog, tests, builds, and packs a versioned installer; `npm run publish-release` syncs release notes to the public repo.
