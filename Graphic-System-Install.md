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
3. Config i3


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

# Section Four - VPN (Optional)
1. If you are locate in China, or some other country where you can't access google, then you should read this section, and set up your VPN.
2. The guide will use Clash For Linux as cient. Therefore, you should subscribe only the node which support clash protocol.
3. If you can't find a place to pay for nodes, here is a link perhaps will help: [Link](https://www.yxrcr.com/#/login)

# Section Five - AUR Helper (Optional)
1. Commands
```
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```
- It's complete possiable to install package without AUR helper from AUR. Just simply clone from AUR link, and use **makepkg -si**.
- If **makepkg** is missing, you should install base-devel package through pacman.

# Section Six - Browser
1. If you have AUR helper
```
yay -S google-chrome
```
2. If you don't have AUR helper
```
git clone https://aur.archlinux.org/google-chrome.git
cd google-chrome
makepkg -si
```

# Section Six - 
