Build Environment for Kiri 
==========================

This `setup-env.md` will guide you on how to setup up an environment to build and test the Kiri app on your system. This setup works for both VMs and Host machines running debian linux distribution as build environment. 

> Note: Debian is recommended for this project cause we rely on a stable releases.

QEMU/KVM Setup
--------------

Create the virtual disk image for qemu.
```sh
> qemu-img create -f qcow2 debian.qcow2 256G
```

Open an editor and create a file named `boot.sh`.
```sh
> editor boot.sh
```

Copy and Paste the below script in `boot.sh`.
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

Make it executable and run the script to boot the virtual machine.
```sh
> chmod +x boot.sh
> ./boot.sh
```
