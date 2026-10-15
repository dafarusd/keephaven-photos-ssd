# Keephaven Photos SSD 2026.10.18

Early release. Free while it's early. If you grab it now it stays free for you. Later versions
will cost money. It's booted on one PC so far, so keep your originals somewhere else too.

Get it at [keephaven.co/ssd](https://keephaven.co/ssd). The download is six files and your own
update code.

## Checksums

The writer checks these for you before it touches a disk, and again after it writes. They are
here so you can check them yourself first. In PowerShell: `Get-FileHash <file> -Algorithm SHA256`.

| File | What it is |
|---|---|
| `keephaven-photos-ssd-2026.10.18.img.gz.sha256` | the download |
| `keephaven-photos-ssd-2026.10.18.img.sha256` | the drive once written, which the writer reads back and compares |
| `Keephaven-Writer.exe.sha256` | the writer itself |

## Source

AGPL-3.0-only, all of it, at
[github.com/dafarusd/keephaven](https://github.com/dafarusd/keephaven), tagged
`drive-2026.10.18`. Each drive names that tag and its own build id in `QEMU-SOURCE.txt` at the
drive's root.
