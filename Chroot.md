# Chroot

## Chrooting into Arch Linux

| NAME | MAJ:MIN | RM | SIZE   | RO | TYPE | MOUNTPOINTS |
|------|---------|----|--------|----|------|-------------|
| sda  | 8:0     | 0  | 465.8G | 0  | disk |             |
| sda1 | 8:1     | 0  | 512M   | 0  | part | /boot       |
| sda2 | 8:2     | 0  | 100G   | 0  | part | /           |
| sda3 | 8:3     | 0  | 365.3G | 0  | part | /home       |


` # mount /dev/sda2 /mnt `

` # mount /dev/sda1 /mnt/boot/efi`

` # mount /dev/sda3 /mnt/home`

` # chroot /mnt`

[Arch Linux](Arch_Linux.md)
