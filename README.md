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
3. Type **m** for help, **d** to delete a partition, **n** to add a partition, **t** to change the partition type, etc. The help menu is specific enough.
4. Use **w** to exit, in order to save the change

# Section Fiv - Make File System
1. For efi partition, use
```
mkfs.vfat <partition path>
```
2. For swap partition
- To make the file system
```
mkswap <partition path>
```
- To enable the swap partition
```
swapon <partition path>
```
3. For linux file system
```
mkfs.ext4 <partition path>
```
ps: You could use lsblk **-f command** to show the type of partition in order to check 

# Section Six - Mount Partition
1. For linux file partition, mount at home
```
mount <linux file partition path> /mnt
```
2. For EFI partition
```
mkdir -p /mnt/boot/efi
mount <EFI partition path> /mnt/boot/efi
```

# Section Seven - Install Arch Linux System And Necessary Software
1. Install command
   - linux: kernel
   - linux-firmware: firmware
   - linux-headers: some common headers will need
   - base: base packages
   - base-devel: packages for developer, include gcc, g++, make, cmake, etc.
```
pacstrap /mnt linux linux-firmware linux-headers base base-devel
```

# Section Eight - Generate EFI Table
1. Generate command
```
genfstab -U /mnt >> /mnt/etc/fstab
```
ps: It is highly recommand to cat the file and check the correctness. It should include and only include the name of your partition and their detail information

# Section Nine - Step Into Installed Arch
1. Command
```
arch-chroot /mnt
```

# Section Ten - Set Time Zone
1. Command
```
ln -sf /usr/share/zoneinfo/<Region>/<City> /etc/localtime
```
2. Generate /etc/adjtime
```
hwclock --systohc
```
ps: For Chinese user, the Region is going to be Asia, and City is going to be Shanghai

# Section Eleven - Localization
1. Uncomment the locale you want in the file /etc/locale.gen
2. Generate locale infomation
```
locale-gen
```
3. Create file /etc/locale.conf, and set variable LANG to the locale you just uncomment. (Example: LANG=en_US.UTF-8)
ps: For most of user, you should uncomment en_US.UTF-8 UTF-8. For Chinese user, a better way is to uncomment en_GB.UTF-8 or en_SG.UTF-8 in order to have 24 hours, US standered measurement unit. It is not recommand to set locale as Chinese, since it could result in tty display wrong code.

# Section Twelve - Set Up Network Config
1. Set up host name
```
vim /etc/hostname
```
2. Add the following to the file /etc/hosts
```
127.0.0.1        localhost
::1              localhost
127.0.1.1        <host name>.localdomain        <host name>
```

# Section Thirteen - User Setting
1. Set root password
```
passwd
```
2. Create new user for daily use, and set the password for it
```
useradd -m <new user name>
passwd <new user name>
```
3. Give new user necessary permission by adding it to some groups
```
usermod -aG wheel,audio,video,optical,storage <user name>
```

# Section Thirteen - Install And Config Necessary Packages
1. Following packages are recommanded
   - grub, efibootmgr, efivar (about boot)
   - networkmanager (about network)
   - amd-ucode (or intel-ucode, depends on which cpu you use)
   - sudo (allow wheel group user has root permission)
```
pacman -S grub efibootmgr efivar networkmanager amd-ucode sudo
```
2. Install grub
```
grub-install <path to the disk>
```
3. Change the window resolution in file /etc/default/grub
4. Make grub config
```
grub-mkconfig /boot/grub/grub.cfg
```
5. Enable networkmanager daemon
```
systemctl enbale NetworkManager
```
6. Config sudo, uncomment the line "%wheel ALL=(ALL) ALL" (might be slight different)
```
EDITOR=nvim visudo
```

# Section Fourteen - Finish The Basic Install
1. Exit and umount the partition.
```
exit
umount /mnt/boot/efi
umount /mnt
```
