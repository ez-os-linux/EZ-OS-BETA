# EZ OS (beta)

Download the ISO from [Releases](https://github.com/ez-os-linux/EZ-OS-BETA/releases).

**Community, help and beta testing:** [join the EZ OS Discord](https://discord.gg/sP9yD5SR5)

```
EZ OS 0.7.0 - TRIAL VERSION
===============================
Tested in virtual machines only, never on real hardware.

1. CHECK THE DOWNLOAD
   Linux:   sha256sum -c SHA256SUMS
   Windows: certutil -hashfile EZ-OS-0.7.0-x86_64.iso SHA256     then compare with SHA256SUMS

2. TRY IT SAFELY: KVM/QEMU virtual machine (recommended)
   Settings: UEFI, Secure Boot DISABLED, 4 GB of RAM, a NEW 30 GB virtual disk, virtio graphics with 3D if possible.

   a) With virt-manager
      - New machine > Local media > pick the ISO > system: "Generic Linux"
      - Memory 4096, 4 CPUs, 30 GB disk (new)
      - Tick "Customize configuration before install"
      - Overview > Firmware: UEFI (x86_64), WITHOUT "secboot"
      - Video: Virtio, tick 3D; Spice display: tick OpenGL (if possible)
      - Begin installation

   b) Command line (OVMF paths for Arch; elsewhere: /usr/share/OVMF/)
      qemu-img create -f qcow2 ez.qcow2 30G
      cp /usr/share/edk2/x64/OVMF_VARS.4m.fd vars.fd
      qemu-system-x86_64 -enable-kvm -machine q35,vmport=off -cpu host -m 4096 -smp 4 \
        -drive if=pflash,format=raw,readonly=on,file=/usr/share/edk2/x64/OVMF_CODE.4m.fd \
        -drive if=pflash,format=raw,file=vars.fd \
        -drive file=ez.qcow2,if=virtio -cdrom EZ-OS-0.7.0-x86_64.iso \
        -device virtio-vga-gl -display gtk,gl=on -device qemu-xhci -device usb-tablet \
        -nic user,model=virtio -device intel-hda -device hda-duplex
      Without 3D: use  -device virtio-vga -display gtk  instead.
      After installing: run the same command WITHOUT "-cdrom EZ-OS-0.7.0-x86_64.iso".

   Inside the machine, your own desktop may keep the Super key: press Ctrl+Alt+G to grab the keyboard.

3. ON A REAL PC (at your own risk)
   - USB stick: Ventoy, balenaEtcher, or Rufus in DD mode.
   - In the firmware settings: UEFI, Secure Boot disabled.
   - Choose "Try EZ OS": nothing is written to your disks.
   - The installer then offers:
       * "Install alongside existing systems": uses UNPARTITIONED space (24 GB minimum, GPT disk). Nothing is erased.
         On Windows, make some first: Disk Management > right-click C: > Shrink Volume.
         Turn off BitLocker and fast startup first.
       * "Erase the disk and install EZ OS": all of it, half, or the size you want. !!! EVERYTHING ON IT IS LOST.
     Back up your important files in any case.

   - Desktop environment: Hyprland installs offline. KDE Plasma (0.9 GB) and GNOME (0.4 GB) are downloaded:
     plug in the network cable or connect Wi-Fi FIRST (Try > Quick settings).

4. FIRST STEPS (Hyprland desktop)
   Super+Space: applications     Super+Y: EZ Store     Super+I: settings
   Super+K: every shortcut       Super+L: lock

5. NOT THERE YET
   BIOS startup, Secure Boot, automatic shrinking of Windows, system updates.
   Not tried: real hardware, Wi-Fi, Bluetooth, sleep, several displays, music.

6. YOUR FEEDBACK HELPS: Wi-Fi? sound? screen size? crash (photo)? PC model?

License: GPL-3.0. Built on NixOS and Hyprland, not officially affiliated with them.
```
