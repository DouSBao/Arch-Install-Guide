# Arch-Install-Guide
- This is a personal use and unprofessional guide of installing Arch Linux, and config it with i3-gaps and so on.
- The guide will assume you have already prepared the usb to install the Arch, and have already get into the "tiny" arch window.
- Some command will need to be manually fixed, and replace the temp part by a suitable name.
- The name in <> shoul dbe 

# Section One - Connect To Wifi
1. Try the following to check is the wifi connect
```
ping <website>
```
2. Use the following to get into iwd shell
```
iwctl
```
3. Use the following to show your wireless network card
```
device list
```
4. Use the following first command to show the status of your network card.
  - If the status of "Powered" is off, then use second and the third command on turn it on.
```
device <network card> show
device wlan0 set-property Powered on
adapter phy0 set-property Powered on
```
