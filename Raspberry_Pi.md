# Raspberry Pi

## Installing The OS 

Use the [Raspberry Pi Imager](https://www.raspberrypi.com/software/|Raspberry Pi Imager) to install to SD Card.

1. Select OS to install in the Imaging software
2. Answer questions regarding SSH, username etc
3. Choose SD Card to image.

## Boot the Rpi

Insert the SD Card into the Pi. Power and boot. SSH into the board and do the following. This is a new security feature. Not doing this will lock you out when trying to SSH into the Pi.

* Create a file in `/boot` called `userconf.txt`
* Run `openssl passwd -6` and copy the output. The output will look like 
  `$6$Crz3ILyzn.Cqw8WK$mpVW7yVI0KAOO4QfEvN/2RW1oCkbeKSpUE5zvCfonK8YZhUdC7tLrhS2BrvzxMMjDvj5GXI/gshZF/Q1vyhXv0`
* In the `userconf.txt` file, add the username and *openssl* output as `username:$6$Crz3ILyzn.Cqw8WK$mpVW7yVI0KAOO4QfEvN/2RW1oCkbeKSpUE5zvCfonK8YZhUdC7tLrhS2BrvzxMMjDvj5GXI/gshZF/Q1vyhXv0`
 
## Static IP Setup

In the `/etc/dhcpcd.conf` file add the following -

```conf
interface eth0
static ip_address=192.168.10.2/24
static routers=192.168.10.1
static domain_name_servers=192.168.10.1
```

## Does Client Send Hostname?

Run `nmcli connection show --active`

The output will look like

```
NAME             UUID                                  TYPE  DEVICE
TelstraF04697 1  0d885f3c-9381-43c9-a1fc-e10f11e1be73  wifi  wlan0
```

Run the following to check if Client returns hostname to DNS Server

`nmcli connection show TelstraF04697 | grep send-hostname`

It will return something like the following

```
ipv4.dhcp-send-hostname:                yes
ipv6.dhcp-send-hostname:                yes
```

If the values are no, change them to yes like so

```
sudo nmcli con mod <connection name> ipv4.dhcp-send-hostname yes
sudo nmcli con mod <connection name> ipv6.dhcp-send-hostname yes
sudo nmcli con reload
```
[Index](index.md)
