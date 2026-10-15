<!--
SPDX-FileCopyrightText: 2026 Keephaven LLC
SPDX-License-Identifier: AGPL-3.0-only
-->

# Keephaven Photos SSD

Your photo library, on a USB drive, running on a Windows PC you already own.
No account, no subscription, and nothing leaves the drive.

This repository is the documentation: what it is, what it needs, exactly what
it does, and the checksums of every release.

**It is open source, AGPL-3.0-only, the same as the Keephaven boxes.** The
source is at
[github.com/dafarusd/keephaven](https://github.com/dafarusd/keephaven) —
everything, including the Windows program that runs it, the drive layout and
the update path. Build your own or write a drive; both are the point.

---

## Early release

Free while it's early. If you grab it now it stays free for you. Later
versions will cost money. It's booted on one PC so far, so keep your originals
somewhere else too.

The drive is not included &mdash; you supply a USB SSD.

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

## Writing your drive

1. **You download one file**: `Keephaven-Setup.exe`, about 6 MB. Your update
   code is already inside it, so there is nothing to copy down or keep track
   of. That code isn't a licence and it doesn't identify you — it's how your
   drive finds its updates later.
2. Run it. Windows will warn you that the publisher is unknown; see
   [below](#the-two-warnings-you-will-see). Setup downloads Keephaven (about
   5.4 GB) and the writer, checks every piece against its published checksum,
   and refuses anything it can't check.
3. It then starts the writer, which shows you the one drive it is about to
   erase and what is on it now, and makes you type that drive's make and size
   before it touches anything.
4. It writes about 36 GB, then **reads all 36 GB back off the drive** and checks
   it against the published checksum. It prints PASS or FAIL in those words. On
   a laptop with a Core i3, over USB 3, the write took 2 minutes 19 seconds and
   the read-back a little over one.
5. Open the drive, double-click `Keephaven.exe`, and follow the setup page in
   your browser. Setup asks for no password at all.

Setup never touches a disk, and the writer never touches the network. They are
two programs for that reason: a tool that erases drives should have nothing in
it that a proxy, a certificate store or an antivirus can turn into a second
failure mode.

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
code and the version it's running — no account, no address book, no file list.
Your drive also sets its clock from a public time server, and the apps inside
check for their own versions, the same as they do on a Keephaven box.

An update is a signed image. The signature is checked on the drive, against a
public key baked into the read-only part of the system, before anything is
installed. A failed check rejects the update. It will not downgrade itself, and
nothing installs without you tapping to accept it.

Your code gates **bandwidth, not the software**. It is not a licence and it
grants you nothing you don't already have under the AGPL. If a code stops
working, the drive carries on exactly as it is, keeps every photo, and says on
its own screen that the code was not accepted — it never pretends to be a
network fault.

## The two warnings you will see

Windows SmartScreen will tell you the publisher is unknown, once for the writer
and once for Keephaven itself. The programs are not signed with a code-signing
certificate. Choose **More info**, then **Run anyway**.

If you would rather check for yourself first, every release's checksums are
published in this repository and alongside the download. In PowerShell:

```powershell
Get-FileHash <file> -Algorithm SHA256
```

## Licence and source

- Keephaven's own code, this edition and the boxes alike: **AGPL-3.0-only**.
  [LICENSE.txt](LICENSE.txt) is the full text,
  [NOTICE](NOTICE) says what it covers, and the source is at
  [github.com/dafarusd/keephaven](https://github.com/dafarusd/keephaven).
- The QEMU on the drive is GPL-2.0 and Keephaven patched it. The drive carries
  QEMU's licence, the patch in full, the build recipe and a written offer of
  the complete source.
- Everything else inside — the operating system and the apps — keeps its own
  licence. [THIRD-PARTY.md](THIRD-PARTY.md) lists them and says where to get
  the source.

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
