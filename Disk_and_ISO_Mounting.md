# Mounting ISO images

Use this technique to mount UDF based images such as Windows ISO's.

`udisksctl loop-setup -r -f isofile.iso`

It will return 

> Mapped file isofile.iso as /dev/loop0.

To mount the image

`udisksctl mount -b /dev/loop0`

It will return

> Mounted /dev/loop0 at /run/media/user/some_name

To unmount

`udisksctl unmount -b /dev/loop0`

It will return

> Unmounted /dev/loop0.

To delete the loop device

`udisksctl loop-delete -b /dev/loop0`

Nothing will be returned if successful

[Arch Linux](Arch_Linux.md)
