# Section Two - AUR Helper (Optional)
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
