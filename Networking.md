# Networking

## Networking using systemd-networkd

1. Stop all running instances of any network managers
2. Start the systemd-networkd Network Manager `sudo systemctl enable systemd-networkd` and `sudo systemctl enable systemd-resolved`
3. Run `ip a` to view interfaces and make sure they are all down. Take note of the interface names. In my case `eno1` and `wlp2s0`
4. Change directory to `/etc/systemd/network` and create file(s) for each interface you have
   `/etc/systemd/network/10-eno1.network`
   ```
   
    [Match]
    Name=eno1

    [Network]
    DHCP=yes
   ```
   
   `/etc/systemd/network/20-wlp2s0.network`
   ```
   
    [Match]
    Name=wlp2s0

    [Network]
    DHCP=ipv4
    IgnoreCarrierLoss=3s
   ```   
   
   wlp2s0 is the Wifi interface and eno1 is the ethernet interface

[Arch Linux](Arch_Linux.md)


