# Raspbian plus NodeJS Image for Raspberry Pi Development
A disk image suitable for NodeJS development on Raspberry Pi

## Contains
- Raspbian GNU/Linux 7
- Raspberry Pi Firmware 3.12.24+
- npm 1.4.3
- NodeJS 0.10.26
- Git 1.7.10.4

## Instructions for Linux

Tested on a Samsung Chromebook.

> **Measure twice, cut once!** The following can destroy your filesystem. Ensure you are targeting the removable device you intend to before hitting that [Enter] key!

1. Download and unzip the xxx.img file to a suitable directory
1. Determine the name of your removable disk. Try using `dh -f` to list all partitions. On my Samsung Chromebook my SD card shows up as /dev/mmcblk1.
1. Unmount all partitions using `sudo umount /dev/<device>pn` where n is each partition number. 
1. Raw copy the image to the SD card with `sudo dd if=<path-to-image>/imagename of=/dev/<device>`. You are targeting the device and not any particular partition. It goes without saying that this command will destroy all data in all partitions on the device! The dd command does not provide any progress feedback and does take some time.
1. Place the SD card in your Raspberry Pi SD card slot and power up with a keyboard and monitor attached.
1. Login with default username and password of pi/raspberry
1. `sudu nano /etc/wpa_supplicant/wpa_supplicant.conf` and change the ssid and psk values to your SSID and key respectively. The current setup assumes WPA2-Personal and AES or TKIP. If your network is configured otherwise you may need to edit other settings.
1. Reboot your Pi and confirm it is picking up your wireless network
2. Confirm the development stack is present with `node -v`, `npm -v` and `git --version`

## Next Steps
This image uses the default pi/raspberry username and password. You should seriously consider changing the password as well as create a new non-root user. The .bashrc file in /etc/skel contains a path to the NodeJS bin folder so new users should inherit that by default.

This image was created in July 2014. Shit happens and it is now out of date. Run `sudo apt-get update` and `sudo apt-get upgrade` to get the latest system changes. Also consider upgrading the versions of NodeJS and Git if they have changed too.

## Future Enhancements

I use MongoDB a lot so I will probably add that to the next version. 