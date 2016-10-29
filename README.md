# Pinky

Pinky is an [NES] emulator written in [Rust] completely from scratch
based only on [publicly available documentation].

[NES]: https://en.wikipedia.org/wiki/Nintendo_Entertainment_System
[Rust]: https://www.rust-lang.org/en-US/
[publicly available documentation]: http://wiki.nesdev.com/w/index.php/Nesdev_Wiki

## Features

   * Accurate-ish (cycle accurate) 6502, PPU and APU emulation.
   * A testsuite based on test ROMs.
   * A PPU testsuite automatically generated from a transistor-level
     simulation of a real PPU.
   * Supports NROM (0) and MMC1 (1) mappers.
   * Can be compiled as a [libretro] core.

[libretro]: http://www.libretro.com/index.php/api/

There are still many things missing, including:

   * Unofficial 6502 instructions support.
   * Support for other mappers.
   * Accurate PPU sprite overflow.
   * Savestate support.
   * PAL support.

Currently this is **not** a production quality emulator, though
whatever games it can play (due to limited mapper support) it can
play quite well (e.g. such games as Super Mario Brothers, Donkey Kong
or Tetris; you can check out [nesmapper.txt] which will tell you
which game use which mapper).

[nesmapper.txt]: http://tuxnes.sourceforge.net/nesmapper.txt

## Getting started

Internally this project is split into multiple crates.

The `pinky-libretro` contains the libretro core of this emulator,
which is the intended way to run it. It should be compatible with
any libretro frontend, but it was only tested with [RetroArch].

After compiling the libretro core you can run it like this with RetroArch:

```
retroarch -L libpinky_libretro.so your_rom.nes
```

There's also a simple standalone SDL2-based frontend in the `pinky-devui`
directory; running it is just a matter of passing it a path to your game ROM
on the command line.

[Retroarch]: http://www.libretro.com/index.php/retroarch-2/

The `nes-testsuite` contains an emulator agnostic testsuite of NES roms,
which could be easily hooked to any other emulator simply by implementing
a single trait (see `nes/src/testsuite.rs`).

The `rp2c02-testsuite` contains a PPU testsuite which is autogenerated
with the help of [Visual2C02], which is a transistor-level simulator
of an actual NES PPU.

The `nes` contains the emulator itself. `mos6502` has the 6502 interpreter,
which could be useful for emulating other 6502-based machines.

[Visual2C02]: https://www.qmtpro.com/~nes/chipimages/visual2c02/

## There are already hundreds of NES emulators out there; why another?

Because why not? Writing a game console emulator is one of the most fun and
rewarding projects out there, and nothing can compare with the feeling of
beating one of your favorite games on an emulator you've wrote yourself.

The choice of NES is also an obvious one - it's the least time consuming
console to emulate simply due to the fact that it's extremely well documented.
