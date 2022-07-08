# Arch-Install-Guide
- This is a personal use and unprofessional guide of installing Arch Linux.
- This guide will use i3-gaps as window manager, and don't use any display manager. Which means, use tty as login shell, and manually type startx to start xorg server everytime.
- The guide will assume you have already prepared the usb to install the Arch, and have already get into the "tiny" arch window.
- Any <> appears in the command should be manually fixed and replaced by a suitable name.

# Section One - Connect To Wifi
1. Check whether the wifi is connect. If it is connect, ignore this section.
```
ping <website>
```
2. Check is dhcpcd.service service running
```
systemctl status dhcpcd.service
```
3. If is not enable, enable it, and start the service
```
systemctl enable dhcpcd.service
systemctl start dhcpcd.service
```
4. Use iwctl tool box.
```
iwctl
```
5. Show your wireless network card name.
```
device list
```
6. Use the first command to show the status of your network card.
   - If the status of "Powered" is off, then use second and the third command on turn it on.
   - If still not working, try **rfkill unblock all**
```
device <network card> show
device wlan0 set-property Powered on
adapter phy0 set-property Powered on
```
7. Connect to wifi
```
station <network card> connect <SSID>
```
8. Check if success
```
station <network card> show
```
9. Exit iwctl
```
exit
```
ps: If iwctl not works anyway, you could connect to cable, or connect your phone to the machine in order to use wifi. Then download NetworkManager, use nmcli or nmtui to connect to wifi.

# Section Two - Update mirrorlist source
1. Use reflector to update the package mirrorlist at /etc/pacman.d/mirrorlist
```
reflector --country China --age 24 --sort rate --protocol https --save /etc/pacman.d/mirrorlist
```
2. Synchronize package manager pacman
```
pacman -Syy
```
# Section Three - Update System time
1. Update the time
```
timedatectl set-ntp true
```
2. Check the status of time service
```
timedatectl status
```

# Section Four - Partition The Disk
1. Check the name of disk
   - Usually, the disk name will be /dev/sda, /dev/nvme0n1 or /dev/mmcblk0
```
fdisk -l
```
2. Use fdisk tool box
```
fdisl <disk path>
```
3. Type **m** for help, **d** to delete a partition, **n** to add a partition, etc. The help menu is specific enough.

# Section Fiv - 
