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
- Spend time on this! This section is important. You can use go through i3 default config file while read through the user guide, and edit the config, make it benefit and convenient you.

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
8. After you installed xorg, window manager and terminal Emulator, you should be able to run command **startx** and step into your graphic window. Here is some simple keybindings you could do inside i3
```
$mod+Enter -> (Open terminal)
$mod+Shift+q -> (Close window)
$mod+Shift+e -> (Exit i3, back to default window)
```
- For mod key, by default, it should be either Home or Alt. Depends on which you choice when you start i3 without a config file.
- For more infomation, you should read i3 user guide.

# Section Four - ALSA
1. Install alsa-utils package, which provides a easy-use interface to interact with alsa.
```
sudo pacman -S alsa-utils
```
2. List all sound cards
```
aplay -l
```
3. List current (default) sound card.
```
amixer scontrols
```
4. If the above command doesn't show 'Master', then something is going wrong. If you have muti sound cards, use option '-c <number>' to show whether another sound card is functioning.
```
amixer -c <sound card number> scontrols
```
5. Use command **alsamixer** step into the control window, follow the introduction shown on the top of window, select the correct sound card, and unmute all channels of it. Do the same thing to microphone.
6. Exit the control window. If you need to change the default sound card (which means when you do the step 3, Master is not detected), write the following to the file /etc/asound.conf
```
defaults.pcm.card <valid card number>
defaults.ctl.card <valid card number>
defaults.pcm.device <device number associated with the valid card number shown in step 2>
```
7. Reboot. The sound system should work now. Here is a website for quick [test](https://www.onlinemictest.com/)

# Section Five - Input Method
1. Install fcitx5 and associated packages
```
sudo pacman -S fcitx5 fcitx5-qt fcitx5-gtk fcitx5-configtool
```
2. Export the following variables at anywhere you like
```
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
```
3. Reboot
4. Add pinyin to input method via fcitx5-configtool
5. Here is a nice gruvbox skin for fcitx5 [here](https://github.com/ayamir/fcitx5-gruvbox)
  
# Section Four - Some Other Useful And Tiny Tools
1. Compton (Window animation and transparency)
2. Feh (Set wallpaper)
3. Neofetch (Display system info)
- Enable these tools by adding them in ~/.xinitrc file. So they will be lauched when startx.
- These tiny tools might not 100% associated with "graphic", but they surely will make you system better :)
