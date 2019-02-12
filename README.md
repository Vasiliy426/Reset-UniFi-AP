### What is it for?

This manual describes the way to reset Ubiquiti UniFi AP AC (Lite, PRO etc) access points.
![Just like these.](https://github.com/vasiq426/reset-ap/blob/master/unifi-ap-ac.jpg)

These APs have great value for it's money, but damn things tend to suddenly disconnect from the UniFi SDN controller PC software.
All steps described below reqire SSH access to your AP. Use standard SSH port 22/TCP, with login/password you set in the controller software. Default AP's login/password is ubnt/ubnt
If you can't SSH to your AP, you can manually reset AP via reset button near LAN port.

### Manual upgrade/rollback the AP's firmware

Connect via SSH to the AP, and then type:

```
# upgrade https://full/URL/to/the/firmware/firmwarename.bin
```
Copy the URL from the [AP's firmware download page](https://www.ubnt.com/download/unifi/unifi-ap-ac-lite). Doublecheck the compatibility of your device and the firmware you are about to download.

### Soft-reset

If the AP disappeared in the controller, or status is Disconnected/Heartbeat Lost, and the status is not changing, SSH to AP and type:

```
# set-default
```

this will clear the the AP's user settings. AP will reboot shortly after that.

### Hard-reset

For complete rollback to default settings, SSH to the AP, and type:

```
# syswrapper.sh restore-defaults
```

If there's running DHCP in the subnet the AP belongs to, AP will obtain free IP address, If not, default IP of the AP will be 192.168.1.20.

### Adopting the AP

For adopting the AP in the controller software, SSH to the AP and type:

```
# mca-cli
# set-inform http://ip-of-pc-with-the-controller:8080/inform
# exit
```

After that AP should appears in the controller, ready for adoption (pending).
