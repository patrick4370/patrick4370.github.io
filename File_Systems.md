# File Systems

## UDF

To mount UDF file systems, such as the Microsoft Windows DVD do

`sudo mount -t udf file.iso /mount/point`

or

`sudo mount -t udf, iso13346 -o loop file.iso /media/iso13346`

## General Mounting ISO

To mount an ISO image using user space tools do

`udisksctl loop-setup -r -f file.iso`

It will return something like

> Mapped file File.iso as /dev/loop0.

Now we mount the loop device

`udisksctl mount -b /dev/loop0p1`

The `p1` denotes the partition number. The command will return a message like

> Mounted /dev/loop0p1 at /run/media/user/file_blah/

To unmount the ISO

`udisksctl unmount -b /dev/loop0p1`

This will return a message

> Unmounted /dev/loop0p1.

Now we will need to delete the loop device

`udisksctl loop-delete -b /dev/loop0`

There shouldn't be any messages if successful


crw-rw---- 1 root disk 10, 237 May  4 16:17 /dev/loop-control
brw-rw---- 1 root disk  7,   0 May  5 14:25 /dev/loop0

[Arch Linux](Arch_Linux.md)
