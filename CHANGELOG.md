# Changelog

All notable changes to privden are recorded here. Dates are ISO-8601.

This file starts at **0.1.3**, the first public release. Earlier versions were internal
builds and were never published — see [Before 0.1.3](#before-013) if you have one.

---

## [0.1.3] — 2026-07-23

The first public release. A private Matrix chat server for a Windows PC, for use inside your
own network.

### What it does

- **Local Matrix homeserver**, packaged from [Tuwunel](https://github.com/matrix-construct/tuwunel)
  v1.8.0 and run as a tray application (`privden.exe`).
- **Direct messages, group rooms, and file transfer**, with Matrix end-to-end encryption on
  every conversation.
- **Account creation from the tray** — an owner account at first run, and further accounts
  for the household afterwards.
- **Works with any Matrix client** — Element, Element X, FluffyChat and SchildiChat are
  known-good. Clients connect to the PC's address on the local network
  (`http://<ip>:<port>`); the port is chosen during installation, and `8008` is the default.
- **Five languages** in both the installer and the application: English, French, Spanish,
  Russian, Hungarian. The installer follows the language chosen at setup.

### Installation

- Installs to `C:\Program Files\privden` in 64-bit mode. Requires administrator rights.
- Messages, accounts, configuration and logs live in `%LOCALAPPDATA%\privden` and are left in
  place when the program is uninstalled.
- The licence agreement is shown during setup, and `LICENSE.txt`, `NOTICE.txt` and
  `THIRD-PARTY-NOTICES.md` are installed alongside the program.
- Upgrading from 0.1.2 preserves messages, accounts and settings. Verified on Windows.

### Known limitations

These are deliberate for a first release, not defects:

- **No access from outside your network.** Reaching the server by name, over TLS, from
  anywhere is what privden Connect is being built for; it is not part of this release.
- **The connection between app and server is not encrypted.** Message *content* is protected
  by end-to-end encryption, but the link itself is plain HTTP within your own network.
- **Connect by IP address, not by domain name.** Modern Matrix clients resolve a domain name
  by looking for the server over HTTPS on port 443, which this release does not serve.
- **No voice or video calls, no federation, no bridges.**
- **iOS is untested.** Android, Windows and macOS clients have been verified over the local
  network; no iPhone has been tried yet, and Apple's transport policy may reject a plain-HTTP
  connection.
- **Not code-signed.** Windows SmartScreen will warn when the installer runs. Verify the
  published SHA-256 before running it.

---

## Before 0.1.3

**0.1.2** — internal build, 2026-07-19. Not published. The first version to install in
64-bit mode, which is why it is the only version with a supported upgrade path to 0.1.3.

**0.1.1 and earlier** — internal builds. **No upgrade path; do not install 0.1.3 over one.**
These installed in 32-bit mode and registered themselves under `Wow6432Node`, where the
current installer deliberately does not look. It will not detect such an install and will set
itself up as a *second, parallel copy* rather than upgrading. Uninstall the old version
manually first — look for privden in `C:\Program Files (x86)\privden`.

This should affect nobody: 0.1.1 was never released publicly. It is recorded here so that
anyone holding an internal build does not discover it the hard way.

---

[0.1.3]: https://github.com/privden/privden-windows/releases/tag/v0.1.3
