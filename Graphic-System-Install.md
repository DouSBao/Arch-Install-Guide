# Section One - Xorg
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
4. Install gpu driver (amd)
```
sudo pacman -S xf86-video-amdgpu xf86-video-ati mesa vulkan-radeon
```
5. Install gpu driver (intel)
```
sudo pacman -S xf86-video-intel vulkan-intel mesa
```
6. Install gpu dirver (nvidia)
```
sudo pacman -S nvidia nvidia-settings nvidia-utils
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
3. For config i3, refer to [i3 User Guide](https://i3wm.org/docs/userguide.html).


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
4. Most terminal application will use nerd font icon. Therefore, you should find one that you like from [patched font](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts), and install Regular, Italic, Bold, and Bold-Italic. Either ttf or otf is acceptable.
5. If you want to apply the font downloaded only for the current user, you should create fonts directory at $HOME/.local/share/. Relatively, you could create fonts directory at /usr/local/share/ Most common font directory structure will looks like this:
```
$HOME/.local/share/fonts
+ ttf
| + hack
| | + Regular.ttf
| | | Bold.ttf
| | | Italic.ttf
| | | Bold-Italic.ttf
| + victor
| | + Regular.ttf
| | | Bold.ttf
| | | Italic.ttf
| | | Bold-Italic.ttf
+ otf
| + hack
| | + Regular.otf
| | | Bold.otf
| | | Italic.otf
| | | Bold-Italic.otf
| + victor
| | + Regular.otf
| | | Bold.otf
| | | Italic.otf
| | | Bold-Italic.otf
= = =
```
6. Run the command in order to reload fonts into cache. (So they could be used)
```
fc-cache -vf
```
7. Show the exact name of fonts, so you could use it in alacritty.yaml file
```
fclist | grep <rough name of font>
```

# Section Four - VPN (Optional)
1. If you locate in China, or some other country where you can't access google, then you should read this section, and set up your VPN.
2. The guide will use Clash For Linux as cient. Therefore, you should subscribe only the node which support clash protocol.
3. If you can't find a place to pay for nodes, here is a link perhaps will help: [Link](https://www.yxrcr.com/#/login)
4. Download the Clash For Linux clien, unzip it, and make it executable
```
wget https://github.com/Dreamacro/clash/releases/download/v1.10.0/clash-linux-amd64-v1.10.0.gz
gunzip clash-linux-amd64-v1.10.0.gz
mv clash-linux-amd64-v1.10.0 clash
chmod u+x clash
```
5. Execute clash, it will try to download Country.mmdb file for you. If the speed is slow, manually download it from [here](https://github.com/Dreamacro/maxmind-geoip/releases). If you manually download it, remember to copy the file to $HOME/.config/clash
6. Use this tool to convert the subscribe link, which you can find at subscribe page, to short URL, via this [tool](https://converter.niallapi.top/)
7. Download the config.yaml file via the short URL
```
curl -L -o config.yaml <short URL>
```
8. Launch clash again, if success, you should see different message. If you have a browser, you could try to accss youtube in order to verify this.
9. In order to enable clash as a daemon, run the follow commands
```
sudo mkdir /etc/clash
sudo cp clash /usr/local/bin
sudo cp config.yaml /etc/clash/
sudo cp Country.mmdb /etc/clash/
```
10. Copy the following content to /etc/systemd/system/clash.service
```
[Unit]
Description=Clash daemon, A rule-based proxy in Go.
After=network.target

[Service]
Type=simple
Restart=always
ExecStart=/usr/local/bin/clash -d /etc/clash

[Install]
WantedBy=multi-user.target
```
11. Enable the service
```
sudo systemctl enable clash
```
12. Launch the clash and check whether it's working normally.
```
sudo systemctl start clash
sudo systemctl status clash
```

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
3. (Optional) Install key binding extension for chrome. [Link](https://chrome.google.com/webstore/detail/shortkeys-custom-keyboard/logpjaacgmcbpdkdchjiaagddngobkck?hl=en)

# Section Seven - Some Other Useful But Tiny Tools
1. Compton (Window animation and transparency)
2. Feh (Set wallpaper)
3. Neofetch (Display system info)
- Enable these tools by adding them in ~/.xinitrc file. So they will be lauched when startx.
