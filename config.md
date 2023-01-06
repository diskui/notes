things i will do after the installation of the (arch-based) `linux` system:

install gnome:

```shell
pacman -S gnome --needed

systemctl enable gdm
```

add `archlinuxcn` source:

```shell
echo -e "[archlinuxcn]
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/\$arch" >> /etc/pacman.conf
pacman -Sy
pacman -S archlinuxcn-keyring
pacman -S paru
```

configure the proxy:

```shell
#install clash
paru -S clash-for-windows-bin
# or use the tar file temporarily
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
paru -S google-chrome visual-sdudio-code-bin jetbrains-toolbox typora
```

configure git and generate an ssh key:
```shell
git config --global user.name "linux"
git config --global user.email kaxiford@gmail.com
git config --global core.editor "nvim"
ssh-keygen -t ed25519 -C "kaxiford@gmail.com"

#add to github
```

configure ibus:

```shell
 # set the environment varibles
 sudo echo -e "GTK_IM_MODULE=ibus
 XMODIFIERS=@im=ibus
 QT_IM_MODULE=ibus" >> /etc/envrionment
 
 ibus-setup
 # add the input method and do the same in gnome settings
 # set the ctrl+space keyshortcut for switch input method as well the flameshot keyshortcut
```

enable copying to clipboard of zathura:

```shell
mkdir ~/.config/zathura
echo 'set selection-clipboard clipboard' >> ~/.config/zathura/zathurarc
```

