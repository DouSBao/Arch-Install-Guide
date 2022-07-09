# Section One - Basic: Xorg
1. Install basic xorg server and headers
```
sudo pacman -S xorg-server xorg-xinit libx11 libxinerama
```
2. Config xinit by cp the default config file to home page, and delete the lines at the botton of file. (xterm, etc)
```
cp /etc/X11/xinit/xinitrc ~/.xinitrc
nvim ~/.xinitrc
```
3. Install font required by xorg
```
sudo pacman -S ttf-dejavu ttf-droid ttf-hack ttf-font-awesome otf-font-awesome ttf-lato ttf-liberation ttf-linux-libertine ttf-opensans ttf-roboto ttf-ubuntu-font-family
```

