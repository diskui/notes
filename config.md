things i will do after the installation of the (arch-based) `linux` system:

install gnome:

```shell
pacman -S gnome sddm --needed

systemctl enable sddm
```

add `archlinuxcn` source:

```shell
echo -e "[archlinuxcn]
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/\$arch" >> /etc/pacman.conf
pacman -Sy
pacman -S archlinuxcn-keyring
pacman -S yay
```

configure the proxy:

```shell
#install clash
yay -S clash-for-windows-bin
# or use the tar file temporarily
echo "http_proxy=\"127.0.0.1:7890\"
https_proxy=\"127.0.0.1:7890\"
socks5_proxy=\"127.0.0.1:7890\"" >> /etc/envrionment
```

install `zsh` and `oh-my-zsh`, with some plugins: `git`, `zsh-autosuggestion`, `zsh-syntax-highlighting`, and `zsh-vi-mode`

```bash
# install zsh
pacman -S zsh --needed

#change to normal user
# install oh my zsh
git clone https://github.com/ohmyzsh/ohmyzsh.git
cd ohmyzsh/tools/
./install.sh
cd ../../
sudo rm -rf ohmyzsh

# install plugins
git clone https://github.com/zdharma-continuum/fast-syntax-highlighting.git \
  ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/fast-syntax-highlighting
  
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

git clone https://github.com/jeffreytse/zsh-vi-mode \
  $ZSH_CUSTOM/plugins/zsh-vi-mode
  
# replace the configuration file
echo -e "plugins=(
	git
	zsh-autosuggestions
	fast-syntax-highlighting
	zsh-vi-mode
	)
	source \$ZSH/oh-my-zsh.sh" >> ~/.zshrc

```

install some packages:

```shell
pacman -S wl-clipboard bitwarden telegram-desktop firefox \
ranger zathura zathura-pdf-mupdf foliate  spotify\
flameshot xdg-desktop-portal-gnome xdg-desktop-portal btop proxychains drawing --needed
```

some `aur` packages:

```shell
yay -S google-chrome visual-studio-code-bin jetbrains-toolbox typora --needed
```

configure git and generate an ssh key:
```shell
git config --global user.name "linux"
git config --global user.email kaxiford@gmail.com
git config --global core.editor "nvim"
ssh-keygen -t ed25519 -C "kaxiford@gmail.com"

#add to github
```

install and configure ibus:

```shell
 # set the environment varibles
 echo -e "GTK_IM_MODULE=ibus
 XMODIFIERS=@im=ibus
 QT_IM_MODULE=ibus" >> /etc/envrionment
 
 ibus-setup
 # add the input method and do the same in gnome settings
 # set the ctrl+space keyshortcut for switch input method as well the flameshot keyshortcut
```

or use fcitx5:

```shell
pacman -S fcitx5-im fcitx5-chinese-addons fcitx5-pinyin-zhwiki fcitx5-nord
yay -S fcitx5-input-support

# set audo-start
```



enable copying to clipboard of zathura:

```shell
mkdir ~/.config/zathura
echo 'set selection-clipboard clipboard' >> ~/.config/zathura/zathurarc
```

