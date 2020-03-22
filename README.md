# kmodcache

Annoyed by those times when it was not possible to simply plug a USB because the current kernel's modules were removed after a kernel upgrade, and inspired by the [original kmodcache](https://aur.archlinux.org/packages/kmodcache) and [kernel-modules-hook](https://github.com/saber-nyan/kernel-modules-hook) this project was born.

kmodcache performs a copy of the current kernel's modules under `/usr/lib/modules` into the RAM (around 40MB for xz compressed modules is stored in `/var/run` ) and temporarily points modprobe and modinfo to them.

The copy process is triggered by a pacman hook only when the current kernel is upgraded.

kmodcache does not use systemd, instead it adds `/run/sbin` to PATH to temporarily store the modprobe and modinfo that points to the cached modules.

Thought the PKGBUILD targets Arch Linux, kmodcache is written having POSIX in mind and should be able to run in any POSIX system. You may want to change the variable where the backup is performed.
