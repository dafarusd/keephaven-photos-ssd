<!--
SPDX-FileCopyrightText: 2026 Keephaven LLC
SPDX-License-Identifier: LicenseRef-Keephaven-Proprietary
-->

# Keephaven Photos SSD

Your photo library, on a USB drive, running on a Windows PC you already own.
No account, no subscription, and nothing leaves the drive.

This repository is the documentation: what it is, what it needs, exactly what
happens when you buy it, the checksums of every release, and an honest
side-by-side against everything else in the category — including where we come
out worse.

**The code for this edition is not here.** The box editions of Keephaven are
open source under the AGPL at
[github.com/dafarusd/keephaven](https://github.com/dafarusd/keephaven), and the
system inside the SSD edition is built from that same source. The Windows
program that runs it, the drive layout and the update path are ours and are not
published. [LICENSE.txt](LICENSE.txt) says precisely which is which.

---

## What it costs

**$39, one time.** One purchase is one Keephaven: write it to as many drives as
you like, run one at a time. Updates are included with no end date — there is no
subscription and there never will be. If it isn't for you, email
support@keephaven.co within 30 days of buying and you get the full price back;
your update code is switched off and the drive keeps working as it is.

The drive is not included. Checkout opens soon.

## What it is

A Windows program on a USB drive. Double-click it and your Keephaven starts —
the same NixOS system that runs on the Keephaven Photos box, running on your PC
instead of on a Raspberry Pi. Your photos go on the drive, not into anyone's
cloud.

Photos are served by [Immich](https://immich.app): background upload from your
phone, face grouping, search by what's in the picture, albums, shared links.

## What you need

- A Windows PC, 64-bit, with **8 GB of RAM** and a free **USB 3** port — either
  the oval USB-C kind or the older rectangular one.
- A **USB SSD of 64 GB or more**, in a USB enclosure. **The drive is not
  included.** You buy it, you own it, and you can take it apart and move it to
  another enclosure whenever you like.
- Thunderbolt and USB4 enclosures are **not supported**: Windows reports those
  as internal drives rather than USB, and the writer will not offer them.

A bigger drive is simply more room for photos. 64 GB is the floor, not a
recommendation.

## What happens when you buy it

1. You get a download folder: the image (about 5.4 GB compressed), a small
   writer program, three checksum files, a how-to, and one file that is yours
   alone — `Keephaven-code.txt`, your update code.
2. Keep all of it in one folder and run the writer. Windows will warn you that
   the publisher is unknown; see [below](#the-two-warnings-you-will-see).
3. The writer shows you the one drive it is about to erase and what is on it
   now, and makes you type that drive's make and size before it touches
   anything.
4. It writes about 36 GB, then **reads all 36 GB back off the drive** and checks
   it against the published checksum. It prints PASS or FAIL in those words. On
   a laptop with a Core i3, over USB 3, the write took 2 minutes 19 seconds and
   the read-back a little over one.
5. Open the drive, double-click `Keephaven.exe`, and follow the setup page in
   your browser. Setup asks for no password at all.

You can write your drive as many times as you like with the same download and
the same code — a new drive, a bigger drive, the same drive after a mistake.
See [HOW-TO-WRITE-THE-DRIVE.txt](HOW-TO-WRITE-THE-DRIVE.txt) for the full text
that ships with the download.

## Where your Keephaven lives

- On that PC: `http://localhost`
- On your phone, on the same home network: the address the Keephaven window
  shows you.

Your password is in `Keephaven-password.txt` on the drive itself. A Keephaven
box has it printed on a sticker underneath; a drive has this file instead.
Anyone who can read the drive can read that file, so treat the drive the way
you would treat the box.

## What it leaves on your PC

Nothing is installed. One folder — `C:\ProgramData\Keephaven` — holds a copy of
the program and a log, and you can delete it whenever you like. While Keephaven
is running it opens ports 80, 8888 and 2283 in the Windows firewall for itself,
on home and domain network profiles, and closes them again when you stop it.

To stop: type `q` in the Keephaven window and wait for "safe to unplug".

## Updates

Your drive asks for a new version once a day. That request carries your update
code and nothing else — no account, no address book, no file list.

An update is a signed image. The signature is checked on the drive, against a
public key baked into the read-only part of the system, before anything is
installed. A failed check rejects the update. It will not downgrade itself, and
nothing installs without you tapping to accept it.

Your code gates **bandwidth, not the software**. If a code stops working, the
drive carries on exactly as it is, keeps every photo, and says on its own screen
that the code was not accepted — it never pretends to be a network fault.

## The two warnings you will see

Windows SmartScreen will tell you the publisher is unknown, once for the writer
and once for Keephaven itself. The programs are not signed with a code-signing
certificate. Choose **More info**, then **Run anyway**.

If you would rather check for yourself first, every release's checksums are
published in this repository and alongside the download. In PowerShell:

```powershell
Get-FileHash <file> -Algorithm SHA256
```

## What it does not do

Not a roadmap. These are true today.

- **The drive is not encrypted.** Anyone holding it can read your photos, the
  same as anyone holding a Keephaven box. Keep it where you would keep the box.
- **File sharing over the network does not work on a PC.** Windows itself uses
  the one port that needs. Everything through the web page works normally; a
  Keephaven box has no such limit.
- **One login, shared.** Per-person accounts are planned, not built.
- **It runs while the PC runs.** Close the window and your Keephaven stops.
- **Remote access from outside your house has not been tested on a drive.** It
  works on the boxes. On a drive it is untried, so it is not a feature here.
- **No update has yet been installed on a drive end to end.** The path is built,
  signed and tested, and the feed is live. The full round trip on real hardware
  has not happened yet.

## How it compares

[COMPARISON.md](COMPARISON.md) puts the three Keephaven editions beside
twenty-one other ways to keep your photos — Umbrel, Start9, Zima, Synology,
QNAP, TerraMaster, UGREEN, WD, Ente, Immich, PhotoPrism, Nextcloud, iCloud and
Google Photos — with a source and a date on every cell.

It ends with **Where Keephaven is worse**, which is eighteen items long. That
section is the point of the document.

## Licence and source

- This edition: [LICENSE.txt](LICENSE.txt). Keephaven's own code for it is not
  free software and is not published.
- The box editions: AGPL-3.0-only,
  [github.com/dafarusd/keephaven](https://github.com/dafarusd/keephaven).
- Everything else inside — the operating system, the apps, and the QEMU the
  drive runs on — keeps its own licence. [THIRD-PARTY.md](THIRD-PARTY.md) lists
  them and says where to get the source.

## Releases

Each release is published with the SHA-256 of the image, the compressed image
and the writer. Nothing is listed here yet.

---

Built solo by [@Dafarusd](https://x.com/Dafarusd) — local-first software and
hardware you own.

Keephaven — [keephaven.co](https://keephaven.co) ·
[box source](https://github.com/dafarusd/keephaven) ·
[X](https://x.com/Keephaven) ·
[Facebook](https://www.facebook.com/profile.php?id=61592155452190)

support@keephaven.co
