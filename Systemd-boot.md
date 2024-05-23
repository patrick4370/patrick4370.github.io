
## Systemd-boot 

During install mount the FAT32 EFI partition to `/boot`

So, if we have a drive partitioned as below, the mount points will look like:

``` 
NAME   FSTYPE FSVER LABEL       UUID                                 FSAVAIL FSUSE% MOUNTPOINTS
sda                                                                                 
├─sda1 vfat   FAT32             4759-D82F                              16.9M    97% /boot
├─sda2 ext4   1.0               90ac2f2d-af88-4a35-9782-883a0b92106e     74G    19% /
└─sda3 ext4   1.0               936f578b-7ac2-4188-8d51-351d2fc04a26  294.3G    13% /home
``` 

In the `arch-chroot` environment execute the following:

`bootctl install`

We then edit the file `/boot/loader/loader.conf`

I use the following entries:

```
# /boot/loader/loader.conf
default arch-zen.conf
timeout 5
console-mode keep
editor 1
```

The entries for booting are located in the `/boot/loader/entries/` directory.

A typical entry file looks like the following:

```
title   Arch Linux Zen
linux   /vmlinuz-linux-zen
initrd  /intel-ucode.img
initrd  /initramfs-linux-zen.img
options root="UUID=90ac2f2d-af88-4a35-9782-883a0b92106e" rw
```

Add more entries as you see fit.

[Arch](Arch)
