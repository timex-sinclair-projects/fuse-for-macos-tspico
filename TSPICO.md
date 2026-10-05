# Fuse for macOS with a TS-Pico

This is [Fuse for macOS](https://github.com/fmeunier/fuse-for-macos) with a
TS-2068 that has a
[TS-Pico](https://github.com/timex-sinclair-projects/tspico-firmware-build)
plugged in. The TS-Pico work is on `tspico-device`. Its `fuse` submodule is
[fuse-macos-tspico-core](https://github.com/timex-sinclair-projects/fuse-macos-tspico-core)
(a fork of fmeunier/fuse), on that repository's `tspico-device` branch.

It's called **Fuse TS-Pico** (bundle ID
`io.github.timex-sinclair-projects.fuse-tspico`), so it sits beside an
upstream Fuse without sharing its preferences, and it doesn't update itself
from upstream's feed.

The TS-Pico itself isn't emulated here. Every access to ports 0Eh/0Fh goes to
`pico_host`, which runs the real TS-Pico firmware with its SD card in a folder
on your Mac. This is version 1 of
[the bridge spec](https://github.com/timex-sinclair-projects/tspico-firmware-build/blob/main/docs/EMULATOR_BRIDGE.md),
the same as the Linux and Windows Fuse in
[fuse-tspico](https://github.com/timex-sinclair-projects/fuse-tspico).

## Using it

1. Split the TS-Pico ROM (`TSPICO-21.ROM`) into two 16K halves, and choose
   them in Preferences > ROMs as the TS2068's two ROMs:

       head -c 16384 TSPICO-21.ROM > tspico-home.rom
       tail -c 16384 TSPICO-21.ROM > tspico-exrom.rom

2. In Preferences > Peripherals, choose **TS-Pico (TS 2068)**. The bridge
   address defaults to `tcp:127.0.0.1:2068`.
3. Start `pico_host`, then choose the TS 2068 machine.

## Building

As upstream (see README). Before building, `git submodule update --init`. To
build from a folder that iCloud Drive syncs, such as `~/Documents`, copy it out
first: iCloud's Finder attributes make `codesign` fail.
