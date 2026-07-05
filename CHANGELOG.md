# Changelog

All notable changes to the Glances Docker Monitor Stream Deck plugin.
Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versions follow SemVer.

## [Unreleased]

### Changed
- Added the deploy pipeline (`npm run deploy`): syncs the package version into the manifest, runs tests/typecheck/build, and packs a versioned installer into `release/` (adopted from streamdeck-pihole, hardened to reject non-x.y.z versions and to version the output filename).
- Plugin identifier is now `com.marktastic.streamdeck-glances` (folder, manifest UUID, and all action UUIDs).

### Added
- Initial plugin: seven Stream Deck actions backed by the Glances REST API (v4 with v3 fallback).
- Container Name key — name on a status-colored background (green running/healthy, orange paused/restarting/starting, red stopped/unhealthy); press opens the container's URL (per-container mapping or `{name}`/`{host}` template).
- Container CPU / Memory / Uptime keys — values in Glances threshold colors (green / blue ≥50 / purple ≥70 / red ≥90); pressing a metric key sorts the list by it, pressing again flips direction. Default sort: CPU descending.
- Scroll List key — moves the visible container window up/down; shows list position. Optional auto-scroll pages through the list on a configurable interval (manual presses pause it for 15 s).
- Host Metrics key — cycles CPU, memory, swap, load average, network and disk I/O for the host, on a configurable interval or per press.
- Switch Host key — shows the active Glances host (green online / red offline) and cycles through any number of configured host profiles.
- Property inspectors (dependency-free): shared connection editor for host profiles (label, host/IP, port, protocol, optional Basic-auth credentials), refresh interval, auto-scroll interval; URL template + per-container URL overrides with live container-name suggestions.
- Unit tests for Glances payload parsing; icon generation pipeline; rollup/TypeScript build.
