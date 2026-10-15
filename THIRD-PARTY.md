<!--
SPDX-FileCopyrightText: 2026 Keephaven LLC
SPDX-License-Identifier: LicenseRef-Keephaven-Proprietary
-->

# Third-party software in the Keephaven Photos SSD

Keephaven's own code for this edition is proprietary, all of it, including the modules
it shares with the box editions - Keephaven LLC wrote them and a copyright holder may
license its own work twice. See LICENCE.txt. The box editions stay AGPL-3.0-only and
public and are unaffected.

Everything below is other people's work, used unmodified as its makers publish it.
Those licences are not Keephaven's to change and nothing here tries to.

The drive also contains other people's software. Each keeps its own licence, and
nothing in Keephaven's licence changes that or can.

## The app

This edition is Photos: Immich and what it needs, and nothing else. The container
images are pinned by digest in modules/images.nix, taken from the same upstream
index as the box editions, so these are the same projects under the same licences.

| Component | Role | Licence |
|---|---|---|
| Immich (server + machine learning) | Photos | AGPL-3.0 |
| Immich Postgres with VectorChord | Photos database | see below |
| Valkey | Photos cache | BSD-3-Clause |

Immich: https://github.com/immich-app/immich
Immich Postgres: Postgres itself is under the PostgreSQL License; VectorChord is
AGPL-3.0 or Elastic License 2.0; Immich's image build files are AGPL-3.0.
  https://github.com/immich-app/base-images
  https://github.com/tensorchord/VectorChord
Valkey: https://github.com/valkey-io/valkey

## QEMU, which is the part Keephaven modified

QEMU 11.1.0 is GPL-2.0. Keephaven redistributes a Windows binary it built, with one
patch of its own to block/file-win32.c. That patch is a derivative of GPL-2.0 code
and is GPL-2.0 whoever wrote it, and so is the script that compiles it. Every drive
carries QEMU's licence, the patch in full, the build recipe, the package pin, and a
written offer of the complete corresponding source good for three years. See
QEMU-SOURCE.txt and QEMU-LICENCE.txt.

## The operating system on the drive

Built from nixpkgs at the revision in qemu-build-flake.lock; nix build fetches the
same inputs this image was built from. Every package keeps its own licence, recorded
in its nixpkgs meta.license. The main ones:

| Component | Licence |
|---|---|
| nixpkgs package expressions | MIT |
| Linux kernel (x86-64) | GPL-2.0-only |
| systemd, its EFI stub and ukify, which build linux.efi | LGPL-2.1-or-later |
| Docker | Apache-2.0 |
| Samba | GPL-3.0 |
| Tailscale | BSD-3-Clause |
| Avahi | LGPL-2.0-or-later |
| minisign | ISC |
| OpenSSH | BSD-2-Clause |
| Python | Python-2.0 (PSF) |
| Go standard library, in the Windows program | BSD-3-Clause |

Samba is in the image although file sharing over the house network does not work
while Keephaven runs on a PC; README.txt says so.

The app licences were checked 2026-09-28 against each project's GitHub licence field
and nixpkgs meta.license. The QEMU and operating-system rows were checked 2026-10-13
against the build files in this image.
