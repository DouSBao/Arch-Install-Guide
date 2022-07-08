# Arch-Install-Guide
A personal use, unprofessional guide of installing and config Arch Linux
Ignore the preparation of iso in usb. The guide will start at successfully step into the tiny Arch in the usb.

# Step One - Connect To Wifi
1. Try ping <website>, if no error occur, jump to next step section
2. Use command 'iwctl' to step into iwd tool box.
3. Use command 'device list' to show the wireless network card you have
4. Use command 'device <network card> show' to display the status of the card.
  a. If the 'powered' is shown as 'off', then use command 'device <network card> set-property Powered on' or command 'adapter <adapter> set-property        Powered on' to turn the power on.
