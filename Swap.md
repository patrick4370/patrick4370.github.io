
# Swap File Generation

### Create Swap

`sudo dd if=/dev/zero of=/swapfile bs=1M count=$(( X*1024 )) status=progress`

Where X is the swapfile size in Gb's

### Change Permissions 

`chmod 0600 /swapfile`

### Format Swap 

`mkswap -U clear /swapfile`

### Turn on swap

`swapon /swapfile`

### Add an entry to /etc/fstab

`/swapfile   none    swap    defaults    0 0`

### Hibernation Settings 

To identify the swapfile UUID run the following. 

`findmnt -no UUID -T /swapfile`

To find the swapfile offset run the following.

`filefrag -v /swapfile | awk '$1=="0:" {print substr($4, 1, length($4)-2)}'`

Update your boot loader with these kernel parameters

`resume=UUID=<UUID returned by the findmnt command> resume_offset=<Number returned by filefrag command>`

Add to your /etc/fstab

`/swapfile    none    swap    defaults    0 0`

[Arch](Arch)
