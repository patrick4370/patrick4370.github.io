# Bluetooth

## Change Bluetooth Agent Name 

If you want to change the bluetooth device name permanently, you have to create a file called `/etc/machine-info` which should have the following content:

`PRETTY_HOSTNAME=device-name`

After this, restart the Bluetooth service:

`sudo service bluetooth restart`

## Change Location of Received Files

Blueman doesn't use a config file, instead using dconf.

I used dconf-editor and found the setting at:

`/org/blueman/transfer/shared-path`

Change to a path you require.

## Connecting a Device

*Installation*

1. Install the bluez package, providing the Bluetooth protocol stack.
2. Install the bluez-utils package, providing the bluetoothctl utility. Alternatively install bluez-utils-compatAUR to additionally have the deprecated BlueZ tools.
3. The generic Bluetooth driver is the btusb kernel module. Check whether that module is loaded. If it is not, then load the module.
4. Start/enable bluetooth.service.

Install bluetoothctl — Pairing a device from the shell is one of the simplest and most reliable options.
[bluez-utils][http://www.bluez.org/]

`sudo pacman -S bluez-utils`

*Pairing*

_Note: Before using the Bluetooth device, make sure that it is not blocked by rfkill._

The exact procedure depends on the devices involved and their input functionality. What follows is a general outline of pairing a device using bluetoothctl.

Start the bluetoothctl interactive command. Input help to get a list of available commands.

`bluetoothctl` and press <Enter>

```
$ bluetoothctl

[NEW] Controller 00:10:20:30:40:50 hostname [default]
[bluetooth]# agent KeyboardOnly
Agent registered

[bluetooth]# default-agent
Default agent request successful

[bluetooth]# power on
Changing power on succeeded
[CHG] Controller 00:10:20:30:40:50 Powered: yes

[bluetooth]# scan on
Discovery started
[CHG] Controller 00:10:20:30:40:50 Discovering: yes
[NEW] Device 00:12:34:56:78:90 device name
[CHG] Device 00:12:34:56:78:90 LegacyPairing: yes

[bluetooth]# pair 00:12:34:56:78:90
Attempting to pair with 00:12:34:56:78:90
[CHG] Device 00:12:34:56:78:90 Connected: yes
[CHG] Device 00:12:34:56:78:90 Connected: no
[CHG] Device 00:12:34:56:78:90 Connected: yes
Request PIN code
[agent] Enter PIN code: 1234
[CHG] Device 00:12:34:56:78:90 Paired: yes
Pairing successful
[CHG] Device 00:12:34:56:78:90 Connected: no

[bluetooth]# connect 00:12:34:56:78:90
Attempting to connect to 00:12:34:56:78:90
[CHG] Device 00:12:34:56:78:90 Connected: yes
Connection successful
```

_In some case, the mouse is paired but not moving when used. The device add to be trusted and unblocked. First of all open a terminal and run bluetoothctl_

Power off the bluetooth:

`[bluetooth] # power off`

Power on the bluetooth, then enable the pairing method on the mouse if needed:

`[bluetooth] # power on`

List the available bluetooth devices, you have to copy the mouse device ID XX:XX:XX:XX:XX:XX:

`[bluetooth] # scan on`

Unpair the device if already paired:

`[bluetooth] # remove XX:XX:XX:XX:XX:XX`

Put device in pairing mode (typically by long pressing a button, or a key combination on some keyboards). It will be detected by scan and displayed. Mind that the device ID may have changed (slightly), so copy the device ID shown by the scan.

Trust the device:

`[bluetooth] # trust XX:XX:XX:XX:XX:XX`

Pair the mouse with the computer:

`[bluetooth] # pair XX:XX:XX:XX:XX:XX`

Connect the computer with the mouse:

`[bluetooth] # connect XX:XX:XX:XX:XX:XX`

Unblock the device control:

`[M585/M590] # unblock`

Power the bluetooth off and on.

If the mouse does not work directly, just power off and power on the mouse.

In some cases, it may also be necessary to load the uhid kernel module. 

[Arch Linux](Arch_Linux.md)
