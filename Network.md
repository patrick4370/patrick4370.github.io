# Network

## AutoFS 

_Setting up_

Install *autofs*

`pikaur -S autofs`

Edit the file `/etc/autofs/auto.master`

```
# Include /etc/autofs/auto.master.d/*.autofs
# To add an extra map using this mechanism you will need to add
# two configuration items - one /etc/autofs/auto.master.d/extra.autofs file
# (using the same line format as the auto.master file)
# and a separate mount map (e.g. /etc/auto.extra or an auto.extra NIS map)
# that is referred to by the extra.autofs file.
#
+dir:/etc/autofs/auto.master.d
#
# If you have fedfs set up and the related binaries, either
# built as part of autofs or installed from another package,
# uncomment this line to use the fedfs program map to access
# your fedfs mounts.
#/nfs4  /usr/sbin/fedfs-map-nfs4 nobind
#
# Include central master map if it can be found using
# nsswitch sources.
#
# Note that if there are entries for /net or /misc (as
# above) in the included master map any keys that are the
# same will not be seen as the first read key seen takes
# precedence.
#
+auto.master

# Read the file /etc/autofs/auto.nfs for the mount information
/mnt/nfs	/etc/autofs/auto.nfs	--timeout=60

```
  
Create a *auto.nfs* file (`/etc/autofs/auto.nfs`)

```
backup 		-fstype=nfs,rw,async,vers=3    192.168.10.3:/media/backup
documents 	-fstype=nfs,rw,async,vers=3    192.168.10.3:/media/documents
kit		    -fstype=nfs,rw,async,vers=3    192.168.10.3:/media/kit	
```

This contains the mount points relative to `/mnt/nfs/` where the directories get created on demand. Use `showmount -e <server>` to get shares served by the server.

## systemd-networkd

To renew a lease on an interface, run `networkctl renew <interface>`

## wpa_supplicant:wq

Create a *wpa_supplicant* file for the particular interface. E.g., my wifi card has an interface name of `wlp2s0` so the file name will be `wpa_supplicant-wlp2s0.conf`. This will contain the following

```
/etc/modprobe.d/bonding.configuration
---
# Giving configuration update rights to wpa_cli
   2 ctrl_interface=/run/wpa_supplicant
   3 ctrl_interface_group=wheel
   4 update_config=1
   5
   6 # ISO/IEC alpha2 country code in which the device is operating
   7 country=AU
   8
   9 network={
  10     ssid="TelstraF04697"
  11     psk=Add your PSK here
  12 }
```
[Index](index.md)
