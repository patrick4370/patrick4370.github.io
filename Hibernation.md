# Hibernation 

To set up hibernation we need to create a swap file.

### Configure the initramfs 

When an initramfs with the base hook is used, which is the default, the resume 
hook is required in `/etc/mkinitcpio.conf`. Whether by label or by UUID, the swap 
partition is referred to with a udev device node, so the resume hook must go after 
the udev hook. This example was made starting from the default hook configuration:

`HOOKS=(base udev autodetect keyboard modconf block filesystems resume fsck)`

*Remember to regenerate the initramfs for these changes to take effect.*

### Create the swapfile

`sudo dd in=/dev/zero of=/swapfile bs=1G count=10 status=progress`
`sudo chmod 0600 /swapfile`
`sudo mkswap -U clear /swapfile`
`sudo swapon /swapfile`

Edit *_/etc/fstab_* and add the following line

`/swapfile none swap defaults 0 0`

### Required Kernel Parameters 

The kernel parameter `resume=<swap_device>` must be used.

To find the *UUID* for the swapfile, run the following

`findmnt -no UUID -T /swapfile`

_77fc844c-f045-4674-a644-4734dd51daa1_

Now we will find the offset for the swapfile by running

`filefrag -v /swapfile`

```
Filesystem type is: ef53
File size of /swapfile is 4294967296 (1048576 blocks of 4096 bytes)
 ext:     logical_offset:        physical_offset: length:   expected: flags:
   0:        0..       0:      38912..     38912:      1:            
   1:        1..   22527:      38913..     61439:  22527:             unwritten
   2:    22528..   53247:     899072..    929791:  30720:      61440: unwritten
...
```

We can add the kernel parameter of _swap_file_offset=_ with the value under the
output of physical_offset: in this case it is 38912.

## System does not power off when hibernating

When you hibernate your system, the system should power off (after saving the state on the disk). Sometimes, you might see the power LED is still glowing. If that happens, it might be instructive to set the HibernateMode to shutdown in sleep.conf.d(5):

`/etc/systemd/sleep.conf.d/hibernatemode.conf`

```
[Sleep]
HibernateMode=shutdown
```
With the above configuration, if everything else is set up correctly, on invocation of a systemctl hibernate the machine will shutdown saving state to disk as it does so. 

[Arch Linux](Arch_Linux.md)
