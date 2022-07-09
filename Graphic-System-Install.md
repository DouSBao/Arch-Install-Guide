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

# Section Two - Window Manager
1. Install i3-gaps (fork from i3, and has more features)
```
sudo pacman -S i3-gaps
```
2. Add the following line to the bottom of ~/.xinitrc, in order to automatic launch i3 when type command startx
```
exec i3
```

# Section Three - Terminal Emulator
1. Install alacritty
```
sudo pacman -S alacritty
```
2. In i3 config file, $HOME/.config/i3/config, under the comment "# start a terminal", change the default terminal to alacritty
```
# start a terminal
bindsym $mod+Return exec alacritty
```
3. To config alacritty, create file $HOME/.config/alacritty/alacritty.yml.
- For avaliable color scheme, refer to [color scheme](https://github.com/alacritty/alacritty/wiki/Color-schemes)
- For avaliable options of alacritty, refer to [alacritty config options](https://github.com/alacritty/alacritty/blob/master/alacritty.yml)
