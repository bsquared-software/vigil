<h1 align="center">Vigil</h1>

<p align="center">A native macOS server monitor: live metrics, Docker, a terminal and files for your Linux servers, all over SSH.</p>

<p align="center">
  <img src="https://img.shields.io/badge/macOS-26%2B-08090A?logo=apple&logoColor=white" alt="macOS 26+">
  <img src="https://img.shields.io/badge/Swift-6-08090A?logo=swift&logoColor=F05138" alt="Swift 6">
  <a href="LICENSE"><img src="https://img.shields.io/badge/licence-MIT-3FCB86" alt="MIT licence"></a>
  <a href="https://bsquared.software"><img src="https://img.shields.io/badge/built%20by-BSquared-3FCB86" alt="Built by BSquared"></a>
</p>

Vigil keeps an eye on the servers you run. Add a server once, and you get one window with
everything you'd otherwise open three terminals for. It needs nothing installed on the server:
if you can `ssh` in, Vigil works.

## What it does

- **Dashboard.** CPU and load, memory, disk per mount, network, uptime and the state of
  your `systemd` services, refreshed every few seconds, with charts.
- **Docker.** Every container with its status and live CPU and memory. Start, stop and
  restart containers, and read their logs.
- **Terminal.** A real interactive shell (PTY) on the server, with a command history sidebar.
- **Files.** Browse the server's file system, preview text files, upload and download by
  drag and drop, create folders and delete files.
- **Menu bar and alerts.** Server status in the menu bar, and a notification when CPU or disk
  use crosses a threshold (90% by default, set in Settings).
- **Shortcuts.** A "Check server status" action for the Shortcuts app.
- Multiple servers and windows, keyboard shortcuts throughout, and VoiceOver labels.

## How it works

Vigil uses the `ssh` already on your Mac (`/usr/bin/ssh`), so your `~/.ssh/config` hosts,
keys and agent work as they do in Terminal. It opens one shared connection per server
(SSH `ControlMaster`) and runs everything over it: the metrics are read from standard tools
(`top`, `free`, `df`, `ip`, `ss`, `systemctl`, `docker`) and parsed on the Mac.

- **Authentication:** SSH keys. Vigil finds the keys in `~/.ssh/` for you. Password login isn't
  supported yet.
- **Storage:** server details in `~/Library/Application Support/Vigil/`. Nothing leaves your Mac.

## Build

Requires macOS 26, Xcode 26 and XcodeGen (`brew install xcodegen`).

```sh
xcodegen generate
open Vigil.xcodeproj          # then Run, or:
xcodebuild -scheme Vigil test # 24 tests
```

The original design is in [`docs/plans/`](docs/plans/). It planned to use Citadel for SSH;
the app ships with the system `ssh` instead and has no third-party dependencies.

## Licence

[MIT](LICENSE). Maintained by [BSquared](https://bsquared.software), a UK software company.
Issues and pull requests are welcome.
