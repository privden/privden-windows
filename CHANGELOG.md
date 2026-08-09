# Changelog

All notable changes to privden are recorded here. Dates are ISO-8601.

This file starts at **0.1.3**, the first public release. Earlier versions were internal
builds and were never published — see [Before 0.1.3](#before-013) if you have one.

---

## [0.4.0] — 2026-08-09

Your privden server now reserves a permanent name of its own, setup asks fewer questions, the
server core is updated, and the PC no longer falls asleep while it is serving. Everything from
0.1.3 still works the same way on your local network.

Versions 0.2.0 through 0.3.12 were internal builds and were never published; the work in them
is part of this release. It is a large release for a small version jump: most of those builds
exist because each was made to check one thing on a real machine before the next was made.

### Your permanent privden name

- **First run reserves a name for your server.** You choose a short name and it becomes
  `yourname.privden.chat`, confirmed with a code sent to your email. The name is yours and is
  kept for the future — it is the name privden Connect will use to let people reach your server
  over the internet, by name, once Connect ships. For now your server still runs on your local
  network exactly as before, and clients still connect to its local address.
- **Names are checked as you type.** privden tells you whether a name is free and suggests
  alternatives when it is already taken; the reservation itself is the final word.
- **The reservation is kept alive automatically** by a quiet daily check-in, and is stored
  securely on your PC. If a name goes unused for a very long time it can be released — privden
  tells you once if that ever happens.
- If setup cannot reach the internet while reserving the name, it offers to **Retry** or to
  quit: a server needs its reserved name before it can start.

### Getting your name back after a reinstall

- **A name you already reserved can be restored on a new install.** Confirm the same email
  address and privden offers the name back instead of asking you to pick another one. There is
  a link on the name screen — *I already have a name* — for going straight there.
- Restoring is about the **name**, not your messages: a reinstall that deleted your data does
  not bring the data back, and privden says so plainly before you confirm.
- Uninstalling privden does **not** release your name. That is deliberate — the name stays
  yours, and this is the way to pick it up again.

### Simpler setup

- The installer no longer asks for the server name, the port, or the network-access mode on
  their own pages. The server name comes from the name you reserve at first run; the port
  (still `8008` by default) and a **“reachable only from this computer”** option move into an
  **Advanced** section of the first-run screen. By default your server stays reachable across
  your local network, as before. The installer now only asks where to install and which
  language to use.

### Updated server core

- **The bundled Tuwunel homeserver moves from v1.8.0 to v1.8.2**, bringing upstream's
  reliability and correctness fixes. Three of the Windows fixes privden used to carry on its
  own are now part of Tuwunel itself, so privden ships less of its own change to the server.
  Your messages, accounts and settings are unaffected — the database format is unchanged.

### The PC no longer falls asleep while it is serving

- **privden keeps the computer awake while the server is running** and the machine is on mains
  power. Until now a PC with ordinary power settings went to sleep on its own and stopped
  serving — most likely every night, with nothing on screen to say it had happened.
- **On battery it deliberately does nothing**, and it lets go of the machine within a minute of
  the server being stopped from the privden menu. Stopping the server is how you let a
  plugged-in machine sleep tonight; there is no setting to add, and nothing to remember to
  switch back.
- The boundary of all this is worth reading before you rely on privden:

  > **privden works while the computer is on and you are logged in.** After a restart, someone
  > has to log in to the computer before privden starts serving again. privden is meant for a
  > computer that stays plugged in — it is not designed to run on battery.

### Fixes

**Typing and layout**

- **Long text could not be typed into any field.** A single-line field stopped accepting
  characters once the text reached the right-hand edge — about thirty characters — and went
  quiet rather than scrolling. It affected seven fields: the user name and both password fields
  in the account window, and four in the first-run window. A long password or a long name
  simply could not be finished. Present since those windows were written, and easy to miss
  because everything anyone had tested was short.
- **The first-run window drew two controls on top of each other.** The *I already have a
  privden name* link and the **Advanced** toggle were placed at the same spot, so the toggle
  painted over the first half of the link and what shipped read “have a privden name” inside a
  stray box. The link now sits at the left of the button row and moves with it, and the window
  no longer leaves a band of empty space below its content.
- The bottom row of buttons on the first-run window is no longer clipped.
- The **Verify & reserve** button dropped the ampersand from its label and now shows it.
- Status lines during name reservation were all coloured as errors, so “that name is
  available” and “Sending code…” looked like failures. Each line now carries the right colour.

**Choosing a name**

- **“Next” now refuses a name the check has just called taken.** It used to move on anyway, so
  a name privden already knew was unavailable cost a real emailed code and three screens before
  being refused at the end.
- **The rule under the name field now says which letters.** Every language said “lowercase
  letters” and stopped there — which says nothing to someone looking at their own perfectly
  lowercase `é`, `ñ`, `ő` or `орыафлопа`. It now says `a`–`z`, digits and hyphens, in all five
  languages.
- **A name check that cannot reach the internet now says so.** It used to clear the line and
  leave an empty space where a verdict had been, which reads as “nothing to say” rather than
  “could not ask”.

**Language**

- **The Settings window was half-translated.** Opened with the interface in Russian it showed a
  Russian title bar and an English everything-else: only the title had ever gone through the
  translations. The whole window now follows the language you chose.
- **First run could overwrite the language you had chosen.** A PC set to Russian could run the
  whole of first run in English and then store English as your choice. Fresh installs were
  never affected; this only happened where a stored choice and the installer's handoff
  disagreed.
- The Russian heading on the name-recovery screen lost its last word to an ellipsis.
- Wording corrections across all five languages — a doubled conjunction, a Hungarian word in
  the wrong grammatical role, the Russian *Generate* button reading “create” instead, and
  hyphens standing in for dashes.

**The Settings window**

- Address lines were padded with spaces to line them up and came out ragged instead. They are
  laid out properly now.
- The window carried a network memo that explained how to forward a port without naming what
  that costs, and advertised voice and video ports for a feature privden does not ship. Both
  are gone — the same text had already been removed from the installer and nobody noticed it
  had a second home.

**The installer**

- **A message box told you to close privden and click OK to retry, and nothing retried.** It
  appeared when the installer could not stop a running privden; clicking OK led straight to a
  second box saying the installation had been cancelled. You were told to act, acted, and were
  then told it was too late. The box is gone; the installer stops a running privden by itself,
  which is the ordinary path and asks nothing.

**Your log file**

- **A damaged settings file could copy its own contents into privden's log.** When the settings
  file failed to parse, the error carried the offending line verbatim — and that line can be
  the server's registration secret. The log now records the position and the reason and says
  the line was left out on purpose. The log is append-only and lives on your PC, so anything
  written there stays there.

**The tray menu**

- The owner-account recovery item stayed available after the owner account had been created,
  and answered with a confusing message when used.

### Upgrading from 0.1.3

- **Installing over an existing privden leaves your data alone.** Your messages, accounts,
  settings and logs live in `%LOCALAPPDATA%\privden`, which the installer does not touch — it
  stops the running copy by itself, replaces the program, and starts again.
- **An upgrade never goes through first run**, by design. It keeps the server name it already
  has and does not ask for an email or reserve a name. A reserved `yourname.privden.chat` name
  is something a **fresh install** gets; an upgraded install carries on exactly as it did.
- **What has and has not been tested.** Upgrades were run repeatedly between the internal
  builds of this release, on a real machine, including the case where the running privden has
  to be stopped first. The particular step **from 0.1.3 to 0.4.0** was not walked end to end —
  0.1.3 was published but never actually installed by anyone outside the project, so the
  scenario has no one in it. If you are the exception and something looks wrong after
  upgrading, your data is still in `%LOCALAPPDATA%\privden`: uninstalling and installing again
  does not remove it.

### Unchanged since 0.1.3

- The local-network limitations from 0.1.3 still apply: access is within your own network only,
  the app-to-server link is plain HTTP (message *content* stays end-to-end encrypted), and
  clients connect by IP address rather than by domain name — see the 0.1.3 notes below for the
  full list.
- One item on that list is now settled: **iPhone works.** Element X on iOS connects to the
  server by local IP address just as Android and desktop clients do. The 0.1.3 notes listed
  iOS as untested; it has since been tested and it works.
- **Still not code-signed.** Windows SmartScreen warns when the installer runs. Verify the
  published SHA-256 before running it. The certificate is being obtained; it is a matter of
  paperwork rather than software.

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

[0.4.0]: https://github.com/privden/privden-windows/releases/tag/v0.4.0
[0.1.3]: https://github.com/privden/privden-windows/releases/tag/v0.1.3
