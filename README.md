# CodeOS-Kernel

This is the kernel that powers CodeOS. It is the actual kernel source from
the CodeOS tree (`kernel/` directory), mirrored here so it can be built and
tracked on its own. This kernel is still in development — I recommend NOT
using it on actual hardware; run it in VirtualBox or QEMU instead

## Is it Linux-Based

No. This kernel does not use or take anything from Linux. It stands on its
own — not FreeBSD-based or anything — completely new.

## Story

I was on June 2, 2026, thinking about CodeOS when an idea hit me: "What if I
make a kernel?" Well, I did, and here is the result.

## Notes

Still in development, so do not expect it to run desktops like XFCE 4,
Hyprland, or Plasma — you have to wait for support, and the files can be copied by
```sh
git clone https://github.com/tech-for-everyone/CodeOS-Kernel/edit/main
```


## Layout

This repository duplicates the `kernel/` directory of the CodeOS tree one-to-one:

```
arch/       — per-arch support (x86_64, arm64)
boot/       — boot-time init
bootloader/ — limine bootloader pieces + secureboot keys
drivers/    — device drivers
fs/         — filesystem layer
kernel/     — core kernel (incl. the CSL scripting engine, script.c)
lvgl/       — vendored LVGL graphics library
mm/         — memory management
sched/      — scheduler
scripts/    — build helpers
userspace/  — in-kernel userspace
Makefile    — build entry point
linker.ld / linker.arm64.ld
```

The Rust components of the kernel live under `kernel/` too:
`rust_ow` (OpenWeb HTTP + HTML renderer), `rust_penrose` (window manager),
and `rust_hyperde` (desktop environment).

## Building

```sh
make            # x86_64 kernel → codeos-1-kernel.bin
make ARCH=arm64 # ARM64 build (needs aarch64-linux-gnu cross toolchain)
make iso        # bootable ISO
```

Run the result with QEMU:

```sh
qemu-system-x86_64 -cdrom codeos-1-kernel.iso
```

Note: the kernel Makefile also reads `../include` from the surrounding CodeOS
tree; provide that include path if building this repository fully standalone.

## Mirror status

Kept in sync with the `kernel/` directory of the CodeOS tree
(github.com/CodeOS-Comunity/HyperDE, branch `kernel-shell`). Build artifacts
and generated files are not committed (see `.gitignore`).

## License

GPL-3.0 (see LICENSE), corresponding to the CodeOS Kernel (COPYING).
