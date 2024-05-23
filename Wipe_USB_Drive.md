# Wipe USB Drive

Warning: This will irrevocably destroy all data on /dev/sdx. To restore the USB drive as an empty, 
usable storage device after using the Arch ISO image, the ISO 9660 filesystem signature needs to be removed by 
running `wipefs --all /dev/sdx` as root, before repartitioning and reformatting the USB drive.

[Arch Linux](Arch_Linux.md)
