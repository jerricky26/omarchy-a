# iPad 7 (J171) notes

Personal device notes for running Linux on an iPad 7th generation (2019, 10.2-inch, Wi-Fi, A10 Fusion / t8010, board J171).

## Build

- Kernel: Hoolock / Orchard Linux tree at `6831bc701`, built with `CONFIG_ARCH_APPLE=y` and `CONFIG_ARM64_16K_PAGES=y`.
- Device tree: `arch/arm64/boot/dts/apple/t8010-j171.dtb`.
- Bootloader: Hoolock m1n1, packed as `m1n1 + bootargs + dtb + Image.gz + initramfs` into `m1n1-linux.bin`.
- Boot args: `console=tty0 consoleblank=0 loglevel=8 clk_ignore_unused panic=0 rdinit=/init`.
- Host: x86_64 ThinkPad on Ubuntu 26.04, connected over USB.

## Boot (tethered)

1. Put the iPad in DFU mode.
2. `palera1n -lp -k Pongo.bin`
3. `printf '/send m1n1-linux.bin\nbootm\n' | pongoterm`

## Caveats

- The iPad does not charge while in DFU, pongoOS, or Linux. Start each session with a good charge and boot back into iPadOS to recharge.
- Linux runs from RAM only; nothing is written to the iPad's storage.
- No GPU acceleration, touchscreen, Wi-Fi, or audio on A10 yet.
