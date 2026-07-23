# privden

**Your den. Your rules.**

A free Windows app that turns your PC into a private chat server, compatible with
[Matrix](https://matrix.org/). Your messages, your data, your control.

*[Читать по-русски](README.ru.md)*

> **This repository holds releases, not source code.** privden is proprietary software; the
> download below is the product. See [Source code](#source-code) for what is and isn't open,
> and why.

---

## Download

**[Latest release →](https://github.com/privden/privden-windows/releases/latest)**

`privden-setup.exe` — a single installer, about a minute to run.

### Requirements

| | |
|---|---|
| **OS** | Windows 10 or 11, 64-bit |
| **Rights** | Administrator (the installer writes to `Program Files` and registers the app) |
| **Disk** | ~200 MB for the program, plus your messages and files |
| **Network** | A home network. See [How you connect](#how-you-connect) — the first release is for use inside your own network |

macOS is planned; there is no macOS build yet.

### Verify your download

Every release publishes the SHA-256 of `privden-setup.exe` in its release notes. In
PowerShell:

```powershell
Get-FileHash -Algorithm SHA256 .\privden-setup.exe
```

Compare the output with the hash in the release notes. If they differ, do not run the file.

**This matters more than usual right now**, because privden is not yet code-signed — see
below.

### Windows will warn you

privden is not code-signed yet, so Windows SmartScreen will show **"Windows protected your
PC"** when you run the installer. That warning is accurate: it means Windows cannot confirm
who published this file. Check the SHA-256 first, then choose **More info → Run anyway** if
you decide to proceed.

Code signing is in progress. Once it lands, this warning goes away and the publisher name
appears in the elevation prompt instead. The SHA-256 will keep being published either way.

---

## What privden does

You install it on a PC at home. That PC becomes a Matrix chat server for your household —
your partner, your kids, your flatmates, a small team. Everyone chats through their normal
Matrix app; the messages live on your machine rather than on somebody else's service.

**Working today:**

- Direct messages and small group rooms
- Sending and receiving files
- End-to-end encryption on every conversation
- Several accounts on one server, created from the tray app
- Works with any Matrix client — Element, Element X, FluffyChat, SchildiChat and others
- Installer and app in **English, French, Spanish, Russian and Hungarian**

**Not in this release:**

- **Access from outside your network.** See below — this is the honest part.
- Voice and video calls
- Federation with other Matrix servers
- Bridges to WhatsApp, Telegram and similar

We would rather ship a small thing that works than a long list that half-works.

### How you connect

Your apps reach the server by typing the **IP address** of the PC it runs on, for example
`http://192.168.1.50:8008` — the port is set during installation and `8008` is only the
default. Your PC's address on your own network; nothing is exposed to the internet.

Two things to know, plainly:

- **That connection is not itself encrypted.** Your *messages* are, by Matrix end-to-end
  encryption — but the link between app and server is plain HTTP inside your own network.
  Anyone already on your network could see traffic metadata. Transport encryption is part of
  the planned paid service, not of this release.
- **Type the IP address, not a domain name.** Modern Matrix clients treat a domain name as an
  instruction to go looking for the server over HTTPS on port 443, which this release does not
  serve. An IP address skips that and connects directly.

Reaching your server from outside the house, by name, over TLS is what **privden Connect** is
being built to do. It is not part of this release and is not sold yet — see
[privden.com](https://privden.com).

### Where things go

| What | Where |
|---|---|
| Program files | `C:\Program Files\privden` |
| Your messages, accounts, config, logs | `%LOCALAPPDATA%\privden` |

Uninstalling removes the program. Your data directory is yours — check it before deleting
anything.

---

## Source code

**The source is private and stays that way.** No fork, no pull requests. That is a deliberate
choice, and it is worth being straight about what it does and doesn't mean:

- **What's closed:** the installer, the tray application, the first-run setup, the
  translations. Product work, with no bearing on whether your messages are secret.
- **What's open, and isn't ours:** the [Matrix protocol](https://spec.matrix.org/), its
  end-to-end encryption, and the [Tuwunel](https://github.com/matrix-construct/tuwunel)
  homeserver that privden packages and runs (Apache-2.0). Anyone wanting to audit the
  cryptography audits it upstream, where it is public and reviewed.
- **Where closing it genuinely costs you something:** `privden.exe` creates your accounts and
  handles your password, so it sits in the trust path for *credentials* even though not for
  message encryption. "Read the code" is not an answer we can offer. Code signing and the
  published SHA-256 are what we offer instead.

The reason is capacity, not revenue. A public repository is a standing promise to triage
issues and review contributions, and an abandoned one damages trust more than an absent one.

---

## Bugs and questions

[Issues](https://github.com/privden/privden-windows/issues) are open. Bug reports and
questions about using privden are welcome here.

A useful report includes your Windows version, the privden version (tray menu → About), what
you did, and what happened. Logs live in `%LOCALAPPDATA%\privden\logs`.

> **One caveat on logs:** while the tray app is running, Windows Explorer and `dir` report a
> stale size and timestamp for `privden.log`. Open the file and read it — do not judge it by
> the size column.

Feature requests are read but not promised. Because the source is closed, issues about the
code itself cannot be acted on publicly.

---

## Licence

privden is proprietary software, covered by the End User Licence Agreement in
[LICENSE](LICENSE). The installer shows it before installing and copies it to the install
directory as `LICENSE.txt`.

The third-party components shipped inside it are **not** covered by that agreement and stay
under their own licences:

| Component | Licence | Attribution |
|---|---|---|
| Tuwunel homeserver (`tuwunel.exe`) | Apache-2.0 | [NOTICE](NOTICE) |
| Bundled data files (EFF wordlist, password blocklist) | CC BY 3.0 US / MIT | [NOTICE](NOTICE) |
| Rust crates linked into both binaries | mixed | `THIRD-PARTY-NOTICES.md`, attached to each release |

`THIRD-PARTY-NOTICES.md` is generated per build and attached to the release it belongs to,
rather than tracked here, so it can never describe a different build than the one you
downloaded. It is also installed alongside the program.

---

## Links

- [privden.com](https://privden.com) — what privden is, where it's going
- [CHANGELOG.md](CHANGELOG.md) — what changed, release by release
- [Matrix](https://matrix.org/) — the open protocol privden speaks
- [Tuwunel](https://github.com/matrix-construct/tuwunel) — the homeserver privden packages
