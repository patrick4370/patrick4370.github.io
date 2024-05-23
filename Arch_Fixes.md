# Arch Fixes

## Fix “Warning: local is newer than community” Error In Arch Linux

If you get the following when running pacman to update:

`warning: youtube-dl: local (2017.01.22-1) is newer than community (2017.01.16-1)
nothing to do`

The following choices will fix the problem

This quick and dirty method SHOULD fix it, and update the packages as normal
`$ sudo pacman -Syu`

If that didn't work
`$ sudo pacman -Suu`

The above command will update all packages, then downgrade all affected packages.

And then, do the full upgrade using command
`$ sudo pacman -Syyu`

## Disable touchpad on laptop

Run xinput on the command line. This is the output -
Find the id for the touchpad and mouse 'nipple'.


```⎡ Virtual core pointer                          id=2    [master pointer  (3)]
   ⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]  
   ⎜   ↳ Logitech Wireless Mouse PID:0080          id=10   [slave  pointer  (2)]  
   ⎜   ↳ AlpsPS/2 ALPS DualPoint Stick             id=13   [slave  pointer  (2)]  
   ⎜   ↳ AlpsPS/2 ALPS DualPoint TouchPad          id=14   [slave  pointer  (2)]  
   ⎣ Virtual core keyboard                         id=3    [master keyboard (2)]  
       ↳ Virtual core XTEST keyboard               id=5    [slave  keyboard (3)]  
       ↳ Power Button                              id=6    [slave  keyboard (3)]  
       ↳ Power Button                              id=8    [slave  keyboard (3)]  
       ↳ Sleep Button                              id=9    [slave  keyboard (3)]  
       ↳ Dell WMI hotkeys                          id=11   [slave  keyboard (3)]    
       ↳ AT Translated Set 2 keyboard              id=12   [slave  keyboard (3)]  
       ↳ Video Bus                                 id=7    [slave  keyboard (3)]  
```

This shows the command for starting i3wm with devices disabled. [~/.config/i3/config]

`exec --no-startup-id xinput set-prop 14 "Device Enabled" 0`

`exec --no-startup-id xinput set-prop 13 "Device Enabled" 0`

## A start job is running for (At startup)

Go to `/etc/systemd/system/multi-user.target.wants/` and find the offending filename that comes up in the startup message and delete

[index](index.md)
