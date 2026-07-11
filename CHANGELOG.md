# Changelog

All notable changes to the Glances Docker Monitor Stream Deck plugin.
Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versions follow SemVer.

## [Unreleased]

## [0.1.15] - 2026-07-11
### Changed
- Actions list condensed: Container Name plus one Container Metric action (CPU by default; pick Memory, Uptime, Status, Disk I/O, Network or Image per key). Existing Container Memory and Container Uptime keys keep working; those action types are just hidden from the list.
- Docs corrected: stopped containers only appear when the Glances server sets `all=true` under `[containers]` (Glances reports running containers by default); unhealthy shows dark orange, not red; container support install wording clarified; URL auto-detection (published ports) reflected in setup steps.

### Added
- Marketplace listing assets: generator script (`scripts/generate-marketing.mjs`) producing the 1920x960 thumbnail, dashboard, and features gallery images plus the 288x288 app icon into `marketing/`; final form-field copy (name, 1287-character description, support link) added to the listing document.
- Editable marketing deck: `npm run marketing` builds the PNGs plus `marketing/docker-monitor-marketing.pptx` (three 1920x960 slides; tiles embedded as images, all copy as native PowerPoint text boxes) so listing text can be tweaked and re-exported to PNG without code.

## [0.1.14] - 2026-07-10
### Changed
- Auto Switch Host now leaves a host with nothing to show sooner: when the cycled-to host has no containers listed, it dwells for half the configured interval instead of the full time before moving on.

## [0.1.13] - 2026-07-09
### Changed
- Scroll keys (and the dial) now wrap around: pressing up at the top jumps to the bottom of the container list and pressing down at the bottom jumps to the top, matching auto-scroll's wrap behavior.

## [0.1.12] - 2026-07-09
### Added
- Container Name keys show a small link indicator (top-right) when a specific destination is known for that container — a URL override, the URL template, or an auto-detected published port — so you can tell at a glance which containers open their real service versus only the Glances web UI fallback. Monochrome for now.

## [0.1.11] - 2026-07-09
### Fixed
- Bundled profile now installs and switches correctly. It is generated in Stream Deck 6's real export format; the previous file used an outdated format that Stream Deck could not install, so the Open Profile key prompted to install a profile and then did nothing.

### Changed
- The bundled XL profile is temporarily removed pending validation on real XL hardware; the 15-key profile (Stream Deck / MK.2) is included.

## [0.1.10] - 2026-07-09
### Changed
- Open Profile action now uses the plugin's logo as its icon.

## [0.1.9] - 2026-07-09
### Added
- "Reset times" button in the connection editor's Timing section, restoring refresh, host-switch, scroll, and resume intervals to their defaults.

### Changed
- New default intervals: Auto Switch Hosts 20s (was 15), Auto Scroll Containers 4s (was 10); resume-after stays 8s. Defaults in the plugin and property inspector are kept in sync.

## [0.1.8] - 2026-07-09
### Changed
- Renamed the auto-scroll pause field from "Pause after manual" to "Resume auto-scroll after" for clarity.

## [0.1.7] - 2026-07-09
### Changed
- Connection editor: the active host now shows a disabled "Active" button; the others show "Show this host". There is no separate deactivate because exactly one host is active at a time (this is which host the keys display, not a save action).
- Timing controls: Auto Switch Hosts and Auto Scroll Containers each show their interval inline ("every N s") on the same line as the toggle, so the seconds field is always visible instead of appearing only when enabled. Auto Switch Hosts is now listed before Auto Scroll Containers, and "Auto scroll list" is renamed to "Auto Scroll Containers".

## [0.1.6] - 2026-07-09
### Added
- Auto switch host: optionally cycle to the next host on a configurable interval (default 15s). The connection editor's Timing section is reorganized and relabeled to separate data refresh, list auto-scroll, and host switching.

### Changed
- Unhealthy containers now show dark orange instead of red (the container is running but its health check is failing); stopped/exited containers stay red.

### Removed
- The Switch Host online-color override (added in 0.1.5) was removed. That key's color is a reachability indicator (green reachable, red not), so it is not user-configurable.

## [0.1.5] - 2026-07-08
### Added
- Open Profile action: a one-key shortcut that switches the Stream Deck to the bundled Docker Monitor profile for the connected device.
- Switch Host key has a configurable online background color (with reset); the offline state always stays red.
- Three new Host Metrics pages (enable via checkboxes; off by default): Disk usage % (fullest real filesystem with used/total), Temperature (hottest CPU sensor, colored by the sensor's own warning/critical thresholds), and GPU (utilization, VRAM %, temperature).
- Test button on each host in the connection editor — probes the Glances API with the entered details and reports success (with container count) or the exact failure inline.

### Changed
- Renamed to "Docker Monitor".
- Bundled profiles now install and activate automatically for the connected Stream Deck (15-key or XL).
- Swapped the greens: container status keys use the darker green, the Switch Host key the brighter one.
- Container CPU key text sized to match the Memory and Uptime keys.

## [0.1.4] - 2026-07-06
### Changed
- Starter profiles rearranged: host metrics (CPU/MEM/SWAP/LOAD, plus NET/DISK on XL) across the top row with the host switch in the corner; container rows below with scroll arrows in the last column.

### Fixed
- Pressing a Container Name key on an empty row no longer flashes the error triangle — it's simply a no-op.

## [0.1.3] - 2026-07-05
### Added
- Container keys now open the right service automatically: Glances 4 exposes port mappings, so a Name key press opens the container's first published port (override order: URL mapping → template → published port → Glances web UI).
- Every container key has a Column picker: Container Name, CPU, Memory, Uptime (primary), plus Status, Disk I/O, Network, and Image.
- Per-container disk I/O and network throughput columns, computed from Glances rates (or counter deltas on older servers).
- Alerts Only thresholds are configurable (CPU % and MEM %, default 50) with a reset button.
- Host CPU and MEM keys sort the container list by that metric when pressed.

### Changed
- Memory values now match Glances' MEM column (inactive page cache excluded).
- Auto Scroll is a checkbox with separate Interval and Pause fields (shown only when enabled); settings page notes all times are in seconds.
- List row selection is Auto by default; the manual row field only appears when Manual is chosen.
- Uptime key text enlarged to match the Memory key; Switch Host key text enlarged.
- Metric key text (container CPU/MEM/Uptime/Disk/Network/Image and all host-metric pages) is top-aligned instead of vertically centered.

## [0.1.2] - 2026-07-05
### Fixed
- Alerts-only mode flagged nearly every container: Glances reports the health-check string as the status (`healthy` instead of `running`), which the filter read as "not running". Status is now normalized (health carried separately), so healthy/quiet containers are correctly hidden.

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
