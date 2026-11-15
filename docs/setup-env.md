Build Environment for Mira
==================================

This `setup-env.md` will guide you on how to setup up an environment to build and test the mira app on your system. This setup works for both VMs and Host machines running debian linux distribution as build environment. 

Debian Linux Installation Guide
-------------------------------







QEMU/KVM Setup
--------------

```sh
qemu-img create -f qcow2 debian.qcow2 256G
```

```sh
editor boot.sh
```

```sh
#!/bin/sh
qemu-system-x86_64 \
  -enable-kvm \
  -m 4G \
  -smp 4 \
  -cdrom <iso_filename> \
  -drive file=debian.qcow2,if=virtio,format=qcow2 \
  -device virtio-vga-gl \
  -display gtk,gl=on \
  -netdev user,id=net0 -device virtio-net-pci,netdev=net0 \
  -audiodev driver=pa,id=audio0 \
  -device AC97,audiodev=audio0
```

```sh
chmod +x boot.sh
./boot.sh
```

VirtualBox Setup
----------------


VMware Setup
------------
