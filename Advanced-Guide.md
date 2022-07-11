# Introduction
- This guide is optional and completely personal prefer. I suggest you don't follow the sequence to read, but read the part which you interested first.

# Section One - VPN
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

# Section Two - AUR Helper
1. Commands
```
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```
- It's complete possiable to install package without AUR helper from AUR. Just simply clone from AUR link, and use **makepkg -si**.
- If **makepkg** is missing, you should install base-devel package through pacman.

# Section Three - Browser
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

# Section Four - Polybar
1. Install polybar though pacman
```
sudo pacman -S pacman
```
2. Create launch script at $HOME/.config/polybar/launch.sh
```
#!/bin/zsh

killall -q polybar

while pgre -u $UID -x polybar > /dev/null; do
        sleep 1
done

polybar <polybar bar section name> 2>&1 | tee -a /tmp/polybar.log & disown
```
3. Make script executable
```
chmod +x launch.sh
```
4. Always launch polybar when i3 restart. Add the following to i3 config
```
exec-always --no-startup-id $HOME/.config/polybar/launch.sh
```
5. Config polybar through [user guide](https://github.com/polybar/polybar/wiki)
- ps: Polybar is not hard to config. You should spent some time on the user guide and make your own! It worses :)

# Section Fix - TODO
