# privden

**Your den. Your rules.**

A Windows app that turns your PC into a private chat server, compatible with
[Matrix](https://matrix.org/). Your conversations and files stay on your computer.

*[Читать по-русски](README.ru.md)*

> **This repository holds releases, not source code.** privden is proprietary software; the
> download below is the product. See [Source code](#source-code) for what is open and what is not.

---

## Download

**[privden for Windows — the latest release →](https://github.com/privden/privden-windows/releases/latest)**

`privden-setup.exe` — one installer, about a minute to run.

Plans and prices: **[privden.com/pricing](https://privden.com/pricing/)**.
How to use it: **[the documentation](https://privden-wiki.vercel.app/)**.

### Requirements

| | |
|---|---|
| **System** | Windows 10 or 11, 64-bit |
| **Rights** | An administrator account, to install |
| **Disk** | About 200 MB for the program, plus your messages and files |
| **First run** | An internet connection and an email address, once, to reserve your server's name |

**A work computer may not let privden work.** Computers managed by an employer — with company
security software, a company VPN or device management — often stop other devices from reaching a
server on them, and quietly. If your computer belongs to your employer, use a personal one.

There is no macOS or Linux download yet.

### Signed by Privden LLC

The installer and every program it installs are signed by **Privden LLC**. Windows shows that name
when it asks for permission to install, and the signature is what lets privden run where Windows
11's Smart App Control is switched on.

### Check your download

Every release publishes the SHA-256 of `privden-setup.exe` in its notes. In PowerShell:

```powershell
Get-FileHash -Algorithm SHA256 .\privden-setup.exe
```

If the two differ, do not run the file.

---

## What privden does

You install privden on a computer at home or in the office. That computer becomes a private chat
server for the people you invite. They chat with ordinary Matrix apps — Element X, FluffyChat,
Element and others — and the conversations and files stay on your computer rather than on somebody
else's service. Messages are end-to-end encrypted by default.

The server runs as a Windows service, so it comes back by itself after a restart, before anyone
signs in. privden is meant for a computer that stays plugged in: while the server runs, it keeps
such a computer from falling asleep, and on battery it does not. The privden menu adds people,
makes and restores backups, and moves privden to another computer.

privden speaks English, French, Spanish, Russian and Hungarian.

### Where things go

| What | Where |
|---|---|
| The program | `C:\Program Files\privden` |
| Your messages, accounts, settings and logs | `C:\ProgramData\privden` |

Uninstalling removes the program, and asks before it touches your data.

---

## Source code

**The source is private and stays that way.** No fork, no pull requests. What that does and does not
mean:

- **What is closed:** the installer, the privden app, the setup, the translations. Product work,
  with no bearing on whether your messages are secret.
- **What is open, and is not ours:** the [Matrix protocol](https://spec.matrix.org/), its end-to-end
  encryption, and the [Tuwunel](https://github.com/matrix-construct/tuwunel) server that privden
  runs (Apache-2.0). Anyone who wants to audit the cryptography audits it there, where it is public.
- **Where closed source costs you something:** `privden.exe` creates your accounts and handles your
  password, so it is trusted with *credentials*, though not with message encryption. "Read the
  code" is not an answer we can offer; the signature and the published SHA-256 are.

---

## Bugs and questions

[Issues](https://github.com/privden/privden-windows/issues) are open, for bug reports and questions
about using privden. A useful report says your Windows version, the privden version (in
**Settings**), what you did, and what happened. Logs are in `C:\ProgramData\privden\logs`.

Feature requests are read but not promised. Because the source is closed, issues about the code
itself cannot be acted on publicly.

---

## Licence

privden is proprietary software, covered by the End User Licence Agreement in [LICENSE](LICENSE).
The installer shows it before installing and copies it to the install directory as `LICENSE.txt`.

The third-party components inside it are **not** covered by that agreement and keep their own
licences:

| Component | Licence | Attribution |
|---|---|---|
| Tuwunel server (`tuwunel.exe`) | Apache-2.0 | [NOTICE](NOTICE) |
| Bundled data files (EFF wordlist, password blocklist) | CC BY 3.0 US / MIT | [NOTICE](NOTICE) |
| Rust crates built into the programs | mixed | `THIRD-PARTY-NOTICES.md`, attached to each release |

`THIRD-PARTY-NOTICES.md` is generated for each build and attached to the release it belongs to, so
it always describes the build you downloaded. It is also installed with the program.

---

## Links

- [privden.com](https://privden.com) — what privden is
- [Plans and prices](https://privden.com/pricing/)
- [Documentation](https://privden-wiki.vercel.app/)
- [CHANGELOG.md](CHANGELOG.md) — what changed, release by release
- [Matrix](https://matrix.org/) — the open protocol privden speaks
- [Tuwunel](https://github.com/matrix-construct/tuwunel) — the server privden runs
